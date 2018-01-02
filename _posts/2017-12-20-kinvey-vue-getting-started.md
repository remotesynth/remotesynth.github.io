---
layout: post
title: "Getting Started with Kinvey mBaaS - A Simple Vue App"
date: "2017-12-20"
categories:
    - Kinvey
description: Converting the previous example to work in a Vue app
comments: true
---

Following up on my [prior post](https://www.remotesynthesis.com/blog/kinvey-anonymous-data), I wanted to try to integrate the [Kinvey HTML5 (i.e. JavaScript) SDK](https://devcenter.kinvey.com/html5/downloads) into a Vue app. [Kinvey](https://www.kinvey.com/) already provides pre-built SDKs for some frameworks such as Angular, AngularJS and, though it isn't as commonly used anymore, Backbone. However, if you are using a different framework like Vue or React, you can still leverage the JavaScript SDK.

I had two goals with my Vue integration:

* Abstract out the anonymous login process that I showed in the prior post and notify the rest of the app that data is ready to be pulled.
* Isolate the Kinvey integration so that we just need to import the one module which already includes the SDK integration wherever it is needed in the app.

In this post I'll share my current project. Keep in mind that I am new to Vue, so I am very open to ideas for improvement. I'll reserve the option to revise, even drastically, as I build out a real app (in fact, I already did a total refactor of this once after realizing I may have taken a less-than-optimal initial approach). Also, the current status of this app is only pulling the same anonymous data as in the prior post. You can find the [sample code on GitHub](https://github.com/remotesynth/basic-kinvey-vue-web).

Ok. Enough caveats...let's take a look.

## A Very Simple App

This app pulls the list of Zelda shrines and displays them much the same as in the pure HTML/JavaScript example prior. To set this up, I only created two Vue components.

A root component that really just holds the list for now:

```html
<template>
  <div id="app">
    <shrines-list></shrines-list>
  </div>
</template>

<script>
import ShrinesList from './components/shrines-list.vue'

export default {
  name: 'app',
  components: {
    'shrines-list': ShrinesList
  }
}
</script>
```

And the shrines list component that has the following template (I'll share the JavaScript that populates the list later):

```html
<template>
<div>
<ul>
  <li v-for="shrine in shrines" :key="shrine._id">
    {{ shrine.name }}
  </li>
</ul>
</div>
</template>
```

Finally, when I create the app, I imported my kinvey-vue component (which I'll show in a moment) and put it in an app global scope. This allows me to access it from any component in my app.

```javascript
import kinvey from './kinvey-vue/index'
import Vue from 'vue'
import App from './App.vue'

Vue.prototype.$kinvey= kinvey;

new Vue({
  el: '#app',
  render: h => h(App),
});
```

So my app was set up, but now I needed a build the module to connect to Kinvey.

## A Simple Kinvey Vue Module

To get this app started I created what is the start of a reusable Kinvey Vue module that initiates the anonymous connection as soon as it is created (note that if your app doesn't ever get anonymous data from Kinvey then, obviously, you wouldn't want to do it this way). I also abstracted out the Appkey and AppSecret used to connect to Kinvey to make it easier to reuse this without having to modify the source.

Here's the code and I'll discuss it in detail after:

```javascript
import Vue from 'vue'
import { Kinvey } from 'kinvey-html5-sdk'
import KinveyConfig from './kinvey-config'

const KinveyVue = new Vue({
    data: {
        appkey: KinveyConfig.APPKEY,
        appsecret: KinveyConfig.APPSECRET,
        activeUser: null,
        isConnected: false,
        DataStoreType: Kinvey.DataStoreType
    },
    created() {
        var client = Kinvey.init({
            appKey: this.appkey,
            appSecret: this.appsecret
        });
        this.activeUser = Kinvey.User.getActiveUser(client);

        if (!this.activeUser) {
            var that = this;
            console.log('signing up');
            Kinvey.User.signup()
                .then(function(user) {
                    that.activeUser = user;
                    that.isConnected = true;
                    that.$emit('kinvey-connected');
                }).catch(function(error) {
                    console.log(error);
                });
        }
        else {
            console.log('user exists');
            this.isConnected = true;
            this.$emit('kinvey-connected');
        }
    },
    methods: {
        getCollection(collectionName,datastoretype) {
            return Kinvey.DataStore.collection(collectionName,datastoretype);    
        }
    }
});

export default KinveyVue;
```

The `created()` method is basically the code from my prior plain HTML/JavaScript example with some minor differences (and a few console logs that help visualize what was happening and when as the app ran). The key differences are:

* Rather than directly call a method to begin getting the shrine data, I announce an event notifying the app that we are logged in and connected. This way _any component_ needing data can then know that it is ok to request it.
* I set an `isConnected` flag within the component. The reason for this is that when the login is already cached in local storage, this process happens _very fast_. In my testing this meant that the event was often announced before the application even full loaded, meaning that the Vue app never even caught it. As I'll show, this flag helped me fix that issue.

Right now I also added a `getCollection()` method that returns a connection to a Kinvey collection/data store. I tried numerous ways of handling this and tried including the entire call but due to the fact that the call for the data returns a promise I kept running into difficulties within the component responding to this when the asynchronous call was returned. This could be my own naivete and I may return to this later as I revise and expand the app.

Lastly, let's look at how I integrated this into the shrines list component.

## Integrating with a Vue Component

I'm going to go back to my shrines list component and add the script to connect to Kinvey and then pull the data.

```javascript
export default {
    data() {
      return {
        shrines: [{'_id':'0','name':'Loading...'}]
      }
    },
    methods: {
      getShrines() {
        var datastore = this.$kinvey.getCollection('shrines',this.$kinvey.DataStoreType.Network),
          stream = datastore.find(),
          that = this;
        stream.subscribe(function onNext(item) {
          that.shrines = item;
        }, function onError(error) {
          console.log(error);
        }, function onComplete() {
          //...
        });
      }
    },
    created() {
      this.$kinvey.$on("kinvey-connected",this.getShrines);
      // if it's already connected
      if (this.$kinvey.isConnected) {
        console.log('loaded on created');
        this.getShrines();
      }
    }
}
```

To start I created a shrines array in my data object (populated with a dummy item to start). When the component is `created()`, I attach an event listener to the custom `kinvey-connected` event from my module. If the connection exists, we call the method to `getShrines()`. In addition, I check if the connection already exists and, if so, call `getShrines()`. I'm not thrilled with this duplication but as I explained earlier, when the connection was cached in local storage, the event seemed to be being announced _before_ this component's `created()` method was even triggered.

The code for getting the shrines is basically the same as the basic HTML/JavaScript example from my prior post with two small changes. The first is that I use my `getCollection()` method from the kinvey-vue module to connect to the collection in Kinvey. Why? This way I don't need to worry about importing the Kinvey SDK or any other code that might be necessary within every component that needs data from Kinvey - it's already there and available. The second change is that rather than push the items on the DOM directly, I am adding them to the `shrines` array and Vue takes care of updating the UI.

## Next Steps

Obviously this example is very simple and a bit contrived. I plan to build out a more complete and realistic Vue app as I move forward - adding in actual user authentication, sync and updating data. As I mentioned before, this is a learning process and experimentation. I'll share as I go along and I'm hoping that my initial module here will hold up as my application expands. And if anyone has suggestions on how I could improve this or approach it better, I'd love feedback.