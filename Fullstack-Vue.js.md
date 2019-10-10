
Making the view data-driven


Driving the template with data will allow us to dynamically render the view based upon the data we give it.

Let's familiarize ourselves with the applications data model.


### The data model

An array of JavaScript objects where each represents a sample submission object.


### The Vue Instance

The Vue instance is the starting point of all Vue applications.

A Vue instance accepts an options object which can contain details of the instance such as its template, data, methods, etc.


Root level Vue instances allow us to reference the DOM with which the instance is to be mounted/attached to.


Let's see an example of this by setting up the Vue instance for our application.

Create the Vue instance using the Vue function:

> el - set up the Vue instance

```
new Vue({
	el: '#app'
});
```

We've just specified the HTML element with the id of app to be the mounting point of our Vue application, by using the el option and providing it a string value of #app. Anywhere within this element can Vue JavaScript code now be used.


The Vue instance can also return data that needs to be handled within the view. This data must be specified within a data object in the instance.

This is how we'll arrange the connection between the data in our seed.js file and teh template view.



Let's update the instance by specifying a new data object. In the object, we'll include a submissions key that will have the same value as the Seed.submissions array:

> data - specify a data object

```
new Vue({
	el: '#app',
	data: {
		submissions: Seed.submissions
	}
});
```

In the HTML template, we can new reference all submission data by accessing submissions.

The Vue object constructor is available on the global scope since we've included the <script /> tag, that loads Vue, in our index.html file.


## Data binding 


The simplest form of data binding in Vue is using the 'Mustache' syntax which is denoted by curly braces {{}}}.

Apply this syntax to bind all the text within our HTML (e.g. title, description, etc).

** The 'Mustache' syntax however cannot be used in HTML attributes like href, id, src etc. **

Vue provides the native **v-bind** attribute (this is known as a Vue directive) to bind HTML attributes.

We'll use this directive to update the src attributes in our template.


