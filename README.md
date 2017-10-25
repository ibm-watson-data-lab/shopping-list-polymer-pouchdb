# Shopping List

[![Deploy to Bluemix](https://bluemix.net/deploy/button.png)](https://bluemix.net/deploy?repository=https://github.com/markstur/shopping-list-polymer-pouchdb&branch=cfbuild)

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
  * Enable Live Replication with a Remote Database
* Adding Multi-User / Multi-Device Features with Hoodie
  * Installing Hoodie
  * Configuring Hoodie
  * Using the Hoodie Store API
  * Using Hoodie Account API
  * Testing Offline Sync
* Adding Geolocation Features
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

Also in `index.html` change:

```html
    <meta name="application-name" content="My App">
```

to:

```html
    <meta name="application-name" content="Shopping List">
```

Still in `index.html` change:

```html
    <meta name="apple-mobile-web-app-title" content="My App">
```

to:

```html
    <meta name="apple-mobile-web-app-title" content="Shopping List">
```

The `index.html` file serves as the [app entrypoint](https://www.polymer-project.org/2.0/toolbox/server#app-entrypoint), which is responsible for instantiating the app shell.

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

Remove the following three lines from `polymer.json`:

```javascript
    "src/my-view1.html",
    "src/my-view2.html",
    "src/my-view3.html",
```

The `polymer.json` file [stores information about your project structure and your desired build configuration(s)](https://www.polymer-project.org/2.0/docs/tools/polymer-json). [The `fragments` property](https://www.polymer-project.org/2.0/docs/tools/polymer-json#fragments) (the property from which we are removing the references to the deleted views) is a way to specify components that may be lazy-loaded.

Remove the following three lines from `src/my-app.html`:

```html
<link rel="lazy-import" href="my-view1.html">
<link rel="lazy-import" href="my-view2.html">
<link rel="lazy-import" href="my-view3.html">
```

The above lines lazy-load the referenced components on demand.

Also in `src/my-app.html` remove the following three lines:

```html
          <a name="view1" href="[[rootPath]]view1">View One</a>
          <a name="view2" href="[[rootPath]]view2">View Two</a>
          <a name="view3" href="[[rootPath]]view3">View Three</a>
```

The above lines represent navigational links to the referenced routes.

Still in `src/my-app.html` remove the following three lines:

```html
          <my-view1 name="view1"></my-view1>
          <my-view2 name="view2"></my-view2>
          <my-view3 name="view3"></my-view3>
```

The above lines represent the pages for the referenced components.

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

Add the following line to the `fragments` property of the `polymer.json` before the line containing `"src/my-view404.html"`:

```javascript
    "src/my-lists.html",
```

Add the following line to the `src/my-app.html` file before the line containing `<link rel="lazy-import" href="my-view404.html">` (this will allow for lazy loading of our new `MyLists` component):

```html
<link rel="lazy-import" href="my-lists.html">
```

Add the following line to the `src/my-app.html` file between the opening and closing `<iron-selector>` tags (this will add a link to our new `MyLists` component in the app's navigation):

```html
          <a name="index" href="[[rootPath]]lists">Lists</a>
```

Add the following line to the `src/my-app.html` file before the line containing `<my-view404 name="view404"></my-view404>` (this will add our new `MyLists` component to the app):

```html
          <my-lists name="lists"></my-lists>
```

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

Add the following line to the `fragments` property of the `polymer.json` after the line containing `"src/my-lists.html",`:

```javascript
    "src/my-items.html",
```

Add the following line to the `src/my-app.html` file after the line containing `<link rel="lazy-import" href="my-lists.html">
` (this will allow for lazy loading of our new `MyItems` component):

```html
<link rel="lazy-import" href="my-items.html">
```

Add the following line to the `src/my-app.html` file after the line containing `<my-lists name="lists"></my-lists>` (this will add our new `MyItems` component to the app while binding its route to the app's subroute):

```html
          <my-items name="items" route="{{subroute}}"></my-items>
```

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
  * Methods for Persisting **Shopping List Items**
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

An explanation:

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
* The property's initial value is an empty **List of Shopping Lists**, but its value can be changed using a setter method named `_setListOfShoppingLists` generated by Polymer (see the Polymer documentation on [read-only properties](https://www.polymer-project.org/2.0/docs/devguide/properties#read-only))

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

##### Create an empty state indicator for shopping lists

[[diff](https://github.com/ibm-watson-data-lab/shopping-list-polymer-pouchdb/commit/2a83a42c0d87a8e895af85aa940a118f002dda99)]

When the **List of Shopping Lists** is empty we should display an [empty state](https://material.io/guidelines/patterns/empty-states.html) indicator. Add the following style to the `<style>` section of the `MyLists` component (`src/my-lists.html`) in order to style the empty state indicator:

```css
      div.empty-state {
        text-align: center;
        margin-top: 120px;
      }
```

Add the empty state indicator before `<template is="dom-repeat" items="[[listOfShoppingListsArray]]">`:

```html
    <template is="dom-if" if="[[listOfShoppingListsIsEmpty]]">
      <div class="empty-state">You have no shopping lists</div>
    </template>
```
An explanation:

* The first line is a [conditional templates](https://www.polymer-project.org/2.0/docs/devguide/templates#dom-if) (`dom-if`) which binds to the `listOfShoppingListsIsEmpty` property and only displays the template contents if the property's value is `true`.
* Note that use of double square brackets (`[[ ]]`) again which indicates one-way data binding, versus double curly brackets (`{{ }}`) which are used for two-way data binding

Add the `listOfShoppingListsIsEmpty` property declaration (the property to which our conditional template is bound):

```javascript
          listOfShoppingListsIsEmpty: {
            type: Boolean,
            readOnly: true,
            notify: true,
            computed: "_listOfShoppingListsIsEmpty(listOfShoppingLists)"
          },
```

An explanation:

* The `computed` field indicates the name of the method to be called in order to compute the value of `listOfShoppingListsIsEmpty` (we still need to write this method)
* The `_listOfShoppingListsIsEmpty` method takes a `listOfShoppingLists` parameter, which means the value of the `listOfShoppingLists` property will be passed to this method and the `listOfShoppingListsIsEmpty` value will be re-computed whenever the `listOfShoppingLists` property value changes

Finally let's add the `_listOfShoppingListsIsEmpty` method after our `_listOfShoppingListsArray(listOfShoppingLists)` method :

```javascript
      _listOfShoppingListsIsEmpty(listOfShoppingLists) {
        return listOfShoppingLists.isEmpty();
      }
```

All the `_listOfShoppingListsIsEmpty` method does is return the result of calling the `isEmpty()` method on the Immutable.js List object that represents the **List of Shopping Lists**.

Let's take a look at our empty state indicator. Start the Polymer development server:

```
$ polymer serve
info:    Files in this directory are available under the following URLs
      applications: http://127.0.0.1:8081
      reusable components: http://127.0.0.1:8081/components/polymer-starter-kit/
```

You should now be able to browse to `http://127.0.0.1:8081` in your web browser and see the Shopping List app with an empty state indicator on the shopping lists page. When you're done, close the browser tab containing the Shopping List app. Back in your terminal, use `Ctrl-C` to cancel the `polymer serve` command and return you to the command prompt.

##### Add stub data to the shopping lists component

[[diff](https://github.com/ibm-watson-data-lab/shopping-list-polymer-pouchdb/commit/3b2e4c4a192ad1a04df260ffd4bac7bd78d0dc8a)]

Let's add some stub data to the `MyLists` component so that we can see the data binding in action. Add the following to the `src/my-lists.html` file after the `_listOfShoppingListsIsEmpty(listOfShoppingLists)` method:

```javascript
      ready() {
        super.ready();
        let shoppingList01 = this.shoppingListFactory.newShoppingList({
          title: "Groceries"
        });
        let shoppingList02 = this.shoppingListFactory.newShoppingList({
          title: "Camping Supplies"
        });
        let listOfShoppingLists = this.shoppingListFactory.newListOfShoppingLists([
          shoppingList01,
          shoppingList02
        ]);
        this._setListOfShoppingLists(listOfShoppingLists);
      }
```

An explanation:

* The `ready` method is a [Polymer lifecycle callback](https://www.polymer-project.org/2.0/docs/devguide/registering-elements#lifecycle-callbacks) which is used for one-time configuration of the component
* Since we are overriding an existing method, we need to call the parent method with `super.ready()` to ensure that the component is properly initialized
* We create two different **Shopping List** entities (`shoppingList01` and `shoppingList02`) using the `newShoppingList(values)` method of the **Shopping List Factory**
* We create a new **List of Shopping Lists** using the `newListOfShoppingLists(shoppingLists)` method of the **Shopping List Factory**
* We change the value of the `listOfShoppingLists` property using the `_setListOfShoppingLists(value)` setter method generated by Polymer (see the Polymer documentation on [read-only properties](https://www.polymer-project.org/2.0/docs/devguide/properties#read-only)) which will cascade to also change the values of the `listOfShoppingListsArray` and the `listOfShoppingListsIsEmpty` properties

Let's take a look at our `MyLists` component with stub data. Start the Polymer development server:

```
$ polymer serve
info:    Files in this directory are available under the following URLs
      applications: http://127.0.0.1:8081
      reusable components: http://127.0.0.1:8081/components/polymer-starter-kit/
```

You should now be able to browse to `http://127.0.0.1:8081` in your web browser and see the Shopping List app with a "Groceries" and a "Camping Supplies" shopping list on the shopping lists page. When you're done, close the browser tab containing the Shopping List app. Back in your terminal, use `Ctrl-C` to cancel the `polymer serve` command and return you to the command prompt.

##### Add a loading spinner to the shopping lists component

[[diff](https://github.com/ibm-watson-data-lab/shopping-list-polymer-pouchdb/commit/e547226424f45fd32ef2a376f9e07d201d9ecb0a)]

We should display a [loading spinner](https://material.io/guidelines/components/progress-activity.html) when the `MyLists` component is loading its **List of Shopping Lists**. This will become more important when we are loading data from a database. Even then, since this is an Offline First app it should load data very fast as all data access happens locally.

Install the [`paper-spinner`](https://www.webcomponents.org/element/PolymerElements/paper-spinner) element:

```
$ bower install --save PolymerElements/paper-spinner#^2.0.0
```

In `src/my-lists.html` add the following line to import the `paper-spinner` component after `<link rel="import" href="../bower_components/iron-icons/iron-icons.html">`:

```html
<link rel="import" href="../bower_components/paper-spinner/paper-spinner.html">
```

Add the following style to the `<style>` section of `src/my-lists.html` in order to style the loading spinner:

```css
      #paperSpinnerContainer {
        text-align: center;
        margin-top: 120px;
      }
```

Within `src/my-lists.html` add the loading spinner wrapped in a conditional template bound to the `loading` property (which we still need to create):

```html
    <template is="dom-if" if="[[loading]]">
      <div id="paperSpinnerContainer">
        <paper-spinner active></paper-spinner>
      </div>
    </template>
```

Within `src/my-lists.html` wrap the empty state indicator and the template repeater in a second conditional template bound to the negated state of the `loading` property (only the first and last lines in the below code snippet are new):

```html
    <template is="dom-if" if="[[!loading]]">

      <template is="dom-if" if="[[listOfShoppingListsIsEmpty]]">
        <div class="empty-state">You have no shopping lists</div>
      </template>

      <template is="dom-repeat" items="[[listOfShoppingListsArray]]">
        <a name="index" href="[[rootPath]]items/[[item._id]]">
          <paper-card heading="[[item.title]]">
          </paper-card>
        </a>
      </template>

    </template>
```

Within `src/my-lists.html` add the `loading` property declaration (the property to which our conditional templates are bound):

```javascript
          loading: {
            type: Boolean,
            notify: true,
            value: true
          },
```

Let's take a look at our `MyLists` component with a loading spinner. Start the Polymer development server:

```
$ polymer serve
info:    Files in this directory are available under the following URLs
      applications: http://127.0.0.1:8081
      reusable components: http://127.0.0.1:8081/components/polymer-starter-kit/
```

You should now be able to browse to `http://127.0.0.1:8081` in your web browser and see the Shopping List app with a loading spinner on the shopping lists page that will continue to spin indefinitely. When you're done, close the browser tab containing the Shopping List app. Back in your terminal, use `Ctrl-C` to cancel the `polymer serve` command and return you to the command prompt.

Let's stop the loading indicator once we've set our **List of Shopping Lists**. Within `src/my-lists.html` add the following as the last line of the `ready()` method:

```javascript
        this.loading = false;
```

#### Adding a PouchDB Database

In the next steps we will install and use a [PouchDB](https://pouchdb.com/) database to persist data within the frontend app. PouchDB is a JavaScript database that syncs. PouchDB stores its data in IndexedDB (other adapters, such as WebSQL, are available for environments that don't support IndexedDB). Data will be persisted in the browser when the app is closed, and available again when the app is re-opened. Data stored in a PouchDB database can be sync'ed to and from any other database that implements the [CouchDB Replication Protocol](http://docs.couchdb.org/en/2.1.0/replication/protocol.html).

##### Install PouchDB and pouchdb-find

[[diff](https://github.com/ibm-watson-data-lab/shopping-list-polymer-pouchdb/commit/f43025130b2bc44b066dfb4d2e7d6bbba5a1493a)]

Install PouchDB:

```
$ bower install --save pouchdb
```

Install the pouchdb-find plugin which will give us the ability to perform [Mango queries](https://pouchdb.com/guides/mango-queries.html) (a query language inspired by MongoDB):

```
$ bower install --save pouchdb-find
```

##### Create a component to encapsulate PouchDB with pouchdb-find

[[diff](https://github.com/ibm-watson-data-lab/shopping-list-polymer-pouchdb/commit/ae61c5ab99cc0c476b03020de7a0f9ba86ef308b)]

The easiest way to use PouchDB and pouchdb-find in your app is by encapsulating the two libraries in their own component. This will allow you to import the component wherever it is needed. Create a `pouchdb.html` file in the `src` directory (`src/pouchdb.html`) and add the following content:

```html
<dom-module id="pouchdb">
  <script src="../bower_components/pouchdb/dist/pouchdb.js"></script>
  <script src="../bower_components/pouchdb-find/dist/pouchdb.find.js"></script>
</dom-module>
```

##### Create a shared database property within the app component

[[diff](https://github.com/ibm-watson-data-lab/shopping-list-polymer-pouchdb/commit/ca335b5a326bba0e8b07adf7a7ed27454b075bd5)]

Rather than create a PouchDB database instance in each of our app's components, we will create one database instance that is shared between components.

In `src/my-app.html` add the following line to import the PouchDB component (created in the previous step) after `<link rel="import" href="my-icons.html">`:

```html
<link rel="import" href="pouchdb.html">
```

In `src/my-app.html` add the following property declaration:

```javascript
          db: {
            type: Object,
            readOnly: true,
            notify: false,
            value: function() {
              return new PouchDB("shopping-list", { storage: "persistent" });
            }
          },
```

Bind the `db` property to the `MyLists` and `MyItems` components using one-way data binding (which will add a `db` property to each of these components) by changing:

```html
          <my-lists name="lists"></my-lists>
          <my-items name="items" route="{{subroute}}"></my-items>
```

to:

```html
          <my-lists name="lists" db="[[db]]"></my-lists>
          <my-items name="items" route="{{subroute}}" db="[[db]]"></my-items>
```

The only difference between the two is the addition of a `db="[[db]]"` attribute/value pair.

##### Use the shopping list repository to find a list of shopping lists

[[diff](https://github.com/ibm-watson-data-lab/shopping-list-polymer-pouchdb/commit/d9e5658836e6e0e4ddb42983fb068c524ac41325)]

In `src/my-lists.html` declare a `shoppingListRepository` property for our **Shopping List Repository** instance:

```javascript
          shoppingListRepository: {
            type: Object,
            readOnly: true,
            notify: false,
            value: function() {
              return new ShoppingListModel.ShoppingListRepositoryPouchDB(this.db);
            }
          },
```

In `src/my-lists.html` create a `_findListOfShoppingLists()` method for finding a **List of Shopping Lists** in PouchDB (via the **Shopping List Repository**) and updating the `listOfShoppingLists` property accordingly:

```
      _findListOfShoppingLists() {
        this.loading = true;
        this.shoppingListRepository.find().then(listOfShoppingLists => {
          this._setListOfShoppingLists(listOfShoppingLists);
          this.loading = false;
        });
      }
```

In `src/my-lists.html` *remove* the `ready()` method that creates stub data and replace it with the following `ready()` method that ensures that the indexes needed for Mango queries are in place and triggers a database query when the component is ready:

```javascript
      ready() {
        super.ready();
        this.shoppingListRepository.ensureIndexes();
        this._findListOfShoppingLists();
      }
```

Let's test our work so far. Start the Polymer development server:

```
$ polymer serve
info:    Files in this directory are available under the following URLs
      applications: http://127.0.0.1:8081
      reusable components: http://127.0.0.1:8081/components/polymer-starter-kit/
```

You should now be able to browse to `http://127.0.0.1:8081` in your web browser and see the Shopping List app. You may notice the loading spinner displayed briefly, after which you should see the empty state indicator. When you're done, close the browser tab containing the Shopping List app. Back in your terminal, use `Ctrl-C` to cancel the `polymer serve` command and return you to the command prompt.

##### Use PouchDB to listen for and propagate changes to shopping lists

[[diff](https://github.com/ibm-watson-data-lab/shopping-list-polymer-pouchdb/commit/d4748572400107b672c9b35155fb968495234f9a)]

We should update our **List of Shopping Lists** displayed when data changes within PouchDB after the initial load of the `MyLists` component. Fortunately PouchDB provides an [API for listening to database changes](https://pouchdb.com/api.html#changes). In `src/my-lists.html` declare a `dbChanges` property that we can use if we want to cancel our listeners or add listeners:

```javascript
          dbChanges: {
            type: Object,
            notify: false
          },
```

In `src/my-lists.html` at the end of the `ready()` method add the following code:

```javascript
        this.dbChanges = this.db.changes({
          live: true,
          selector: {
            type: "list"
          }
        }).on("change", change => {
          this._findListOfShoppingLists();
        });
```

An explanation:

* The `live` option tells PouchDB we want to be notified of all future changes until cancelled
* The `selector` option is a Mango selector that allows us to filter by documents matching this selector
* Whenever a change is received we call the `_findListOfShoppingLists()` method to refresh our **List of Shopping Lists**

##### Create a dialog with a form for creating a new shopping list

[[diff](https://github.com/ibm-watson-data-lab/shopping-list-polymer-pouchdb/commit/734f666802ed43b1c890d1f91cc21c2913279838)]

We obviously need the ability to create new **Shopping List** entities. First we will create a dialog and a form for creating a new **Shopping List**. Then in the next section we will write the code for handling the submission of this form.

Install the [`paper-dialog`](https://www.webcomponents.org/element/PolymerElements/paper-dialog) element:

```
$ bower install --save PolymerElements/paper-dialog#^2.0.0
```

Install the [`iron-form`](https://www.webcomponents.org/element/PolymerElements/iron-form) element:

```
$ bower install --save PolymerElements/iron-form#^2.0.0
```

Install the [`paper-input`](https://www.webcomponents.org/element/PolymerElements/paper-input) element:

```
$ bower install --save PolymerElements/paper-input#^2.0.0
```

Install the [`paper-button`](https://www.webcomponents.org/element/PolymerElements/paper-button) element:

```
$ bower install --save PolymerElements/paper-button#^2.0.0
```

In `src/my-lists.html` add the following lines to import the `paper-dialog`, `iron-form`, `paper-input`, and `paper-button` components after `<link rel="import" href="../bower_components/paper-spinner/paper-spinner.html">`:

```html
<link rel="import" href="../bower_components/paper-dialog/paper-dialog.html">
<link rel="import" href="../bower_components/iron-form/iron-form.html">
<link rel="import" href="../bower_components/paper-input/paper-input.html">
<link rel="import" href="../bower_components/paper-button/paper-button.html">
```

Add the following style to the `<style>` section of the `MyLists` component (`src/my-lists.html`) in order to style the dialog:

```css
      paper-dialog {
        width: 332px;
        padding: 8px;
      }
```

In `src/my-lists.html` add the the following code for the dialog after `<paper-fab mini icon="add"></paper-fab>`:

```html
    <paper-dialog id="listAddDialog">
      <h2>New List</h2>
      <paper-dialog-scrollable>
        <iron-form id="listAddForm">
          <paper-input id="newListTitle" name="title" label="Title" value="{{newList.title}}" required autofocus></paper-input>
        </iron-form>
      </paper-dialog-scrollable>
      <div class="buttons">
        <paper-button dialog-dismiss raised>Cancel</paper-button>
        <paper-button dialog-confirm raised>Save</paper-button>
      </div>
    </paper-dialog>
```

In `src/my-lists.html` declare a `newList` property to represent the new **Shopping List** entity as entered by the app user:

```javascript
          newList: {
            type: Object,
            notify: false,
            value: {}
          },
```

In `src/my-lists.html` add an `on-click` handler to the floating action button, replacing:

```html
    <paper-fab mini icon="add"></paper-fab>
```

with:

```
    <paper-fab mini icon="add" on-click="_listAdd"></paper-fab>
```

In `src/my-lists.html` add the `_listAdd()` method to open the dialog that will be called when the floating action button is clicked:

```
      _listAdd() {
        this.$.listAddDialog.open();
      }
```

##### Create a new shopping list when the create new shopping list form is submitted

[[diff](https://github.com/ibm-watson-data-lab/shopping-list-polymer-pouchdb/commit/215e835f1efb6fda2953487b0ea031961e7ba394)]

The final step to be able to create a new **Shopping List** entity is to wire up the form submission. In `src/my-lists.html` add an `on-click` handler to the "Save" button in the form, replacing:

```html
        <paper-button dialog-confirm raised>Save</paper-button>
```

with:

```html
        <paper-button dialog-confirm raised on-click="_listAddFormSubmit">Save</paper-button>
```

In `src/my-lists.html` add the `_listAddFormSubmit()` method to handle the form submission when the "Save" button is clicked:

```javascript
      _listAddFormSubmit() {
        let shoppingList = this.shoppingListFactory.newShoppingList({
          title: this.newList.title
        });
        this.shoppingListRepository.put(shoppingList).then(shoppingList => {
          this.$.listAddForm.reset();
          this.newList = {};
          this.$.listAddDialog.close();
        });
      }
```

Let's try it out! Start the Polymer development server:

```
$ polymer serve
info:    Files in this directory are available under the following URLs
      applications: http://127.0.0.1:8081
      reusable components: http://127.0.0.1:8081/components/polymer-starter-kit/
```

You should now be able to browse to `http://127.0.0.1:8081` in your web browser and see the Shopping List app. Click the floating action button on the shopping lists page. Enter a title for your new shopping list. Click "Save" and the dialog should close. You should now see your new **Shopping List** in the **List of Shopping Lists** rather than the empty state indicator. When you're done, close the browser tab containing the Shopping List app. Back in your terminal, use `Ctrl-C` to cancel the `polymer serve` command and return you to the command prompt.

#### Completing the App

The instructions in this section are for the `MyItems` component and are similar to the previous steps completed for the `MyLists` component. New concepts covered in this section include observing route changes in Polymer (in order to display the **List of Shopping List Items** for the currently-selected **Shopping List**) and updating a document in the PouchDB database (via the **Shopping List Repository**) based on user action.

##### Use the shopping list domain model for one-way data binding of shopping list items

[[diff](https://github.com/ibm-watson-data-lab/shopping-list-polymer-pouchdb/commit/276fcddf697528be868c57a0d1d2f7395920df89)]

Now we will replace the stubbed out shopping list items in `src/my-items.html` with a one-way [data binding](https://www.polymer-project.org/2.0/docs/devguide/data-binding) to a **List of Shopping List Items**.

In `src/my-items.html` add the following line to import the shopping list model component after `<link rel="import" href="../bower_components/iron-icons/iron-icons.html">`:

```html
<link rel="import" href="shopping-list-model.html">
```

Also in `src/my-items.html` replace:

```html
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
```

with:

```html
    <template is="dom-if" if="[[!listOfShoppingListItemsIsEmpty]]">
      <paper-listbox>
        <template is="dom-repeat" items="[[listOfShoppingListItemsArray]]">
          <paper-item data-checked$="[[item.checked]]">
            <paper-checkbox data-id$="[[item._id]]" checked="[[item.checked]]"></paper-checkbox>
            <paper-item-body>
              <div>[[item.title]]</div>
            </paper-item-body>
            <iron-icon icon="more-vert"></iron-icon>
          </paper-item>
        </template>
      </paper-listbox>
    </template>
```

Next we need to declare the `listOfShoppingListItemsArray` property in order for the above template repeater to have something to which to bind. We will be declaring the `listOfShoppingListItemsArray` property as a *computed* property (a property that has its value computed based on a function). We will compute the `listOfShoppingListItemsArray` property's value using the `toArray()` method of the **List of Shopping List Items** Immutable.js List object. We will use the **Shopping List Factory** to create an empty **List of Shopping List Items** for now.

First let's set up our property declarations. In `src/my-items.html` after `static get is() { return "my-items"; }` add:

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

Add another property declaration:

```javascript
          listOfShoppingListItems: {
            type: Object,
            readOnly: true,
            notify: true,
            value: function() {
              return this.shoppingListFactory.newListOfShoppingListItems();
            }
          },
```

Add the `listOfShoppingListItemsArray` property declaration (the property to which our template repeater is bound):

```javascript
          listOfShoppingListItemsArray: {
            type: Array,
            readOnly: true,
            notify: true,
            computed: "_listOfShoppingListItemsArray(listOfShoppingListItems)"
          },
```

Add the `_listOfShoppingListItemsArray` method after the property declarations block:

```javascript
      _listOfShoppingListItemsArray(listOfShoppingListItems) {
        return listOfShoppingListItems.toArray();
      }
```

Add the `listOfShoppingListItemsIsEmpty` property declaration (the property to which our conditional template is bound):

```javascript
          listOfShoppingListItemsIsEmpty: {
            type: Boolean,
            readOnly: true,
            notify: true,
            computed: "_listOfShoppingListItemsIsEmpty(listOfShoppingListItems)"
          },
```

Finally let's add the `_listOfShoppingListItemsIsEmpty` method after the `_listOfShoppingListItemsArray` method:

```javascript
      _listOfShoppingListItemsIsEmpty(listOfShoppingListItems) {
        return listOfShoppingListItems.isEmpty();
      }
```

##### Create an empty state indicator for shopping list items

[[diff](https://github.com/ibm-watson-data-lab/shopping-list-polymer-pouchdb/commit/33c9380df827c0463bea5e3e8aa244db92fa374f)]

When the **List of Shopping List Items** is empty we should display an [empty state](https://material.io/guidelines/patterns/empty-states.html) indicator. Add the following style to the `<style>` section of the `MyItems` component (`src/my-items.html`) in order to style the empty state indicator:

```css
      div.empty-state {
        text-align: center;
        margin-top: 120px;
      }
```

Add the empty state indicator before `<template is="dom-if" if="[[!listOfShoppingListItemsIsEmpty]]">`:

```html
    <template is="dom-if" if="[[listOfShoppingListItemsIsEmpty]]">
      <div class="empty-state">You have no shopping list items</div>
    </template>
```

##### Add stub data to the shopping list items component

[[diff](https://github.com/ibm-watson-data-lab/shopping-list-polymer-pouchdb/commit/76ac923003ec870aadb3f9981ea1a9afb0a7ffa0)]

Let's add some stub data to the `MyItems` component so that we can see the data binding in action. Add the following to the `src/my-items.html` file after the `_listOfShoppingListItemsIsEmpty(listOfShoppingListItems)` method:

```javascript
      ready() {
        super.ready();
        let shoppingList = this.shoppingListFactory.newShoppingList({
          title: "Groceries"
        });
        let shoppingListItem01 = this.shoppingListFactory.newShoppingListItem({
          title: "Mangos",
          checked: true
        }, shoppingList);
        let shoppingListItem02 = this.shoppingListFactory.newShoppingListItem({
          title: "Oranges"
        }, shoppingList);
        let shoppingListItem03 = this.shoppingListFactory.newShoppingListItem({
          title: "Pears"
        }, shoppingList);
        let listOfShoppingListItems = this.shoppingListFactory.newListOfShoppingListItems([
          shoppingListItem01,
          shoppingListItem02,
          shoppingListItem03
        ]);
        this._setListOfShoppingListItems(listOfShoppingListItems);
      }
```

Let's take a look at our `MyItems` component with stub data. Start the Polymer development server:

```
$ polymer serve
info:    Files in this directory are available under the following URLs
      applications: http://127.0.0.1:8081
      reusable components: http://127.0.0.1:8081/components/polymer-starter-kit/
```

You should now be able to browse to `http://127.0.0.1:8081` in your web browser and see the Shopping List app. Create a **Shopping List** if one hasn't already been created. Click on any **Shopping List** and you should see "Mangos", "Oranges," and "Pears" on the shopping list items page. When you're done, close the browser tab containing the Shopping List app. Back in your terminal, use `Ctrl-C` to cancel the `polymer serve` command and return you to the command prompt.

##### Add a loading spinner to the shopping list items component

[[diff](https://github.com/ibm-watson-data-lab/shopping-list-polymer-pouchdb/commit/3e00ea78a1e2fe57c6fa3f103caae6506e852ce2)]

We should display a [loading spinner](https://material.io/guidelines/components/progress-activity.html) when the `MyItems` component is loading its **List of Shopping List Items**. This will become more important when we are loading data from a database. Even then, since this is an Offline First app it should load data very fast as all data access happens locally.

In `src/my-items.html` add the following line to import the `paper-spinner` component after `<link rel="import" href="../bower_components/iron-icons/iron-icons.html">`:

```html
<link rel="import" href="../bower_components/paper-spinner/paper-spinner.html">
```

Add the following style to the `<style>` section of `src/my-items.html` in order to style the loading spinner:

```css
      #paperSpinnerContainer {
        text-align: center;
        margin-top: 120px;
      }
```

Within `src/my-items.html` add the loading spinner wrapped in a conditional template bound to the `loading` property (which we still need to create):

```html
    <template is="dom-if" if="[[loading]]">
      <div id="paperSpinnerContainer">
        <paper-spinner active></paper-spinner>
      </div>
    </template>
```

Within `src/my-items.html` wrap the empty state indicator and the conditional template for displaying a **List of Shopping List Items** in another conditional template bound to the negated state of the `loading` property (only the first and last lines in the below code snippet are new):

```html
    <template is="dom-if" if="[[!loading]]">

      <template is="dom-if" if="[[listOfShoppingListItemsIsEmpty]]">
        <div class="empty-state">You have no shopping list items</div>
      </template>

      <template is="dom-if" if="[[!listOfShoppingListItemsIsEmpty]]">
        <paper-listbox>
          <template is="dom-repeat" items="[[listOfShoppingListItemsArray]]">
            <paper-item data-checked$="[[item.checked]]">
              <paper-checkbox data-id$="[[item._id]]" checked="[[item.checked]]"></paper-checkbox>
              <paper-item-body>
                <div>[[item.title]]</div>
              </paper-item-body>
              <iron-icon icon="more-vert"></iron-icon>
            </paper-item>
          </template>
        </paper-listbox>
      </template>

    </template>
```

Within `src/my-items.html` add the `loading` property declaration (the property to which our conditional templates are bound):

```javascript
          loading: {
            type: Boolean,
            notify: true,
            value: true
          },
```

Let's stop the loading indicator once we've set our **List of Shopping List Items**. Within `src/my-items.html` add the following as the last line of the `ready()` method:

```javascript
        this.loading = false;
```

##### Observe route changes in shopping list items component

[[diff](https://github.com/ibm-watson-data-lab/shopping-list-polymer-pouchdb/commit/d7c2b79c4b7afa58e2d2e59392796e5ecb6558dc)]

When a user selects a **Shopping List** from a **List of Shopping Lists** in the app this will trigger a route change. We need to observe route changes in our `MyItems` component and update our **List of Shopping List Items** to match the currently-selected **Shopping List**.

In `src/my-items.html` after `static get is() { return "my-items"; }` (and before the property declarations block) declare the following observer:

```javascript
      static get observers() {
        return [
          "_routeChanged(route.*)"
        ]
      }
```

In `src/my-items.html` add a `shoppingListId` property declaration the value of which will represent the identifier for the currently-selected **Shopping List** entity:

```javascript
          shoppingListId: {
            type: String,
            readOnly: true,
            notify: true
          },
```

In `src/my-items.html` add the `_routeChanged(route)` method which will be called whenever the route changes in Polymer and will set the value of the `shoppingListId` property accordingly:

```javascript
      _routeChanged(route) {
        if (route.base.prefix !== this.rootPath + "items") {
          return;
        }
        this._setShoppingListId(route.base.path.replace(/\//g, ""));
      }
```

##### Use the shopping list repository to find a list of shopping list items

[[diff](https://github.com/ibm-watson-data-lab/shopping-list-polymer-pouchdb/commit/526d0a4753ab1537f9a34c45eb7fb18779dc273d)]

In `src/my-items.html` declare a `shoppingListRepository` property for our **Shopping List Repository** instance:

```javascript
          shoppingListRepository: {
            type: Object,
            readOnly: true,
            notify: false,
            value: function() {
              return new ShoppingListModel.ShoppingListRepositoryPouchDB(this.db);
            }
          },
```

In `src/my-items.html` declare a `shoppingList` property to represent the currently-selected **Shopping List** entity:

```javascript
          shoppingList: {
            type: Object,
            readOnly: true,
            notify: true,
          },
```


In `src/my-items.html` create a `_findShoppingList()` method for finding the currently-selected **Shopping List** in PouchDB (via the **Shopping List Repository**) and updating the `shoppingList` property accordingly:

```
      _findShoppingList() {
        if (this.shoppingListId === undefined) {
          this._setShoppingList(undefined);
          return;
        }
        this.shoppingListRepository.get(this.shoppingListId).then(shoppingList => {
          this._setShoppingList(shoppingList);
        });
      }
```


In `src/my-items.html` create a `_findListOfShoppingListItems()` method for finding a **List of Shopping List Items** for the currently-selected **Shopping List** in PouchDB (via the **Shopping List Repository**) and updating the `listOfShoppingListItems` property accordingly:

```
      _findListOfShoppingListItems() {
        this.loading = true;
        if (this.shoppingListId === undefined) {
          this._setListOfShoppingListItems(this.shoppingListFactory.newListOfShoppingListItems());
          return;
        }
        this.shoppingListRepository.findItems({
          selector: {
            type: "item",
            list: this.shoppingListId
          }
        }).then(listOfShoppingListItems => {
          this._setListOfShoppingListItems(listOfShoppingListItems);
          this.loading = false;
        });
      }
```

In `src/my-items.html` add an observer to the `shoppingListId` property (this is a method that will be called whenever the property's value changes) (only the `observer: "_shoppingListIdChanged"` part of the code below is new):

```javascript
          shoppingListId: {
            type: String,
            readOnly: true,
            notify: true,
            observer: "_shoppingListIdChanged"
          },
```

In `src/my-items.html` add the `_shoppingListIdChanged(newshoppingListId, oldshoppingListId)` method which will call the `_findShoppingList()` and `_findListOfShoppingListItems()` methods when the `shoppingListId` property value has changed:

```javascript
      _shoppingListIdChanged(newshoppingListId, oldshoppingListId) {
        this._findShoppingList();
        this._findListOfShoppingListItems();
      }
```

In `src/my-items.html` *remove* the `ready()` method that creates stub data and replace it with the following `ready()` method that ensures that the indexes needed for Mango queries are in place and triggers the database queries when the component is ready:

```javascript
      ready() {
        super.ready();
        this.shoppingListRepository.ensureIndexes();
        this._findShoppingList();
        this._findListOfShoppingListItems();
      }
```

##### Use PouchDB to listen for and propagate changes to shopping list items

[[diff](https://github.com/ibm-watson-data-lab/shopping-list-polymer-pouchdb/commit/7137c6870e353e6dc65f0215b9022af8a19c7d25)]

We should update our **List of Shopping List Items** displayed when data changes within PouchDB after the initial load of the `MyItems` component. Fortunately PouchDB provides an [API for listening to database changes](https://pouchdb.com/api.html#changes). In `src/my-items.html` declare a `dbChanges` property that we can use if we want to cancel our listeners or add listeners:

```javascript
          dbChanges: {
            type: Object,
            notify: false
          },
```

In `src/my-items.html` at the end of the `ready()` method add the following code:

```javascript
        this.dbChanges = this.db.changes({
          live: true,
          selector: {
            type: "item"
          }
        }).on("change", change => {
          this._findListOfShoppingListItems();
        });
```

##### Create a dialog with a form for creating a new shopping list item

[[diff](https://github.com/ibm-watson-data-lab/shopping-list-polymer-pouchdb/commit/75561467a879aecea4e0055d5da074386bf952ca)]

We will now add the ability to create new **Shopping List Item** entities. First we will create a dialog and a form for creating a new **Shopping List Item**. Then in the next section we will write the code for handling the submission of this form.

In `src/my-items.html` add the following lines to import the `paper-dialog`, `iron-form`, `paper-input`, and `paper-button` components after `<link rel="import" href="../bower_components/paper-spinner/paper-spinner.html">`:

```html
<link rel="import" href="../bower_components/paper-dialog/paper-dialog.html">
<link rel="import" href="../bower_components/iron-form/iron-form.html">
<link rel="import" href="../bower_components/paper-input/paper-input.html">
<link rel="import" href="../bower_components/paper-button/paper-button.html">
```

Add the following style to the `<style>` section of the `MyItems` component (`src/my-items.html`) in order to style the dialog:

```css
      paper-dialog {
        width: 332px;
        padding: 8px;
      }
```

In `src/my-items.html` add the the following code for the dialog after `<paper-fab mini icon="add"></paper-fab>`:

```html
    <paper-dialog id="listItemAddDialog">
      <h2>New List Item</h2>
      <paper-dialog-scrollable>
        <iron-form id="listItemAddForm">
          <paper-input id="newListItemTitle" name="title" label="Title" value="{{newListItem.title}}" required autofocus></paper-input>
        </iron-form>
      </paper-dialog-scrollable>
      <div class="buttons">
        <paper-button dialog-dismiss raised>Cancel</paper-button>
        <paper-button dialog-confirm raised>Save</paper-button>
      </div>
    </paper-dialog>
```

In `src/my-items.html` declare a `newListItem` property to represent the new **Shopping List Item** entity as entered by the app user:

```javascript
          newListItem: {
            type: Object,
            notify: false,
            value: {}
          },
```

In `src/my-items.html` add an `on-click` handler to the floating action button, replacing:

```html
    <paper-fab mini icon="add"></paper-fab>
```

with:

```
    <paper-fab mini icon="add" on-click="_listItemAdd"></paper-fab>
```

In `src/my-items.html` add the `_listItemAdd()` method to open the dialog that will be called when the floating action button is clicked:

```
      _listItemAdd() {
        this.$.listItemAddDialog.open();
      }
```

##### Create a new shopping list item when the create new shopping list item form is submitted

[[diff](https://github.com/ibm-watson-data-lab/shopping-list-polymer-pouchdb/commit/4c4fd6efa193da43f91f4f271811d3e5ef7d6f49)]

The final step to be able to create a new **Shopping List Item** entity is to wire up the form submission. In `src/my-items.html` add an `on-click` handler to the "Save" button in the form, replacing:

```html
        <paper-button dialog-confirm raised>Save</paper-button>
```

with:

```html
        <paper-button dialog-confirm raised on-click="_listItemAddFormSubmit">Save</paper-button>
```

In `src/my-items.html` add the `_listItemAddFormSubmit()` method to handle the form submission when the "Save" button is clicked:

```javascript
      _listItemAddFormSubmit() {
        let shoppingListItem = this.shoppingListFactory.newShoppingListItem({
          title: this.newListItem.title
        }, this.shoppingList);
        this.shoppingListRepository.putItem(shoppingListItem).then(shoppingListItem => {
          this.$.listItemAddForm.reset();
          this.newListItem = {};
          this.$.listItemAddDialog.close();
        });
      }
```

##### Update database when a list item is checked or unchecked

[[diff](https://github.com/ibm-watson-data-lab/shopping-list-polymer-pouchdb/commit/0b5a35dd6c6fe309df6da8e23f249eaa3da34ea3)]

Whenever a **Shopping List Item** is checked or unchecked we want to update the corresponding PouchDB document (via the **Shopping List Repository**). In `src/my-items.html` add an `on-checked-changed` handler to the `paper-checkbox` element, replacing:

```html
              <paper-checkbox data-id$="[[item._id]]" checked="[[item.checked]]"></paper-checkbox>
```

with:

```html
              <paper-checkbox data-id$="[[item._id]]" checked="[[item.checked]]" on-checked-changed="_checkedChanged"></paper-checkbox>
```

In `src/my-items.html` add the `_checkedChanged(event)` method to handle the event for checking or unchecking a **Shopping List Item** and update the corresponding document in PouchDB:

```javascript
      _checkedChanged(event) {
        let id = event.currentTarget.dataset.id;
        let checked = event.detail.value;
        let listItem = this.listOfShoppingListItems.find(item => {
          return item._id === id;
        });
        if (listItem && listItem.checked !== checked) {
          listItem = listItem.set("checked", checked);
          this.shoppingListRepository.putItem(listItem);
        }
      }
```

### Syncing Data

#### Configure a Database

##### Option 1: Apache CouchDB

[Install CouchDB 2.1](http://docs.couchdb.org/en/2.1.0/install/index.html). Instructions are available for installing CouchDB 2.1 on Unix-like systems, on Windows, on Mac OS X, on FreeBSD, and via other methods.

Configure CouchDB for a [single-node setup](http://docs.couchdb.org/en/2.1.0/install/setup.html#single-node-setup), as opposed to a cluster setup. Once you have finished setting up CouchDB, you should be able to access CouchDB at `http://127.0.0.1:5984/`. Ensure that CouchDB is running and take note of your admin username and password.

##### Option 2: IBM Cloudant

Sign up for an [IBM Bluemix](https://console.ng.bluemix.net/) account, if you do not already have one.

Once you are logged in to Bluemix, create a new Cloudant instance on the [Cloudant NoSQL DB Bluemix Catalog](https://console.ng.bluemix.net/catalog/services/cloudant-nosql-db) page. This should take you to a page representing the newly-created service instance. Click the "service credentials" link. You should have one set of service credentials listed. Click "view credentials" which should show you a JSON object containing your service credentials. Copy the value for the `url` key to your clipboard (the value will be in the form of `https://username:password@uniqueid-bluemix.cloudant.com`).

##### Option 3: Cloudant Developer Edition

Download and install [Docker](https://www.docker.com/) (version 1.9 or above is recommended). Once Docker is installed, download the [Cloudant Developer Edition](https://hub.docker.com/r/ibmcom/cloudant-developer/) from Docker Hub (this is a fairly large image, so the download may take some time):

```
$ docker pull ibmcom/cloudant-developer
```

Start the Docker container:

```
docker run --detach --volume cloudant:/srv --name cloudant-developer --publish 8080:80 --hostname cloudant.dev ibmcom/cloudant-developer
```

**Note:** Instructions are available on the [Cloudant Developer Edition](https://hub.docker.com/r/ibmcom/cloudant-developer/) for starting the container via Docker Compose.

If you want to stop the Docker container, first list the containers:

```
$ docker ps --all
CONTAINER ID        IMAGE                       COMMAND                  CREATED             STATUS              PORTS                  NAMES
1b4030e0f6b6        ibmcom/cloudant-developer   "supervisord -c /e..."   About an hour ago   Up 2 minutes        0.0.0.0:8080->80/tcp   cloudant
```

**Note:** Your output will appear different than the example above.

Find the container ID corresponding to the `ibmcom/cloudant-developer` image and run the following command to stop the container (replacing the container ID with your container ID):

```
$ docker stop 1b4030e0f6b6
1b4030e0f6b6
```

To start the container again run (replacing the container ID with your container ID):

```
$ docker start 1b4030e0f6b6
1b4030e0f6b6
```

#### Enable Live Replication with a Remote Database

[[diff](https://github.com/ibm-watson-data-lab/shopping-list-polymer-pouchdb/commit/972470077fd814895f5748cc9906df97605edc92)]

Install the [`paper-toast`](https://www.webcomponents.org/element/PolymerElements/paper-toast) element:

```
$ bower install --save PolymerElements/paper-toast#^2.0.0
```

In `src/my-app.html` add the following line to import the `paper-toast` component after `<link rel="import" href="../bower_components/paper-icon-button/paper-icon-button.html">`:

```html
<link rel="import" href="../bower_components/paper-toast/paper-toast.html">
```

In `src/my-app.html` add the the following code for the toast right before the closing `</template>` tag:

```html
    <paper-toast id="toast"></paper-toast>
```

In `src/my-app.html` declare a `remoteDb` and a `replicationHandler` property:

```javascript
          remoteDb: {
            type: Object,
            readOnly: true,
            notify: true,
            value: function() {
              // Uncomment and change parameter value to enable replication (don't forget to enable CORS)
              //return new PouchDB("http://admin:password@127.0.0.1:5984/shopping-list");
            }
          },
          replicationHandler: {
            type: Object,
            notify: false
          },
```

In `src/my-app.html` add a `ready()` method that will start bi-directional replication between the local PouchDB database and the remote database (if defined) and open the toast with text indicating that live replication with remote database has started:

```javascript
      ready() {
        super.ready();
        if (this.remoteDb) {
         this.replicationHandler = this.db.sync(this.remoteDb, {
            live: true,
            retry: true
          });
          this.$.toast.text = "Live replication with remote database started";
          this.$.toast.open();
        }
      }
```

To enable replication, uncomment the `return new PouchDB("…")` line and replace the value passed to the PouchDB constructor with the URL for your remote database. Be sure to create a database named `shopping-list` first.

If you are using a local CouchDB database (replace `admin` and `password` with the values noted in the "Configure a Database" section):

```javascript
          remoteDb: {
            type: Object,
            readOnly: true,
            notify: true,
            value: function() {
              // Uncomment and change parameter value to enable replication (don't forget to enable CORS)
              return new PouchDB("http://admin:password@127.0.0.1:5984/shopping-list");
            }
          },
```

If you are using an IBM Cloudant database (replace `username`, `password`, and `uniqueid` with the values noted in the "Configure a Database" section):

```javascript
          remoteDb: {
            type: Object,
            readOnly: true,
            notify: true,
            value: function() {
              // Uncomment and change parameter value to enable replication (don't forget to enable CORS)
              return new PouchDB("https://username:password@uniqueid-bluemix.cloudant.com/shopping-list");
            }
          },
```

If you are using a Cloudant Developer Edition database (replace `admin` and `pass` with the values noted in the "Configure a Database" section):

```javascript
          remoteDb: {
            type: Object,
            readOnly: true,
            notify: true,
            value: function() {
              // Uncomment and change parameter value to enable replication (don't forget to enable CORS)
              return new PouchDB("http://admin:pass@localhost:8080/shopping-list");
            }
          },
```


Let's take a look at our finished Shopping List app, with database replication. Start the Polymer development server:

```
$ polymer serve
info:    Files in this directory are available under the following URLs
      applications: http://127.0.0.1:8081
      reusable components: http://127.0.0.1:8081/components/polymer-starter-kit/
```

You should now be able to browse to `http://127.0.0.1:8081` in your web browser and see the Shopping List app. When you open the app, a toast should open indicating that database replication has started. Open the app in another browser window and place both app instances side-by-side. As you create **Shopping Lists**, create **Shopping List Items**, or check or uncheck **Shopping List Items** you should see the data flow between the two app instances. When you're done, close the browser tab containing the Shopping List app. Back in your terminal, use `Ctrl-C` to cancel the `polymer serve` command and return you to the command prompt.

Congratulations! You have built an Offline First Progressive Web App with Polymer and PouchDB that replicates its data with a remote database.

## Workshop

TBD

## Developer Journey

TBD
