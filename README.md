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
* Creating the Shopping List Polymer App
  * Building the Basic Components
  * Adding the Shopping List Domain Model
  * Adding a PouchDB Database
  * Completing the App
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
* **[Material Design](https://material.io/guidelines/):** A visual language for building apps.
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

#### Initialize the app using the Polymer App Toolbox - Starter Kit

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

Start the Polymer development server:

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

### Creating the Shopping List Polymer App

#### Building the Basic Components

##### Update the app title, description, and related metadata

[[diff](https://github.com/ibm-watson-data-lab/shopping-list-polymer-pouchdb/commit/3989f05a757ae8d4c120a9ee4402c71fd2f680f4)]

Our first step in transforming this app from the Starter Kit into a Shopping List app is to update the app title, description, and related metadata. In `manifest.json` change:

```javascript
  "name": "My App",
  "short_name": "My App",
  "description": "My App description",
```

to:

```javascript
  "name": "Shopping List",
  "short_name": "Shopping List",
  "description": "Shopping List is an Offline First demo Progressive Web App built using Polymer and PouchDB.",
```

**Note:** When viewing and editing files, you will want to use a text editor such as [Sublime Text](https://www.sublimetext.com/) or [Atom](https://atom.io/).

The `manifest.json` file [provides basic metadata about your app to web browsers](https://developer.mozilla.org/en-US/Add-ons/WebExtensions/manifest.json).

--

In `index.html` change:

```html
    <title>My App</title>
    <meta name="description" content="My App description">
```

to:

```html
    <title>Shopping List</title>
    <meta name="description" content="Shopping List is an Offline First demo Progressive Web App built using Polymer and PouchDB.">
```

--

Also in `index.html` change:

```html
    <meta name="application-name" content="My App">
```

to:

```html
    <meta name="application-name" content="Shopping List">
```

--

Still in `index.html` change:

```html
    <meta name="apple-mobile-web-app-title" content="My App">
```

to:

```html
    <meta name="apple-mobile-web-app-title" content="Shopping List">
```

The `index.html` file serves as the [app entrypoint](https://www.polymer-project.org/2.0/toolbox/server#app-entrypoint), which is responsible for instantiating the app shell.

--

In `src/my-app.html` change:

```html
            <div main-title>My App</div>
```

to:

```html
            <div main-title>Shopping List</div>
```

**Note:** A forward slash (`/`) in a file reference indicates that the file or directory following the forward slash is within the preceding directory. For example, `src/my-app.html` means that the `my-app.html` file is within the `src` directory.

The `src/my-app.html` file serves as the [app shell](https://www.polymer-project.org/2.0/toolbox/server#app-shell), which is responsible for routing within your app and may also include the main navigation elements for your app.

##### Remove views from the Starter Kit that we will not be using

[[diff](https://github.com/ibm-watson-data-lab/shopping-list-polymer-pouchdb/commit/9c2803f204272e4e5ffea591848a365b77fac56d)]

The Starter Kit comes with three example views (`view1`, `view2`, and `view3`). We will delete these views (and a corresponding test) as we will not be using them:

```
$ rm src/my-view1.html
$ rm src/my-view2.html
$ rm src/my-view3.html
$ rm test/my-view1.html
```

**Note:** As mentioned previously, the four `$` instances above indicate four separate commands for you to type (but do _not_ type the `$` at the beginning of each line), hitting enter after typing each of the four separate commands.

--

Remove the following three lines from `polymer.json`:

```javascript
    "src/my-view1.html",
    "src/my-view2.html",
    "src/my-view3.html",
```

The `polymer.json` file [stores information about your project structure and your desired build configuration(s)](https://www.polymer-project.org/2.0/docs/tools/polymer-json). [The `fragments` property](https://www.polymer-project.org/2.0/docs/tools/polymer-json#fragments) (the property from which we are removing the references to the deleted views) is a way to specify components that may be lazy-loaded.

--

Remove the following three lines from `src/my-app.html`:

```html
<link rel="lazy-import" href="my-view1.html">
<link rel="lazy-import" href="my-view2.html">
<link rel="lazy-import" href="my-view3.html">
```

The above lines lazy-load the referenced components on demand.

--

Also in `src/my-app.html` remove the following three lines:

```html
          <a name="view1" href="[[rootPath]]view1">View One</a>
          <a name="view2" href="[[rootPath]]view2">View Two</a>
          <a name="view3" href="[[rootPath]]view3">View Three</a>
```

The above lines represent navigational links to the referenced routes.

--

Still in `src/my-app.html` remove the following three lines:

```html
          <my-view1 name="view1"></my-view1>
          <my-view2 name="view2"></my-view2>
          <my-view3 name="view3"></my-view3>
```

The above lines represent the pages for the referenced components.

--

Finally in `src/my-app.html` change:


```javascript
        // Deault to 'view1' in that case.
        this.page = page || 'view1';
```

to:

```javascript
        // Deault to 'view404' in that case.
        this.page = page || 'view404';
 ```

##### Create a stub of the shopping lists component

[[diff](https://github.com/ibm-watson-data-lab/shopping-list-polymer-pouchdb/commit/aeda633ad83a1604074dce04e5b7845c55bc788c)]

Install the [`paper-card`](https://www.webcomponents.org/element/PolymerElements/paper-card) element:

```
$ bower install --save PolymerElements/paper-card#^2.0.0
```

Install the [`paper-fab`](https://www.webcomponents.org/element/PolymerElements/paper-fab) element:

```
$ bower install --save PolymerElements/paper-fab#^2.0.0
```

Install the [`iron-icons`](https://www.webcomponents.org/element/PolymerElements/iron-icons) element:

```
$ bower install --save PolymerElements/iron-icons#^2.0.0
```

Create a new file named `my-lists.html` in the `src` directory (`src/my-lists.html`). This will be a new component called `MyLists`. Here is the content for this new file:


```html
<link rel="import" href="../bower_components/polymer/polymer-element.html">
<link rel="import" href="../bower_components/paper-card/paper-card.html">
<link rel="import" href="../bower_components/paper-fab/paper-fab.html">
<link rel="import" href="../bower_components/iron-icons/iron-icons.html">

<dom-module id="my-lists">
  <template>
    <style>
      :host {
        display: block;
        padding: 8px 8px;
      }

      paper-card {
        width: 100%;
      }

      paper-fab {
        position: fixed;
        right: 16px;
        bottom: 16px;
      }
    </style>

    <paper-card heading="Groceries">
    </paper-card>

    <paper-fab mini icon="add"></paper-fab>

  </template>
  <script>

    class MyLists extends Polymer.Element {

      static get is() { return "my-lists"; }

    }
    window.customElements.define(MyLists.is, MyLists);
  </script>
</dom-module>
```

This new `MyLists` component:

* Is a Polymer element
* Is a Web Component by extension
* Contains a `paper-card` ([Material Design card](https://material.io/guidelines/components/cards.html)) element representing a stubbed out shopping list titled "Groceries"
* Contains a `paper-fab` ([Material Design floating action button](https://material.io/guidelines/components/buttons-floating-action-button.html)) element that will be used later for adding a new shopping list

--

Add the following line to the `fragments` property of the `polymer.json` before the line containing `"src/my-view404.html"`:

```javascript
    "src/my-lists.html",
```
--

Add the following line to the `src/my-app.html` file before the line containing `<link rel="lazy-import" href="my-view404.html">` (this will allow for lazy loading of our new `MyLists` component):

```html
<link rel="lazy-import" href="my-lists.html">
```

--

Add the following line to the `src/my-app.html` file between the opening and closing `<iron-selector>` tags (this will add a link to our new `MyLists` component in the app's navigation):

```html
          <a name="index" href="[[rootPath]]lists">Lists</a>
```

--

Add the following line to the `src/my-app.html` file before the line containing `<my-view404 name="view404"></my-view404>` (this will add our new `MyLists` component to the app):

```html
          <my-lists name="lists"></my-lists>
```

--

Finally, let's change the default view from `view404` to `lists`. In the `src/my-app.html` file change:

```html
        // Deault to 'view404' in that case.
        this.page = page || 'view404';
```

to:

```html
        // Deault to 'lists' in that case.
        this.page = page || 'lists';
```

##### Create a stub of the shopping list items component

[[diff](https://github.com/ibm-watson-data-lab/shopping-list-polymer-pouchdb/commit/3fd8ea99b0e79aa4016dfc6acbdc8e71ff492d02)]

Install the [`paper-listbox`](https://www.webcomponents.org/element/PolymerElements/paper-listbox) element:

```
$ bower install --save PolymerElements/paper-listbox#^2.0.0
```

Install the [`paper-item`](https://www.webcomponents.org/element/PolymerElements/paper-item) element:

```
$ bower install --save PolymerElements/paper-item#^2.0.0
```

Install the [`paper-checkbox`](https://www.webcomponents.org/element/PolymerElements/paper-checkbox) element:

```
$ bower install --save PolymerElements/paper-checkbox#^2.0.0
```

Create a new file named `my-items.html` in the `src` directory (`src/my-items.html`). This will be a new component called `MyItems`. Here is the content for this new file:


```html
<link rel="import" href="../bower_components/polymer/polymer-element.html">
<link rel="import" href="../bower_components/paper-listbox/paper-listbox.html">
<link rel="import" href="../bower_components/paper-item/paper-item.html">
<link rel="import" href="../bower_components/paper-item/paper-item-body.html">
<link rel="import" href="../bower_components/paper-checkbox/paper-checkbox.html">
<link rel="import" href="../bower_components/paper-fab/paper-fab.html">
<link rel="import" href="../bower_components/iron-icons/iron-icons.html">

<dom-module id="my-items">
  <template>
    <style>
      :host {
        display: block;
      }

      paper-item[data-checked] {
        text-decoration: line-through;
        color: var(--paper-item-disabled-color, var(--disabled-text-color));
      }

      paper-fab {
        position: fixed;
        right: 16px;
        bottom: 16px;
      }
    </style>

    <paper-listbox>
      <paper-item data-checked>
        <paper-checkbox checked></paper-checkbox>
        <paper-item-body>
          <div>Mangos</div>
        </paper-item-body>
      </paper-item>
      <paper-item>
        <paper-checkbox ></paper-checkbox>
        <paper-item-body>
          <div>Oranges</div>
        </paper-item-body>
      </paper-item>
      <paper-item>
        <paper-checkbox></paper-checkbox>
        <paper-item-body>
          <div>Pears</div>
        </paper-item-body>
      </paper-item>
    </paper-listbox>

    <paper-fab mini icon="add"></paper-fab>

  </template>
  <script>
    class MyItems extends Polymer.Element {

      static get is() { return "my-items"; }

    }
    window.customElements.define(MyItems.is, MyItems);
  </script>
</dom-module>
```

This new `MyItems` component:

* Is a Polymer element
* Is a Web Component by extension
* Contains a `paper-listbox` element with `paper-item` elements ([Material Design lists](https://material.io/guidelines/components/lists.html)) representing stubbed out shopping list items, one of which is checked
* Contains a `paper-fab` ([Material Design floating action button](https://material.io/guidelines/components/buttons-floating-action-button.html)) element that will be used later for adding a new shopping list item

--

Add the following line to the `fragments` property of the `polymer.json` after the line containing `"src/my-lists.html",`:

```javascript
    "src/my-items.html",
```
--

Add the following line to the `src/my-app.html` file after the line containing `<link rel="lazy-import" href="my-lists.html">
` (this will allow for lazy loading of our new `MyItems` component):

```html
<link rel="lazy-import" href="my-items.html">
```

--

Add the following line to the `src/my-app.html` file after the line containing `<my-lists name="lists"></my-lists>` (this will add our new `MyItems` component to the app while binding its route to the app's subroute):

```html
          <my-items name="items" route="{{subroute}}"></my-items>
```

--

Now let's take a look at our work so far! Start the Polymer development server:

```
$ polymer serve
info:    Files in this directory are available under the following URLs
      applications: http://127.0.0.1:8081
      reusable components: http://127.0.0.1:8081/components/polymer-starter-kit/
```

You should now be able to browse to `http://127.0.0.1:8081` in your web browser and see the Shopping List app with a stubbed out shopping list and shopping list items (you will need to manual navigate to the `/items` route for now to preview this page). When you're done, close the browser tab containing the Shopping List app. Back in your terminal, use `Ctrl-C` to cancel the `polymer serve` command and return you to the command prompt.

**Note:** Consider testing your work in [Google Chrome](https://www.google.com/chrome/) as Chrome tends to have good support for web platform features used by Progressive Web Apps, plus Chrome has several useful [developer tools](https://developer.chrome.com/devtools).

#### Adding the Shopping List Domain Model

[A domain model for the Shopping List app has already been implemented for you in JavaScript.](https://github.com/ibm-watson-data-lab/shopping-list-model-js) Rather than writing the domain logic and persistence logic yourself, you can instead use this domain model implementation in your Shopping List app. The domain model includes the following:

* **Shopping List Factory** (`ShoppingListFactory`)
  * `newShoppingList(values)`: Makes a new **Shopping List** entity (an [Immutable.js Record](https://facebook.github.io/immutable-js/docs/#/Record)) based on the supplied values
  * `newListOfShoppingLists(shoppingLists)`: Makes a new **List of Shopping Lists** (an [Immutable.js List](https://facebook.github.io/immutable-js/docs/#/List)) out of the supplied collection-like object
  * `newShoppingListItem(values, shoppingList)`: Makes a new **Shopping List Item** entity  (an [Immutable.js Record](https://facebook.github.io/immutable-js/docs/#/Record)) based on the supplied values
  * `newListOfShoppingListItems(shoppingListItems)`:  Makes a new **List of Shopping List Items** (an [Immutable.js List](https://facebook.github.io/immutable-js/docs/#/List)) out of the supplied collection-like object
* **Shopping List Repository for PouchDB** (`ShoppingListRepositoryPouchDB`)
  * `constructor(db)`: Constructs a new **Shopping List Repository for PouchDB** that uses the supplied PouchDB database
  * `ensureIndexes()`: Returns a Promise that resolves with an assurance that indexes needed for [Mango queries](https://pouchdb.com/guides/mango-queries.html) are in place
  * Methods for Persisting **Shopping Lists**
     * `put(shoppingList)`: Returns a Promise that resolves to a **Shopping List** entity persisted to PouchDB
     * `putBulk(shoppingLists)`: Returns a Promise that resolves to a **List of Shopping Lists** persisted to PouchDB
     * `get(shoppingListId)`: Returns a Promise that resolves to a **Shopping List** entity retrieved from PouchDB matching the supplied identifier
     * `find(request)`: Returns a Promise that resolves to a **List of Shopping Lists** retrieved from PouchDB matching the supplied Mango query request
     * `delete(shoppingList)`: Returns a Promise that resolves to a **Shopping List** entity deleted from PouchDB
  * Methods for Persisting **Shoping List Items**
     * `putItem(shoppingListItem)`: Returns a Promise that resolves to a **Shopping List Item** entity persisted to PouchDB
     * `putItemsBulk(shoppingListItems)`: Returns a Promise that resolves to a **List of Shopping List Items** persisted to PouchDB
     * `getItem(shoppingListItemId)`: Returns a Promise that resolves to a **Shopping List Item** entity retrieved from PouchDB matching the supplied identifier
     * `findItems(request)`: Returns a Promise that resolves to a **List of Shopping List Items** retrieved from PouchDB matching the supplied Mango query request
     * `findItemsCountByList(request, fields)`: Returns a Promise that resolves to the count of a **List of Shopping List Items** grouped by **Shopping List** retrieved from PouchDB matching the supplied Mango query request
     * `deleteItem(shoppingListItem)`: Returns a Promise that resolves to a **Shopping List Item** entity deleted from PouchDB
     * `deleteItemsBulk(shoppingListItems)`: Returns a Promise that resolves to a **List of Shopping List Items** deleted from PouchDB
     * `deleteItemsBulkByFind(request)`: Returns a Promise that resolves to a **List of Shopping List Items** deleted from PouchDB matching the supplied Mango query request.

##### Install the shopping list domain model

[[diff](https://github.com/ibm-watson-data-lab/shopping-list-polymer-pouchdb/commit/403a6be2354bb9c992e184bdc98bc261bf247f0c)]

The shopping list domain model is [published to npm](https://www.npmjs.com/package/ibm-shopping-list-model). However, we are using Bower to install our app's frontend dependencies. Fortunately there is a [Bower npm resolver](https://github.com/mjeanroy/bower-npm-resolver) that we can use to bridge this gap. Install the Bower npm resolver:

```
npm install -g bower-npm-resolver
```

Configure Bower to use the npm resolver by creating a `.bowerrc` file and adding the following content:

```javascript
 {
  "resolvers": [
    "bower-npm-resolver"
  ]
}
```

You should now be able to install the shopping list model using Bower:

```
bower install --save npm:ibm-shopping-list-model
```

##### Create a component to encapsulate the shopping list domain model

[[diff](https://github.com/ibm-watson-data-lab/shopping-list-polymer-pouchdb/commit/2c029d8ba590753f429d46587ba6352de77de336)]

The easiest way to use the domain model in your app is by encapsulating it in its own component. This will allow you to import the component wherever it is needed. Create a `shopping-list-model.html` file in the `src` directory (`src/shopping-list-model.html`) and add the following content:

```html
<dom-module id="shopping-list-model">
  <script src="../bower_components/ibm-shopping-list-model/dist/bundle.es6.js"></script>
</dom-module>
```

##### Use the shopping list domain model for one-way data binding of shopping lists

[[diff](https://github.com/ibm-watson-data-lab/shopping-list-polymer-pouchdb/commit/dcd7ecf33ba4b8d905cd481909601a8b8210295f)]

Now we will replace the stubbed out shopping list in `src/my-lists.html` with a one-way [data binding](https://www.polymer-project.org/2.0/docs/devguide/data-binding) to a **List of Shopping Lists**.

In `src/my-lists.html` add the following line to import the shopping list model component after `<link rel="import" href="../bower_components/iron-icons/iron-icons.html">`:

```html
<link rel="import" href="shopping-list-model.html">
```

Also in `src/my-lists.html` replace:

```html
    <paper-card heading="Groceries">
    </paper-card>
```

with:

```html
    <template is="dom-repeat" items="[[listOfShoppingListsArray]]">
      <a name="index" href="[[rootPath]]items/[[item._id]]">
        <paper-card heading="[[item.title]]">
        </paper-card>
      </a>
    </template>
 ```

An explanation of what this does:

* The first line is a [template repeater](https://www.polymer-project.org/2.0/docs/devguide/templates#dom-repeat) (`dom-repeat`) which binds to the `listOfShoppingListsArray` property and creates a new instance of the template contents for each element in the array, creating an `item` and an `index` property which can be used in each instance
* The second line provides a hyperlink to view the **List of Shopping List Items** for the current **Shopping List**, using the `item._id` property
* The third line creates a `paper-card` with a `heading` property having the value of the current `item.title` property
* Note that use of double square brackets (`[[ ]]`) which indicates one-way data binding, versus double curly brackets (`{{ }}`) which are used for two-way data binding

Next we need to declare the `listOfShoppingListsArray` property in order for the above template repeater to have something to which to bind. We will be declaring the `listOfShoppingListsArray` property as a *computed* property (a property that has its value computed based on a function). We will compute the `listOfShoppingListsArray` property's value using the `toArray()` method of the **List of Shopping Lists** Immutable.js List object. We will use the **Shopping List Factory** to create an empty **List of Shopping Lists** for now.

First let's set up our property declarations. In `src/my-lists.html` after `static get is() { return "my-lists"; }` add:

```javascript
      static get properties() {
        return {
        };
      }
```

Add the following property declaration:

```javascript
          shoppingListFactory: {
            type: Object,
            readOnly: true,
            notify: false,
            value: function() {
              return new ShoppingListModel.ShoppingListFactory();
            }
          },
```

An explanation:

* The property name is `shoppingListFactory`
* The property type is `Object`
* The property is read only, meaning it only produces data and never consumes data
* Since we don't intend to change the property value, we don't need to be notified with an event when the property value changes
* Earlier we imported a bundle from the shopping list domain model that makes a library named `ShoppingListModel` available in the global context
* The initial value of the `shoppingListFactory` property will be a new `ShoppingListFactory` object (accessed via the `ShoppingListModel` library in the global context)

Add another property declaration:

```javascript
          listOfShoppingLists: {
            type: Object,
            readOnly: true,
            notify: true,
            value: function() {
              return this.shoppingListFactory.newListOfShoppingLists();
            }
          },
```

An explanation:

* The above property represents the current **List of Shopping Lists** for the `MyLists` component
* The property's initial value is an empty **List of Shopping Lists**, but its value can be changed using a method named `_setListOfShoppingLists`

Add the `listOfShoppingListsArray` property declaration (the property to which our template repeater is bound):

```javascript
          listOfShoppingListsArray: {
            type: Array,
            readOnly: true,
            notify: true,
            computed: "_listOfShoppingListsArray(listOfShoppingLists)"
          },
```

An explanation:

* The `computed` field indicates the name of the method to be called in order to compute the value of `listOfShoppingListsArray` (we still need to write this method)
* The `_listOfShoppingListsArray` method takes a `listOfShoppingLists` parameter, which means the value of the `listOfShoppingLists` property will be passed to this method and the `listOfShoppingListsArray` value will be re-computed whenever the `listOfShoppingLists` property value changes

Finally let's add the `_listOfShoppingListsArray` method after the property declarations block:

```javascript
      _listOfShoppingListsArray(listOfShoppingLists) {
        return listOfShoppingLists.toArray();
      }
```

--

##### Create an empty state indicator for shopping lists

##### Add stub data to the shopping lists component

##### Add a loading spinner to the shopping lists component

#### Adding a PouchDB Database

##### Install PouchDB and pouchdb-find

##### Create a component to encapsulate PouchDB with pouchdb-find

##### Create a shared database property within the app component

##### Use the shopping list repository to find a list of shopping lists

##### Use PouchDB to listen for and propagate changes to shopping lists

##### Create a dialog with a form for creating a new shopping list

##### Create a new shopping list when the create new shopping list form is submitted

#### Completing the App

##### Use the shopping list domain model for one-way data binding of shopping list items

##### Create an empty state indicator for shopping list items

##### Add stub data to the shopping list items component

##### Add a loading spinner to the shopping list items component

##### Observe route changes in shopping list items component

##### Use the shopping list repository to find a list of shopping list items

##### Use PouchDB to listen for and propagate changes to shopping list items

##### Create a dialog with a form for creating a new shopping list item

##### Create a new shopping list item when the create new shopping list item form is submitted

##### Update database when a list item is checked or unchecked

### Syncing Data

#### Enable live replication with a remote database

## Workshop

TBD

## Developer Journey

TBD
