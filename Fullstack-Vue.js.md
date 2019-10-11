
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


### List rendering

Next objective is to render all the submission objects to our view by displaying each submission object as a separate template block.

Render a list of submission objects, use Vue's native **v-for** directive.


> v-for directive 

items is a data collection
item is an alias for every element that is being iterated upon.

```
v-for = "item in items"
		  |         | 
		alias   data collection
```


#### key

specify a key attribute for every iterated element within a rendered v-for list.
Vue uses the key attribute to create unique bindings for each node's identity.


v-bind:key="submission.id"



#### Sorting

#### Computed properties

Computed properties are used to handle complex calculations of information that need to be displayed in the view.

Below the data property in our Vue instance, we'll introduce a computed property sortedSubmissions that returns a sorted array of submissions:


```
new Vue({
	el: '#app',
	data: {
		submissions: Seed.submissions
	},
	computed: {
		sortedSubmissions () {
			return this.submissions.sort((a, b)) => {
				return b.votes - a.votes
			}
		}
	}
})
```

## Event handling

The v-on directive is used to create event listeners within the DOM.

> in native JavaScript, attach an event listener 

```
const ele = document.getElementById('app');
ele.addEventListener('click', () => console.llog('clicked'))

```

> In Vue, use the v-on:click directive to implement a click handler


```
new Vue({
	el: '#app',
	data: {
		// ...
	},
	computed: {
		// ...
	},
	methods: {
		upvote (submissionId) {
			const submission = this.submissions.find (
				submission => submission.id === submissionId
			);
			submission.votes++;
		}
	}
})

```

### Reactive state

We need to note an important aspect of Vue here. With a library like Rect, the above method implementation is problematic since state is often treated as immutable. State within Vue, on the other hand, is reactive.


Reactive state is one of the key differences that makes Vue unique. State (i.e. data) management is often intuitive and easy to understand since modifying state often directly causes the view to update.

Vue has an unobtrusive system to how data is modified and teh view reacts.


Our computed property sortedSubmissions depends on this.submissions, so as the latter changes, so does the former.


## Class bindings

Let's add a conditional class that displays a special blue border around a submission when said submission reaches a certain number of votes.





