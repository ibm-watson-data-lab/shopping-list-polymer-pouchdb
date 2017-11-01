![Bluemix Deployments](https://metrics-tracker.mybluemix.net/stats/5c5df69e10058d49cdc1f4d2fc63ce31/badge.svg)

# Create an Offline First Shopping List with Polymer and PouchDB

In this code pattern, we will create an Offline First shopping list. Shopping List is an Offline First demo Progressive Web App built using Polymer and PouchDB. [This app is part of a series of Offline First demo apps, each built using a different stack.](https://github.com/ibm-watson-data-lab/shopping-list) Credit goes to [Bradley Holt](https://github.com/bradley-holt) for this Polymer/PouchDB implementation.

When the reader has followed this code pattern, they will understand how to:

* Implement an app database that runs in the browser with local data when offline, and syncs with a remote database when online.
* Create an Offline First Progressive Web App.

![](doc/source/images/architecture.png)

## Flow

1. The user manages shopping lists using the Offline First web app.
2. Polymer is used to make it a Progressive Web App with Web Components and Service Workers.
3. The shopping lists are stored locally in PouchDB while offline.
4. When online, PouchDB syncs with Cloudant.

## With Watson
Want to take your Watson app to the next level? Looking to leverage Watson Brand assets? Join the [With Watson](https://www.ibm.com/watson/with-watson) program which provides exclusive brand, marketing, and tech resources to amplify and accelerate your Watson embedded commercial solution.

## Included components
* [Cloudant NoSQL DB](https://console.ng.bluemix.net/catalog/services/cloudant-nosql-db): A fully managed data layer designed for modern web and mobile applications that leverages a flexible JSON schema.

## Featured technologies
* [Polymer](https://www.polymer-project.org/): Libraries, tools, and patterns for building Progressive Web Apps using web platform features such as Web Components, Service Workers, and HTTP/2.
* [PouchDB](https://pouchdb.com/): An open source JavaScript database that syncs with anything that implements the CouchDB Replication Protocol.
* [Databases](https://en.wikipedia.org/wiki/IBM_Information_Management_System#.22Full_Function.22_databases): Repository for storing and managing collections of data.

<!--Update this section when the video is created
# Watch the Video
[![](http://img.youtube.com/vi/Jxi7U7VOMYg/0.jpg)](https://www.youtube.com/watch?v=Jxi7U7VOMYg)
-->

# Steps
* [Deploy to Bluemix](#deploy-to-bluemix) **OR** [Run locally](#run-locally)
* [Database and replication setup](#database-and-replication-setup)

## Deploy to Bluemix
[![Deploy to Bluemix](https://metrics-tracker.mybluemix.net/stats/5c5df69e10058d49cdc1f4d2fc63ce31/button.svg)](https://bluemix.net/deploy?repository=https://github.com/ibm-watson-data-lab/shopping-list-polymer-pouchdb)

1. Press the above ``Deploy to Bluemix`` button and then click on ``Deploy``.

1. In Toolchains, click on Delivery Pipeline to watch while the app is deployed. Once deployed, the app can be viewed by clicking `View app`.

1. To see the app and services created and configured for this code pattern, use the Bluemix dashboard. The app is named `shopping-list-polymer-pouchdb` with a unique suffix. The following services are created and easily identified by the `slpp-` prefix:
    * slpp-CloudantNoSQLDB

## Run locally
> NOTE: These steps are only needed when running locally instead of using the ``Deploy to Bluemix`` button.

1. [Clone the repo](#1-clone-the-repo)
1. [Install the prerequisites](#2-install-the-prerequisites)
1. [Run the server](#3-run-the-server)
1. [Create a Cloudant or CouchDB service](#4-create-a-cloudant-or-couchdb-service)

### 1. Clone the repo

Clone the `shopping-list-polymer-pouchdb` locally. In a terminal, run:

```
$ git clone https://github.com/ibm-watson-data-lab/shopping-list-polymer-pouchdb
```

### 2. Install the prerequisites

First, install [Polymer CLI](https://github.com/Polymer/polymer-cli) using [npm](https://www.npmjs.com/) (we assume you have pre-installed [Node.js](https://nodejs.org/)):

    npm install --global polymer-cli

Second, install [Bower](https://bower.io/) using [npm](https://www.npmjs.com):

    npm install --global bower

Third, install the [Bower npm resolver](https://github.com/mjeanroy/bower-npm-resolver):

    npm install --global bower-npm-resolver

### 3. Run the server

This command serves the app at `http://127.0.0.1:8081` and provides basic URL routing for the app:

    polymer serve

### 4. Create a Cloudant or CouchDB service

PouchDB can synchronize with CouchDB and compatible servers. To run and test locally, you can install CouchDB. Alternatively, you can use a Bluemix Cloudant NoSQL DB service for your remote DB.

#### Installing Apache CouchDB

[Install CouchDB 2.1](http://docs.couchdb.org/en/2.1.0/install/index.html). Instructions are available for installing CouchDB 2.1 on Unix-like systems, on Windows, on Mac OS X, on FreeBSD, and via other methods.

Configure CouchDB for a [single-node setup](http://docs.couchdb.org/en/2.1.0/install/setup.html#single-node-setup), as opposed to a cluster setup. Once you have finished setting up CouchDB, you should be able to access CouchDB at `http://127.0.0.1:5984/`. Ensure that CouchDB is running and take note of your admin username and password.

#### Creating a Bluemix Cloudant NoSQL DB service

Sign up for an [IBM Bluemix](https://console.ng.bluemix.net/) account, if you do not already have one.

Once you are logged in to Bluemix, create a new Cloudant instance on the [Cloudant NoSQL DB Bluemix Catalog](https://console.ng.bluemix.net/catalog/services/cloudant-nosql-db) page. This should take you to a page representing the newly-created service instance. Click the "Service credentials" link. You should have one set of service credentials listed. Click "View credentials" which should show you a JSON object containing your service credentials. Copy the value for the `url` key to your clipboard (the value will be in the form of `https://username:password@uniqueid-bluemix.cloudant.com`).

## Database and replication setup
1. [Create the remote database](#1-create-the-remote-database)
1. [Enable CORS](#2-enable-cors)
1. [Set the replication target](#3-set-the-replication-target)

### 1. Create the remote database

Use your Cloudant or CouchDB dashboard to create a database. Select the Databases icon on the left and then use the `Create Database` button to create the "shopping-list" database.
The Shopping List app can be used locally before the database exists, but cannot sync
until the remote database is completed.

![](doc/source/images/create_db.png)

### 2. Enable CORS

Cross-Origin Resource Sharing (CORS) needs to be enabled. Use your Cloudant or CouchDB dashboard to enable it. The CORS options are under the account settings or config depending on your version. Enable CORS and restrict the domain as needed for security.

![](doc/source/images/enable_cors.png)

### 3. Set the replication target

Run the Shopping List app and use the `Replicator` form to enter your Database URL.
If you use the Bluemix Cloudant URL taken from the service credentials as described above, the URL includes user and password GUIDs.

Add `/shopping-list` to the URL to connect to the database that you created.

![](doc/source/images/replicator.png)

# Using the app

The app allows you to create a shopping list by clicking on the plus sign. Click on the list to see its items. Then, you can add items to the list by clicking the plus sign. There is a checkbox to allow you to mark the items complete as you buy load up your cart.

When you have not configured your Replication Target or when you are offline, the lists will not sync. One good way to test this is to run two browsers. You can use Chrome and Firefox and have different lists in each.

When you go online and have the database and CORS enabled and the Replication Target is set, the shopping lists will sync. You will then be able to use both lists from either browser.

![](doc/source/images/shopping_lists.png)

## Features as epics

Shopping List is a simple demo app, with a limited feature set. [Here](https://github.com/ibm-watson-data-lab/shopping-list#features) is a list of features written as user stories grouped by Epic.

Not all features are implemented in the current Polymer app. This demo app does not yet include item/list removal, geolocation features or multi-user features.

## Building for production

The `polymer build` command builds your Polymer application for production, using build configuration options provided by the command line or in your project's `polymer.json` file.  

You can configure your `polymer.json` file to create multiple builds. This is necessary if you will be serving different builds optimized for different browsers. You can define your own named builds, or use presets. See the documentation on [building your project for production](https://www.polymer-project.org/2.0/toolbox/build-for-production) for more information.

This app is configured to create three builds using [the three supported presets](https://www.polymer-project.org/2.0/toolbox/build-for-production#build-presets):

```
"builds": [
  {
    "preset": "es5-bundled"
  },
  {
    "preset": "es6-bundled"
  },
  {
    "preset": "es6-unbundled"
  }
]
```

Builds will be output to a subdirectory under the `build/` directory as follows:

```
build/
  es5-bundled/
  es6-bundled/
  es6-unbundled/
```

* `es5-bundled` is a bundled, minified build with a service worker. ES6 code is compiled to ES5 for compatibility with older browsers.
* `es6-bundled` is a bundled, minified build with a service worker. ES6 code is served as-is. This build is for browsers that can handle ES6 code - see [building your project for production](https://www.polymer-project.org/2.0/toolbox/build-for-production#compiling) for a list.
* `es6-unbundled` is an unbundled, minified build with a service worker. ES6 code is served as-is. This build is for browsers that support HTTP/2 push.

Run `polymer help build` for the full list of available options and optimizations. Also, see the documentation on the [polymer.json specification](https://www.polymer-project.org/2.0/docs/tools/polymer-json) and [building your Polymer application for production](https://www.polymer-project.org/2.0/toolbox/build-for-production).

## Previewing the build

This command serves your app. Replace `build-folder-name` with the folder name of the build you want to serve:

    polymer serve build/build-folder-name/

## Running the tests

This command will run [Web Component Tester](https://github.com/Polymer/web-component-tester) against the browsers currently installed on your machine:

    polymer test

If running Windows you will need to set the following environment variables:

- LAUNCHPAD_BROWSERS
- LAUNCHPAD_CHROME

Read More here [daffl/launchpad](https://github.com/daffl/launchpad#environment-variables-impacting-local-browsers-detection)

## Adding a new view

You can extend the app by adding more views that will be demand-loaded e.g. based on the route, or to progressively render non-critical sections of the application. Each new demand-loaded fragment should be added to the list of `fragments` in the included `polymer.json` file. This will ensure those components and their dependencies are added to the list of pre-cached components and will be included in the build.

## Deploying to GitHub Pages

If you are deploying to a [Project Page](https://help.github.com/articles/user-organization-and-project-pages/#project-pages) then you will first need to modify the base URL and root path values in `index.html` to match your project name. For example, for the project name `shopping-list-polymer-pouchdb` change:

    <base href="/">

To:

    <base href="/shopping-list-polymer-pouchdb/">

And change:

    window.Polymer = {rootPath: '/'};

To:

    window.Polymer = {rootPath: '/shopping-list-polymer-pouchdb/'};

You can then deploy the app to GitHub pages by running:

    npm run deploy:gh-pages

# App architecture

This app uses a drawer-based layout. The layout is provided by Polymer's `app-layout` elements.

This app, along with the `polymer-cli` toolchain, uses the "PRPL pattern" This pattern allows fast first delivery and interaction with the content at the initial route requested by the user, along with fast subsequent navigation by pre-caching the remaining components required by the app and progressively loading them on-demand as the user navigates through the app.

The PRPL pattern, in a nutshell:

* **Push** components required for the initial route
* **Render** initial route ASAP
* **Pre-cache** components for remaining routes
* **Lazy-load** and progressively upgrade next routes on-demand

# Live demo

https://ibm-watson-data-lab.github.io/shopping-list-polymer-pouchdb/

# Tutorial

Refer to the [tutorial](tutorial) for step-by-step instructions on how to build your own Offline First shopping list Progressive Web App with Polymer and PouchDB.

# Links
<!--Update this section when the video is created
* [Demo on Youtube](https://www.youtube.com/watch?v=placeholder)
-->
* [Offline First](https://www.ibm.com/analytics/us/en/technology/offline-first/): In a data-first world, your web and native apps need to deliver excellent user experiences, including during network disruptions. The Offline First approach to application development puts performance first and recognizes that network downtime is a fact of life.
* [Progressive Web Apps](https://developers.google.com/web/progressive-web-apps/): A Progressive Web App provides both the discoverability of a web app and the reliable, fast, and engaging user experience of a native mobile app. 
* [Web Components](https://www.webcomponents.org/): Open standard for components and widgets that are customizable, reusable, and encapsulated
* [Polymer App Toolbox](https://www.polymer-project.org/2.0/toolbox/): Components, tools, and templates for building Progressive Web Apps with Polymer and Web Components.
* [Polymer App Toolbox - Starter Kit](https://github.com/PolymerElements/polymer-starter-kit): A starter kit for building Polymer apps.

# License
[Apache 2.0](LICENSE)
