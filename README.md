# Shopping List

**Note:** This is a work in progress.

Shopping List is an Offline First demo Progressive Web App built using Polymer and PouchDB. Mult-user / multi-device capabilities are enabled by Hoodie. [This app is part of a series of Offline First demo apps, each built using a different stack.](https://github.com/ibm-watson-data-lab/shopping-list)

## Quick Start

### Prerequisites

First, install [Polymer CLI](https://github.com/Polymer/polymer-cli) using [npm](https://www.npmjs.com/) (we assume you have pre-installed [Node.js](https://nodejs.org/)):

    npm install --global polymer-cli

Second, install [Bower](https://bower.io/) using [npm](https://www.npmjs.com):

    npm install --global bower

Third, install the [Bower npm resolver](https://github.com/mjeanroy/bower-npm-resolver):

    npm install --global bower-npm-resolver

### Running the Development Server

This command serves the app at `http://127.0.0.1:8081` and provides basic URL routing for the app:

    polymer serve

### Building

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

### Previewing the Build

This command serves your app. Replace `build-folder-name` with the folder name of the build you want to serve:

    polymer serve build/build-folder-name/

### Running the Tests

This command will run [Web Component Tester](https://github.com/Polymer/web-component-tester) against the browsers currently installed on your machine:

    polymer test

If running Windows you will need to set the following environment variables:

- LAUNCHPAD_BROWSERS
- LAUNCHPAD_CHROME

Read More here [daffl/launchpad](https://github.com/daffl/launchpad#environment-variables-impacting-local-browsers-detection)

### Adding a New View

You can extend the app by adding more views that will be demand-loaded e.g. based on the route, or to progressively render non-critical sections of the application. Each new demand-loaded fragment should be added to the list of `fragments` in the included `polymer.json` file. This will ensure those components and their dependencies are added to the list of pre-cached components and will be included in the build.

### Deploying to GitHub Pages

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

## Features

Shopping List is a simple demo app, with a limited feature set. Here is a list of features written as user stories grouped by Epic:

* Planning
  * As a \<person planning to shop for groceries\>, I want to \<create a shopping list\> so that \<I can add items to this shopping list\>.
  * As a \<person planning to shop for groceries\>, I want to \<add an item to my shopping list\> so that \<I can remember to buy that item when I am at the grocery store later\>.
  * As a \<person planning to shop for groceries\>, I want to \<remove an item from my shopping list\> so that \<I can change my mind on what to buy when I am at the grocery store later\>.
* Shopping
  * As a \<person shopping for groceries\>, I want to \<view items on my shopping list\> so that \<I can remember what items to buy\>.
  * As a \<person shopping for groceries\>, I want to \<add an item to my shopping list\> so that \<I can remember to buy that item\>.
  * As a \<person shopping for groceries\>, I want to \<remove an item from my shopping list\> so that \<I can change my mind on what to buy\>.
  * As a \<person shopping for groceries\>, I want to \<check off an item on my shopping list\> so that \<I can keep track of what items I have bought\>.
* Offline First
  * As a \<person shopping for groceries\>, I want to \<have the app installed on my device\> so that \<I can continue to utilize my shopping list when no internet connection is available\>.
  * As a \<person shopping for groceries\>, I want to \<have my shopping list stored locally on my device\> so that \<I can continue to utilize my shopping list when no internet connection is available\>.
  * As a \<person shopping for groceries\>, I want to \<sync my shopping list with the cloud\> so that \<I can manage and utilize my shopping list on multiple devices\>.
* Multi-User / Multi-Device
  * As a \<new user\>, I want to \<sign up for the app\> so that \<I can use the app\>.
  * As an \<existing user\>, I want to \<sign in to the app\> so that \<I can use the app\>.
  * As an \<existing user\>, I want to \<sign out of the app\> so that \<I can protect my privacy\>.
* Geolocation
  * As a \<person planning to shop for groceries\>, I want to \<associate a shopping list with a grocery store\> so that \<I can be notified of this shopping list when I am physically at that grocery store\>.
  * As a \<person associating a shopping list with a physical store\>, I want to \<access previously-used locations\> so that \<I can quickly find the physical store for which I am searching\>.
  * As a \<person shopping for groceries\>, I want to \<be notified of a shopping list when I am physically at the grocery store associated with that shopping list\> so that \<I can quickly find the shopping list for my current context\>.

## App Architecture

This app uses a drawer-based layout. The layout is provided by Polymer's `app-layout` elements.

This app, along with the `polymer-cli` toolchain, uses the "PRPL pattern" This pattern allows fast first delivery and interaction with the content at the initial route requested by the user, along with fast subsequent navigation by pre-caching the remaining components required by the app and progressively loading them on-demand as the user navigates through the app.

The PRPL pattern, in a nutshell:

* **Push** components required for the initial route
* **Render** initial route ASAP
* **Pre-cache** components for remaining routes
* **Lazy-load** and progressively upgrade next routes on-demand

## Live Demo

TBD

## Tutorial

Shopping List is an Offline First demo Progressive Web App built using Polymer and PouchDB. Mult-user / multi-device capabilities are enabled by Hoodie. [This app is part of a series of Offline First demo apps, each built using a different stack.](https://github.com/ibm-watson-data-lab/shopping-list) This app is a built using the [Polymer App Toolbox and the Polymer CLI](https://www.polymer-project.org/2.0/start/toolbox/set-up). This tutorial will walk you through the steps necessary to transform the [Starter Kit](https://github.com/PolymerElements/polymer-starter-kit) (generated by the Polymer CLI) into an Offline First Shopping List Progressive Web App that uses [PouchDB](https://pouchdb.com/) (an open source JavaScript database that syncs) and [Hoodie](http://hood.ie/) (an open source backend framework for Offline First applications). If you simply want to try out a completed version of the Shopping List app then read the [Quick Start](#quick-start) section of this README. If you want to jump to the end of the tutorial and view the completed code, then check out the [`tutorial` branch](https://github.com/ibm-watson-data-lab/shopping-list-polymer-pouchdb/tree/tutorial) of this project (note that the `tutorial` branch contains a simplified version of the reference app with a clean commit history and is different than what you will find in the `master` branch).

### Table of Contents

* Prerequisite Knowledge & Skills
* Key Concepts
* Tutorial Outline
* Tutorial Steps
* Initial Set Up
* Creating the Polymer App
* Adding a PouchDB Database
* Syncing Data
  * Configure a Database
     * Option 1: Apache CouchDB
     * Option 2: IBM Cloudant
     * Option 3: Cloudant Developer Edition
  * Configure Remote Database Credentials
  * Trigger Database Replication
* Adding Multi-User / Multi-Device Features with Hoodie
  * Installing Hoodie
  * Configuring Hoodie
  * Using the Hoodie Store API
  * Using Hoodie Account API
  * Testing Offline Sync
* Adding Gelocation Features
* What's next?
  * Other Features
  * Get Involved in the Offline First Community!
  * Further Reading and Resources

### Prerequisite Knowledge & Skills

* Ability to write JavaScript at a novice level, at minimum.
* A basic understanding of [JavaScript promises](https://pouchdb.com/2015/05/18/we-have-a-problem-with-promises.html).
* A basic understanding of HTML.
* Ability to work with an application programming interface (API).

### Key Concepts

* **Progressive Web Apps:** A Progressive Web App provides both the discoverability of a web app and the *reliable, fast, and engaging user experience* of a native mobile app. See [Pokedex.org](https://www.pokedex.org/) for a fun example of a Progressive Web App and check out [PWA Stats](https://www.pwastats.com/) for a community-driven list of stats and news related to Progressive Web Apps.
* **[Polymer](https://www.polymer-project.org/):** Libraries, tools, and patterns for *building Progressive Web Apps using web platform features* such as Web Components, Service Workers, and HTTP/2.
* **[Web Components](https://www.webcomponents.org/):** Open standard for components and widgets that are *customizable, reusable, and encapsulated*
* **[Polymer App Toolbox](https://www.polymer-project.org/2.0/toolbox/):** Components, tools, and templates for *building Progressive Web Apps with Polymer and Web Components*.
* **[Polymer App Toolbox - Starter Kit](https://github.com/PolymerElements/polymer-starter-kit):** A starter kit for building Polymer apps.
* **Offline First:** Progressive Web Apps must be Offline First in order to provide a reliable, fast, and engaging user experience *regardless of network connectivity*.
* **Service Workers:** Use the Cache API (part of the Service Workers specification) to make URL addressable *resources and content* available while offline.
* **IndexedDB:** Use IndexedDB or localForage (a polyfill that uses WebSQL or localStorage if IndexedDB is not supported) to make *application data* available while offline.
* **[PouchDB](https://pouchdb.com/):** An open source *JavaScript database that syncs* with anything that implements the CouchDB Replication Protocol.
* **[Apache CouchDB](http://couchdb.apache.org/):** An open source document database featuring an HTTP API, JSON documents, clustering capabilities for horizontal scalability, and *peer-to-peer replication*.
* **[IBM Cloudant](https://cloudant.com/):** A fully-managed database-as-a-service (DBaaS) *based on Apache CouchDB* with additional full text and geospatial search capabilities
* **[Hoodie](http://hood.ie/):** An open source *backend framework for Offline First applications*, leveraging Apache CouchDB on the server and PouchDB on the client

### Tutorial Outline

TBD

### Tutorial Steps

A step-by-step walkthrough of the tutorial:

1. Initialize the app using the Polymer App Toolbox - Starter Kit
2. Update the app title, description, and related metadata
3. Remove views from the Starter Kit that we will not be using
4. Create a stub of the shopping lists component
5. Create a stub of the shopping list items component
6. Install the shopping list domain model
7. Create a component to encapsulate the shopping list domain model
8. Use the shopping list domain model for one-way data binding of shopping lists
9. Create an empty state indicator for shopping lists
10. Add stub data to the shopping lists component
11. Add a loading spinner to the shopping lists component
12. Install PouchDB and pouchdb-find
13. Create a component to encapsulate PouchDB with pouchdb-find
14. Create a shared database property within the app component
15. Use the shopping list repository to find a list of shopping lists
16. Use PouchDB to listen for and propagate changes to shopping lists
17. Create a dialog with a form for creating a new shopping list
18. Create a new shopping list when the create new shopping list form is submitted
19. Use the shopping list domain model for one-way data binding of shopping list items
20. Create an empty state indicator for shopping list items
21. Add stub data to the shopping list items component
22. Add a loading spinner to the shopping list items component
23. Observe route changes in shopping list items component
24. Use the shopping list repository to find a list of shopping list items
25. Use PouchDB to listen for and propagate changes to shopping list items
26. Create a dialog with a form for creating a new shopping list item
27. Create a new shopping list item when the create new shopping list item form is submitted
28. Update database when a list item is checked or unchecked
29. Enable live replication with a remote database

### Initial Set Up

#### Prerequisites

In a terminal, check for Node.js version 6 or higher:

```
$ node -v
v8.6.0
```

**Note:** The `$` in the above instruction (and in all subsequent examples) indicates the start of a command prompt in a terminal. Do _not_ type the leading `$` into your command prompt. Multiple lines beginning with a `$` in subsequent instructions indicate the start of a new command (i.e. hit "enter" after the previous command and then type the new command). Subsequent lines _not_ beginning with a `$` in examples like the one above indicate output from the previous command. You should _not_ type these lines.

Install Node.js if it is not already installed (or upgrade Node.js if you have a version earlier than 6):

* [Download Node.js](https://nodejs.org/en/download/) or
* [Install Node.js via a package manager](https://nodejs.org/en/download/package-manager/)

Install Bower:

```
$ npm install -g bower
```

**Note:** If the above command results in an `EACCES` error then read the documentation on [fixing npm permissions](https://docs.npmjs.com/getting-started/fixing-npm-permissions).

Install Polymer CLI:

```
$ npm install -g polymer-cli
```

### Initialize the app using the Polymer App Toolbox - Starter Kit

[[diff](https://github.com/ibm-watson-data-lab/shopping-list-polymer-pouchdb/commit/8d28ee041c027943163ea99a709aa223ceb2c700)]

Create a new directory for your project:

```
$ mkdir shopping-list-polymer-pouchdb
```

Change into your new directory:

```
$ cd shopping-list-polymer-pouchdb
```

Run the following command for initializing a new Polymer project using the `polymer-2-starter-kit` template:

```
$ polymer init polymer-2-starter-kit
info:    Running template polymer-init-polymer-2-starter-kit:app...
info:    Finding latest ^3.0.0 release of PolymerElements/polymer-starter-kit
info:    Downloading v3.1.0 of PolymerElements/polymer-starter-kit
info:    Unpacking template files
info:    Finished writing template files


I'm all done. Running bower install for you to install the required dependencies. If this fails, try running the command yourself.
```

**Note:** As mentioned previously, subsequent lines _not_ beginning with a `$` in examples like the one above indicate output from the previous command. You should _not_ type these lines.

You will see a bunch of additional output as the Polymer CLI installs Bower dependencies.

**Note:** Polymer 2.0 uses Bower to manage frontend dependencies even though Bower is deprecated. [Polymer 3.0 is moving from Bower to npm.](https://www.polymer-project.org/blog/2017-08-22-npm-modules)

Start the Polymer Development server:

```
$ polymer serve
info:    Files in this directory are available under the following URLs
      applications: http://127.0.0.1:8081
      reusable components: http://127.0.0.1:8081/components/polymer-starter-kit/
```

You should now be able to browse to `http://127.0.0.1:8081` in your web browser and see the Starter Kit app. The Starter Kit app:

* Uses a [responsive, drawer-based app layout](https://www.polymer-project.org/2.0/toolbox/app-layout)
* Uses [modular, client-side routing](https://www.polymer-project.org/2.0/toolbox/routing)
* Uses a [Service Worker to cache content and assets for offline access](https://www.polymer-project.org/2.0/toolbox/service-worker)

Close the browser tab containing the Starter Kit app. Back in your terminal, use `Ctrl-C` to cancel the `polymer serve` command and return you to the command prompt.

## Workshop

TBD

## Developer Journey

TBD
