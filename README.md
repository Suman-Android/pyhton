Startup App
==================


**This** is a fully functional Android app built entirely with Kotlin and Jetpack Compose. It follows Android design and development best practices and is intended to be a used as a base arctictecture for any android application.


# Architecture Overview

The app architecture has two layers: a [data layer] and a [UI layer].

The architecture follows a reactive programming model with [unidirectional data flow]. With the data layer at the bottom, the key concepts are:

*   Higher layers react to changes in lower layers.
*   Events flow down.
*   Data flows up.

The data flow is achieved using streams, implemented using [Kotlin Flows].

### Example: Displaying Products on the Product screen

When the app is first run it will gives you two option "start fragment flow" and "start compose flow". When you clicked either of the flow then the next product screen will attempt to load a list of product resources from a remote server. Once loaded, these are shown to the user.

The following diagram shows the events which occur and how data flows from the relevant objects to achieve this.


# Modularization

Modularization is the practice of breaking the concept of a monolithic, one-module codebase into loosely coupled, self contained modules.

This **Startup** app has been fully modularized.

## Types of modules

This app contains the following types of modules:

*   The `app` module - contains app level and scaffolding classes that bind the rest of the codebase, such as `MainActivity`, `App` and app-level controlled navigation. A good example of this is the navigation setup through `AppNavHost`. The `app` module depends on all `feature` modules and required `core` modules.

* `feature:` modules - feature specific modules which are scoped to handle a single responsibility in the app. These modules can be reused by any app. If a class is needed only by one `feature` module, it should remain within that module. If not, it should be extracted into an appropriate `core` module. A `feature` module should have no dependencies on other feature modules. They only depend on the `core` modules that they require.

* `core:` modules - common library modules containing auxiliary code and specific dependencies that need to be shared between other modules in the app. These modules can depend on other core modules, but they shouldn’t depend on feature nor app modules.

<table>
  <tr>
   <td><strong>Name</strong>
   </td>
   <td><strong>Responsibilities</strong>
   </td>
   <td><strong>Key classes and good examples</strong>
   </td>
  </tr>
  <tr>
   <td><code>app</code>
   </td>
   <td>Brings everything together required for the app to function correctly. This includes UI scaffolding and navigation. 
   </td>
   <td><code>App, MainActivity</code><br>
   App-level controlled navigation via <code>AppNavHost, TopLevelNavigation</code>
   </td>
  </tr>
  <tr>
   <td><code>feature:Product,</code><br>
   ...
   </td>
   <td>Functionality associated with a specific feature or user journey. Typically contains UI components and ViewModels which read data from other modules.<br>
   Examples include:<br>
   <ul>
      <li>feature:product displays information about a products on the Product Screen.</li>
      </ul>
   </td>
   <td><code>ProductScreen</code><br>
   <code>ProuductViewModel</code>
   </td>
  </tr>
  <tr>
   <td><code>core:data</code>
   </td>
   <td>Fetching app data from multiple sources, shared by different features.
   </td>
   <td><code>ProductDataRepository</code><br>
   </td>
  </tr>
   <td><code>core:common</code>
   </td>
   <td>Common classes shared between modules.
   </td>
   <td><code>AppDispatchers</code><br>
   <code>Result</code>
   </td>
  </tr>
  <tr>
   <td><code>core:network</code>
   </td>
   <td>Making network requests and handling responses from a remote data source.
   </td>
   <td><code>RetrofitNetworkApi</code>
   </td>
  </tr>
   <td><code>core:datastore</code>
   </td>
   <td>Storing persistent data using DataStore.
   </td>
   <td><code>AppPreferencesDataSource</code><br>
   <code>ProductPreferenceSerializer</code>
   </td>
  </tr>
  <tr>
   <td><code>core:model</code>
   </td>
   <td>Model classes used throughout the app.
   </td>
   <td><code>Product</code>
   </td>
  </tr>
</table>



