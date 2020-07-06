---
layout: post
title: Submitting Netlify Forms Using JavaScript
date: '2020-07-06'
description: Submit a Netlify form asynchronously using JavaScript without jQuery.
categories:
  - Jamstack
comments: true
---

[Netlify Forms](https://docs.netlify.com/forms/setup/) make it incredibly easy to handle form submissions. In many cases all you need to do is simply need to give your form a name, add `data-netlify="true"` to your `form` element and you're done. Netlify will detect the form on build and save any form submissions. You can view the data under the forms tab in your Netlify dashboard and even create triggers to do things like notify you via email of submissions. Easy.

If you're working with React, there's a [little bit of additional](https://www.netlify.com/blog/2017/07/20/how-to-integrate-netlifys-form-handling-in-a-react-app/) code required, but it's still fairly simple.

So, what if you are working in plain JavaScript? The docs provide a [jQuery-based example](https://docs.netlify.com/forms/setup/#submit-forms-via-ajax). In my case, the site I was working on did not include jQuery. I couldn't find good examples of doing this without jQuery, so I thought I'd share what worked for me.

## Netlify forms without jQuery

I was connecting a basic form that collects survey responses from users. First of all, I did add the `data-netlify="true"` to the form. This tells Netlify to automatically pick up on the form and added it (with the name `surveyResponses`) to my admin.

I did set up an `action` on my form as well, though this also wasn't entirely necessary. In my case, in this current iteration of the site I planned to redirect the person to a submission page after the response is taken. This allows me to determine where the form goes in the form code rather than hard code it into the submission handler. In theory, this would allow me to use this same code for other forms in the future.

As the [jQuery instructions note](https://docs.netlify.com/forms/setup/#submit-forms-via-ajax), Netlify forms submissions require you to serlialize the form data. jQuery provides a simple `serialize` function. To replace this, I used the `serialize` function [in this CodePen](https://codepen.io/influxweb/pen/ozoYqa):

```javascript
const serialize = function (form) {
	var field,
		l,
		s = [];

	if (typeof form == 'object' && form.nodeName == "FORM") {
		var len = form.elements.length;

		for (var i = 0; i < len; i++) {
			field = form.elements[i];
			if (field.name && !field.disabled && field.type != 'button' && field.type != 'file' && field.type != 'hidden' && field.type != 'reset' && field.type != 'submit') {
				if (field.type == 'select-multiple') {
					l = form.elements[i].options.length;

					for (var j = 0; j < l; j++) {
						if (field.options[j].selected) {
							s[s.length] = encodeURIComponent(field.name) + "=" + encodeURIComponent(field.options[j].value);
						}
					}
				}
				else if ((field.type != 'checkbox' && field.type != 'radio') || field.checked) {
					s[s.length] = encodeURIComponent(field.name) + "=" + encodeURIComponent(field.value);
				}
			}
		}
	}
	return s.join('&').replace(/%20/g, '+');
};
```
My project already leveraged [Axios](https://github.com/axios/axios) for asynchronous HTTTP requests, which I also use to submit the form post request. Here's the code:

```javascript
function formSubmit(e) {
	e.preventDefault();

	const theForm = e.currentTarget;
	const options = {
		headers: { "Content-Type": "application/x-www-form-urlencoded" }
	}
	const formData = "form-name="+ theForm.name + "&" + serialize(theForm);
	axios.post(
		"/",
		formData,
		options
	)
	.then(function (response) {
		window.location.assign(theForm.action);
	})
	.catch(function (error) {
		console.log(error);
	});
}

surveyForm.addEventListener('submit',formSubmit);
```

Some notes on what's going on here:

* The `Content-Type` options may not be necessary. I added this when struggling to get it to work, but it doesn't hurt.
* Even though my form had the `data-netlify` on it and the hidden `form-name` field was being added by Netlify, it was not being serialized for some reason. This is why I just manually add it to the formData being passed. If the `form-name` is not passed, you will get a 404 when trying to submit. With the `form-name` added, it doesn't seem to matter where you post this to. Thus, I post it to just the root.
* In this case, I just redirect to the `action` of the form. I plan to update this function should I need it for other forms in the future to give more flexibility about what happens after the submit. My survey is in a modal (thus why all this was necessary). In the future I may just allow you to define either an action or a function that is called in response to a successful request.
* Right now I am not yet handling the case of an error. You definitely should and I definitely will.