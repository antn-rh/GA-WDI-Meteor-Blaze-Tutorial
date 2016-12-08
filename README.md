<img src="https://d14xs1qewsqjcd.cloudfront.net/assets/og-image-logo.png" width="300">

# INTRO TO METEOR/BLAZE

| LEARNING OBJECTIVES |
|---|
| Introduction to Meteor/Blaze |
| Installing Meteor |
| Minimongo |
| Subscriptions and Publications |
| Hot Code Push |
| Todo App Walkthrough |

## Introduction to Meteor/Blaze

"Meteor is a full-stack JavaScript platform for developing modern web and mobile applications. Meteor includes a key set of technologies for building connected-client reactive applications, a build tool, and a curated set of packages from the Node.js and general JavaScript community." - (http://docs.meteor.com/#/full/)

Blaze is the default frontend framework that comes with Meteor. It is a Meteor-only package, and may be replaced with AngularJS or ReactJS.

- Meteor (or MeteorJS) is a JavaScript framework that is great for Rapid Application Development (RAD).

- It is built on top of Node.js (meaning that meteor uses node features such as package.json, node_modules, npm install, etc. 	

- Created by Meteor Development Group and initially released in 2012.

- It was designed to be easy to learn and use. One of Meteor's principles is "simplicity equals productivity".

- Why Meteor? (https://www.quora.com/Should-I-use-Meteor-Why)

## Installing Meteor

- Current version of Meteor: 1.4 (https://www.meteor.com/install)

	- OSX/Linux users can install from terminal:
	<br>
	`curl https://install.meteor.com/ | sh`

	- Windows users should click on link above for install button


## Minimongo

`minimongo` is reimplementation of (almost) the entire MongoDB API, against an in-memory JavaScript database. It is like a MongoDB emulator that runs inside your web browser. You can insert data into it and search, sort, and update that data.

Minimongo implements the following features, mirroring the MongoDB features:
* Selectors
* Modifiers
* Fields projections
* Querying with sort and limit
* ObjectID generation
* Geo-positional operator $near with GeoJSON parsing
Internally, all documents are mapped in a single JS object from `_id` to the document.

## Hot Code Push

- When you make a change in the database, that change propagates through a persistent client-server connection and triggers an automatic update of the user interface, with no “glue” code necessary.

- Blaze is the top of that stack — the front-end rendering engine that lets you define what your page should look like via HTML-like templates and then hook up data from Minimongo, Meteor’s front-end data store.

## Publications

In a traditional, HTTP-based web application, the client and server communicate in a “request-response” fashion. Typically the client makes RESTful HTTP requests to the server and receives HTML or JSON data in response, and there’s no way for the server to “push” data to the client when changes happen at the backend.

Meteor is built from the ground up on the Distributed Data Protocol (DDP) to allow data transfer in both directions. Building a Meteor app doesn’t require you to set up REST endpoints to serialize and send data. Instead you create publication endpoints that can push data from server to client.

## Subscriptions

We need a way for clients to specify which subset of that data they need, and that’s exactly where subscriptions come in.
Any data you subscribe to will be mirrored on the client thanks to Minimongo, Meteor’s client-side implementation of MongoDB.

You can think of a subscription as a pipe that connects a subset of the “real” collection with the client’s version, and constantly keeps it up to date with the latest information on the server.

	```
	// on the server
	Meteor.publish('posts', function(author) {
	  return Posts.find({flagged: false, author: author});
	});

	// on the client
	Meteor.subscribe('posts', 'bob-smith');
	```

## Todo App Walkthrough

#### Getting Started

- This tutorial can be found on Meteor.com: (https://www.meteor.com/tutorials/blaze/creating-an-app)

#### Head, Body, Template

- Meteor breaks down HTML into three main components: head, body, and templates.

- In the example code, you will notice that there is no HTML boilerplate, no script tags, and no link tags. This is how Meteor is designed (a .meteor folder is generated when creating a Meteor app—it contains the code that allows this to be possible).

- Meteor uses templates to modularize code. An example is in task.html:

	```html
	<template name="task">
		<li class="{{#if checked}}checked{{/if}}">
			<button class="delete">&times;</button>

			<input type="checkbox" checked="{{checked}}" class="toggle-checked" />

			<span class="text">{{text}}</span>
		</li>
	</template>
	```
- This template contains a class of task that is called in body.html:

	```html
	<div class="active">
		<ul>
			<h3 class="active-header">Active Todos</h3>
			{{#each tasks}}
			{{#unless checked}}
			{{> task}}
			{{/unless}}
			{{/each}}
		</ul>
	</div>
	```
- The `>` is used to defined a template the is being called.
- Templates are referenced in JavaScript like:

	```js
	import { Template } from 'meteor/templating';

	import { Tasks } from '../api/tasks.js';

	import './task.html';

	Template.task.events({
	  'click .toggle-checked'() {
	    // Set the checked property to the opposite of its current value
	    Tasks.update(this._id, {
	      $set: { checked: !this.checked },
	    });
	  },
	  'click .delete'() {
	    Tasks.remove(this._id);
	  },
	});
	```

#### Meteor Spacebars

- Spacebars are similar to AngularJS's curly brackets, but with its own unique syntax:

	```html
	<ul>
		<h3 class="active-header">Active Todos</h3>
		{{#each tasks}}
		{{#unless checked}}
		{{> task}}
		{{/unless}}
		{{/each}}
	</ul>
	```
