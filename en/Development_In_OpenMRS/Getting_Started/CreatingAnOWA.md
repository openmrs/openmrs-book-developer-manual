<center><h1>Creating Your First OWA</h1></center>
************************************

Before you get started, please consult the [Starting Development](StartingDevelopment.md) page if you have not already to make sure that a module is right for your type of project.

## Pre-development issues

While you may be ready to begin development right away, it is important to take a step back and plan out your work. Will this be a application which may be useful to all OpenMRS implementers, or implementers of a specific clinic only? This factor may decide where the completed application will be hosted, and what kind of requirements/standards you need to maintain.

It is best not to begin development until you have discussed your design plans with other community developers, and made sure that your plans meet our requirements. Remember that a solid development plan is behind every successful piece of software, and will make your life and the lives of other OpenMRS developers much easier as your project grows.

## Installation

Before you begin developing your app, you will need to make sure that you have several important pieces of software installed. You will need:
 * Node.js 4.x+
 * Maven 3.x+
 * Java 1.7+

You can check to see if these are already installed on your system by running the following commands:
 * `node --version`
 * `mvn --version`
 * `javac -version`

If any of these result in a command not found or a version is lower than it should be, you will need to install the respective software. For instructions on how to install Java and Maven, please see the [Get Setup](GetSetUp.md) page. For instructions on how to install Node.js, please check out [these instructions](https://nodejs.org/en/download/package-manager/).

You will also need to install the OpenMRS SDK in order to create a test environment where you can experiment with your new app. There is a guide on how to do this [here](GetSetUp.md). Please skip the section on creating a new module, as OpenMRS has moved from using Java-based modules to using Open Web Apps (OWAs), which you will learn about here. Next, you will want to verify that the Open Web Apps module is installed (typically, it comes with OpenMRS). You can find information on this [here](https://wiki.openmrs.org/display/docs/Open+Web+Apps+Module#OpenWebAppsModule-Downloads).

Now that you have fulfilled these prerequisites, we can finally begin the process of creating your new OWA. OpenMRS has created a generator that will create a scaffold for your new addon. You will need to install Yeoman using `npm install -g yo`. You may read more about Yeoman [here](http://yeoman.io/learning/). Next, you can install the generator for OpenMRS OWAs by typing `npm install -g generator-openmrs-owa`. After doing this, create a directory where you would like to store your project and change into it. Once you have done this, run `yo openmrs-owa` to create a scaffold for your app.

At this point, the generator will ask you questions about what specific type of app you would like to create. Give your app an appropriate name and description in order to make it clearer for other people who may eventually use it. You may select whatever option you like as the library to include, but this guide will assume you have selected AngularJS. You should also be sure to select SDK as the type of local server you are running.

## Development

You have now successfully created a very basic app to which you will begin adding functionality. This section will teach you the basics of building, deploying, and configuring your app. You will also learn how to access data from the server through the REST API.

### Packaging and deploying

Building and deploying the application is relatively simple. First, open up `config.json` in the application directory and change `LOCAL_OWA_FOLDER` to point to the `owa` folder within your server installation. Typically, this is in a location that looks similar to `/home/{username}/openmrs/{server_name}/owa`. Next, type `npm run build:deploy` within the application directory. This command will automatically build and install your application on your local server. You will need to rerun this command whenever you make changes to your application. Open a web browser and navigate to the home page for your OpenMRS server (the default is usually `localhost:8080/openmrs`, but this will depend on the options you chose when creating the server). Click on System Adminstration, then Advanced Adminstration, and find "Manage Apps" under the Open Web Apps Module heading. Verify that your application appears there, and that clicking it correctly links to your application.

### Configuring your OWA

Now that you have created an OWA, you probably want to configure it to your own specifications. It would be far more convenient for your users if they were able to access your application from the OpenMRS home page. In order to do so, you will want to go to System Adminstration > Manage Apps > Add App Definition and add a definition such as the following: 
```
{
    "id": "replace.with.something.unique",
    "description": "replace with your description",
    "order": 0,
    "extensions": [
        {
            "id": "replace.with.something.unique.homepageLink",
            "extensionPointId": "org.openmrs.referenceapplication.homepageLink",
            "type": "link",
            "label": "Replace with name of your App",
            "url": "owa/managerdashboard/index.html",
            "icon": "icon-bar-chart",
            "requiredPrivilege": "Replace with a privilege name, or else remove"
        }
    ]
}
```

You can find a list of icons [here](https://demo.openmrs.org/openmrs/uicommons/icons.page). Be sure to modify the different fields in the definition to whatever you would like to have displayed. In particular, the first `id` field must match whatever you type into the "App ID" box. The `id` field within the `extensions` list must have the same text, but end with ".homepageLink". The URL will also need to changed, and will typically be something like `owa/{your app name}/index.html`. The easiest way to verify this is to navigate to the page that you want to link to, and use that URL. Finally, the `order` parameter determines where in the menu it will show up, with 0 being the first, 1 being the second, etc. Some more information on adding the definition can be found [here](https://wiki.openmrs.org/display/docs/Adding+OWA+Icon+to+the+Reference+Application+Homepage).

### Using the Rest API
An easy way to use the Rest API with your OWA is to use the OpenMRS Reference Application UI Library. First you need to inject its code into your Angular module. You can do this with the following:
```
import uicommons from 'openmrs-contrib-uicommons';

angular.module('YourAngularModule',['openmrs-contrib-uicommons.header']).controller('controller', Controller);

```
Then in your controller you can use the Rest API like this:
```
controller.$inject = ['openmrsRest']
function controller(openmrsRest) {
   var vm = this;
	vm.items;
	vm.resourceName = "class" //the resource you want to request
	vm.params = {includeAll: true} //the parameters to your request
	openmrsRest.listFull(vm.resourceName, vm.params).then(function(response)(
	    vm.items = response.results; //store response in variable
    ));   
}


```
The functions that you can use with the OpenMRS Rest API are as follows: `list`, `listFull`, `listRef`, `get`, `getFull`, `getRef`, `create`, `update`, `remove`, `retire`, `unretire`, `purge`.

For more information on the Rest API refer to the OpenMRS Rest API docs found [here](https://psbrandt.io/openmrs-contrib-apidocs/).

## Final steps

Now that your application is completed, it is the perfect time to go ahead and test it. Remember that OpenMRS expects all code to be unit tested (if possible) as this makes it more dependable and less prone to errors. Test the app yourself to make sure that there are no obvious mistakes before asking a target end user to try it out. The end user's feedback may result in further design discussions or reviews. Once these have been completed, the application can be implemented at the clinic, and also made available publicly. Refer to the guidelines specified in the 'Development Process' chapter to find out the best way to do this.

Once your application is released, you may think that your work is over. However, there is no such thing. As health systems, requirements, and technology change, so must the software.This makes medical informatics a viable career option, but does not mean you are responsible for maintaining `Hello World` for the rest of its life with OpenMRS.

