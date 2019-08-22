---
layout: post
title: Getting Started with Offline Data in Web Apps Pt. 3
date: '2019-08-22'
description: A guide to getting started with IndexedDB for storing large amounts of complex data offline.
categories:
  - javascript
  - web development
comments: true
---

In [part 1](https://dev.to/remotesynth/getting-started-with-offline-data-in-web-apps-pt-1-136a) of this series, we looked at APIs to determine the online/offline and connection status of the user. In [part 2](https://dev.to/remotesynth/getting-started-with-offline-data-in-web-apps-pt-2-39o2), we looked at storing small amounts of data offline using LocalStorage. In this part, we're going to begin to look at how you can store large amounts of complex data offline using IndexedDB.

## What Is IndexedDB?

If you've used a NoSQL data store, you'll feel relatively comfortable with how IndexedDB works. Like LocalStorage, values in IndexedDB stores data in key value pairs, but, unlike LocalStorage which only has string values, the values can be complex objects. As you'd expect, the key must be unique but it can be a property of the object.

I'm going to be honest here, IndexedDB is not the simplest thing in the world. It's certainly far more than I can cover in detail here, but the key things to understand about IndexedDB are that it is:

* **Asynchronous** - Unlike LocalStorage, storing and retrieving data in IndexedDB will not block the UI.
* **Optimized for storing large amounts of data** - As the name implies, object stores within IndexedDB are indexed, offering a means to quickly retrieve values based upon those indexes rather than iterating over all records using a cursor. I should note that if your index is not unique, you'll still need to open a cursor to get all results for a given index value. Like I said, IndexedDB isn't simple.
* **Handles complex data** - Typically any site will have a single IndexedDB database, but that database can contain any number of object stores. As the name implies, an object store is designed for storing objects.
* **Large storage limits** - The exact size of the storage limit is difficult to specify as it is dynamic and dependent on available disk space, but can get into GBs of storage (Raymond Camden has an somewhat dated but still interesting post on [testing the storage limits of IndexedDB](https://www.raymondcamden.com/2015/04/17/indexeddb-and-limits).
* **Transactional** - Every read and write in IndexedDB must occur within the context of a transaction. For anyone familiar with how traditional transactional SQL databases work, this will seem familiar. In short, transactions ensure that a set of database operations is completed from beginning to end - a failure at any point rolls back the entire transaction. 
* **SQL-less** - IndexedDB has no means of querying using a query language like SQL. To be searchable, a value must be indexed and even then you cannot text search a value using something similar to SQL's `LIKE`. It's also not terribly simple to handle situations where you'll need to search based upon multiple indexes.

So, my simple and quick overview isn't exactly simple or quick. I recommend reading the [basic concepts of IndexedDB](https://developer.mozilla.org/en-US/docs/Web/API/IndexedDB_API/Basic_Concepts_Behind_IndexedDB) on MDN if you want to understand more.

## Getting Started with IndexedDB

In this section, we'll look at some of the basics to get started working with IndexedDB to store data. I'll walk through building a very simple page that loads data from the [Cocktail API](https://www.thecocktaildb.com/api.php) and then stores it locally in IndexedDB so that it can be retrieved faster and/or offline for subsequent page loads.

### Creating the Database

There is a bit of boilerplate that goes into creating the database.

```javascript
let db;
let dbRequest = window.indexedDB.open("Cocktaildb", 1);

dbRequest.onerror = function(event) {
  alert("Database error: " + event.target.errorCode);
};
dbRequest.onsuccess = function(event) {
  db = event.target.result;
  getCocktails();
};
dbRequest.onupgradeneeded = function(event) { 
  const db = event.target.result;

  let cocktailStore = db.createObjectStore("Cocktails", { keyPath : 'idDrink' });
};
```

The `open()` method takes two parameters. The first is the name of the database. The second is the version of the database, which is optional and will default to 1 if the database does not already exist (otherwise it will default to the existing version number). It is important to note that the version must be an integer, so using a version like 1.2 is the same as using 1.

If the database does not exist or is greater than the existing version, it will trigger the `dbRequest.onupgradeneeded` event. This is where you will create your object stores or perform any necessary updates to existing data. You would also include creating any necessary indexes here.

The `onsuccess` method will trigger once the connection has been opened and any upgrade completed, if necessary.

> I am not covering a lot of items here, including indexes, which will be important in most use cases where you'd need to find or update records based upon properties other than an id. There are a lot of good resources that dive much deeper into IndexedDB. Start with MDN's guide to [using IndexedDB](https://developer.mozilla.org/en-US/docs/Web/API/IndexedDB_API/Using_IndexedDB) or Google's [Working with IndexedDB](https://developers.google.com/web/ilt/pwa/working-with-indexeddb) guide.

### Inserting Data

Now that we've created the database and opened the connection, it's time to populate it.

```javascript
let cocktailsStore = db.transaction(["Cocktails"], "readwrite").objectStore("Cocktails");
data.drinks.forEach(item => {
  cocktailsStore.put(item);
});
```

As noted previously, every interaction with the data must occur within the context of a transaction. The `transaction()` method takes two parameters. The first is an array of object store names that will be used within the scope of the transaction and the second is the type of access, which can be `readonly` or `readwrite`.

Since we are going to be inserting data, we'll need the `readwrite` mode. I then open a connection to the `Cocktails` object store. This is performed on a single line but can be separated to keep a variable reference to both the returned transaction object and the object store object. Finally, I use the `put()` method on the object store to insert the object into the data store. If I were updating a record, `put()` still works.

### Retrieving Data

Now that our object store has been populated, let's get the data back out of it.

```javascript
let cocktailsStore = db.transaction(["Cocktails"], "readonly").objectStore("Cocktails");
let getCocktailData = cocktailsStore.getAll();
getCocktailData.onsuccess = function(event) {
	if (event.target.result.length === 0) {
	  // load the remote data
	}
	else {
	  // display the local data
	}
}
```

The example gets all the records out of the object store. You still need to work within a transaction, but, in this case, we only need to read the data. The `getAll()` method gets all the records, which we can iterate through to display.

If you need to get only a single record, use the `get()` method and supply the key. To get based upon an index rather than the key, you would retrieve a reference to that index from the returned object store (i.e. `cocktaildb` in the code above) using `index()` and then use `getAll()` or `get()` on that index.

### Full Example

Here's the complete example to see it in action. I added some additional details to clear out local data and make it more obvious where the data is being displayed from.

<p class="codepen" data-height="265" data-theme-id="0" data-default-tab="js,result" data-user="remotesynth-the-bold" data-slug-hash="RXyBeJ" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="IndexedDb Example">
  <span>See the Pen <a href="https://codepen.io/remotesynth-the-bold/pen/RXyBeJ/">
  IndexedDb Example</a> by Brian Rinaldi (<a href="https://codepen.io/remotesynth-the-bold">@remotesynth-the-bold</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

## Where to Go From Here

This only scratches the surface of IndexedDB - again, check out MDN's [using IndexedDB](https://developer.mozilla.org/en-US/docs/Web/API/IndexedDB_API/Using_IndexedDB) or Google's [Working with IndexedDB](https://developers.google.com/web/ilt/pwa/working-with-indexeddb) guide as you are ready to dive deeper. If you are caching data for offline or performance purposes, you'll also need to come up with a strategy to synchronize your local data with the remote data. In some cases, you may want to  always do this as soon as the user is back online, but in others where the data may not change constantly or be changed by the user, you may want to set up a means to refresh only periodically. All of that depends on the nature of the application you are building.

As I said before, IndexedDB is not the simplest thing in the world. However, there are some really nice tools that can make working with it much simpler. In the next part of this series, we'll look at some of those.