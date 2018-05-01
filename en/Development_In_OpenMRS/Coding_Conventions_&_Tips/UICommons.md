<center><h1>UI Commons Module</h1></center>
**************************************

The OpenMRS UI Commons module provides common utilities for developing UI components for your web app including HTML/CSS along with compiled SCSS, and Angular reusable components.

## Installation

In order to install the UI Commons module, you just need to enter the command
```sh
npm i @openmrs/openmrs-contrib-uicommons
```
after you've installed and the stuff for your app.

## Adding Components

To inject _all_ of the components in the module into your application, add the following Angular code
```js
angular.module('MyAngularModule', ['openmrs-contrib-uicommons']);
```
This add everything, so if you only want somethings you might want to specify only that module. For example, if you only want to add the OpenMRS header to your app, you can add the following code to your files
**Angular**
```js
angular.module('MyAngularModule', ['openmrs-contrib-uicommons.header']);
//...
angular.module('MyAngularModule').controller('controller', controller);

function controller() {
 var vm = this;
 vm.appTitle = "My App Title";
}
```
**HTML**
```html
<html ng-app="MyAngularModule">
 <div ng-controller="controller as vm">
  <openmrs-header title="vm.appTitle"></openmrs-header>
 </div>
</html>
```
This is just the beginning, but the npm page [here](https://www.npmjs.com/package/@openmrs/openmrs-contrib-uicommons) has even more information than what is presented here.
