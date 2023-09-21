---
icon: git-branch
---
This chapter contains an in-depth view of the architecture of the system. If you don't understand everything on the first reading, don't fret! Understanding how the basic system fits together is the most important thing you need for now.

## Technical Overview 

OpenMRS is a framework built upon Java and other related frameworks. It is based on a modular architecture which consists of a core application and optional modules which provide additional functionality to the core workflows.

The key architectural components of the OpenMRS core can be depicted as follows:

![_An Overview of OpenMRS_](/assets/OpenMRS-architecture.png){ style="width:600px" }

The backbone of OpenMRS lies in its core API. The OpenMRS API has methods for all of the basic functions such as adding/updating a patient, encounter, observation, etc. Methods which enable this functionality are provided in service layer classes. 

## The Source Code Structure

In OpenMRS framework and modules, there are different levels in the code architecture. The OpenMRS source code is divided into three main segments: 

* The User Interface (presentation)
* The Service Layer
* The Data Access layer

This layering isolates various system responsibilities from one another, to improve both system development and maintenance.

### The Data Access layer

The Data Access layer is an abstraction layer from the actual data model and its changes. It uses Hibernate as the Object Relational mapping tool, and Liquibase to manage relational database changes in a database-independent way.

The relationships between our domain objects and database tables are mapped using a mixture of Hibernate annotations and XML mapping files. The data access layer is exposed to the service layer through interfaces, thereby shielding it from implementation details such as which object relational mapping tool is being used.
see [openmrs DataModel at openmrs university](https://www.youtube.com/watch?v=9mK9p0Pc9zg)

### The Service layer

The Service layer is responsible for managing the business logic of the application. It is built around the [Spring framework.](https://en.wikipedia.org/wiki/Spring_Framework) The OpenMRS service layer classes make extensive use of the Spring framework for a number of tasks including the following: 

* Spring [Aspect Oriented Programming (AOP)](https://en.wikipedia.org/wiki/Aspect-oriented_programming) is used to provide separate cross cutting functions (for example: authentication, logging).
* Spring Dependency Injection (DI) is used to provide dependencies between components.
* Spring is used to manage transactions in between service layer classes

### User Interface layer

The User Interface layer for the legacy application is built upon Spring MVC, Direct Web Remoting (DWR), JSP and JavaScript. DWR is used for AJAX functionality and it provides the mapping between our Java objects and methods to JavaScript objects and methods respectively. JQuery is used to simplify the interactions with Javascript and the browser. Spring MVC is used to provide the Model-View-Controller design pattern. Our domain objects serve as the Model. We have a mixture of controllers that subclass Spring's ```SimpleFormControllers``` and those which use Spring's ```@Controller annotation```. For the new reference application user interface, we no longer use Spring ```MVC```, ```DWR``` or ```JSP```, but heavily use **Groovy, JQuery, AngularJS**, and more.

## The Modular Architecture

At the heart of OpenMRS is a custom module framework which lets you extend and modify the default functionality of the OpenMRS core in accordance to your needs. Modules are also structured like the OpenMRS core, and consist of user interface, data access and service layers.

Some OpenMRS functionality is pulled out into modules instead of being written into the core application. This allows users to upgrade the content in those modules without having to wait for the next OpenMRS release. Currently, the only core module used in OpenMRS is the Logic Module. 

## Associated Frameworks and Technology Stacks

### Hibernate

[Hibernate](https://en.wikipedia.org/wiki/Hibernate_(framework)) is the object-relational mapping library used by OpenMRS. It allows users to describe the relationship between database tables and domain objects using xml configuration files or Java annotations.

Hibernate is also useful in managing dependencies between classes. As an example, the concept domain in the data model consists of tables named concept, concept_answer, concept_set and concept_name. It would be very difficult to keep up with where to store each part of the concept object and the relations between them if a user decides to update each table individually. However, using Hibernate, developers only need to concern themselves with the Concept object, and not the tables behind that object. The ```concept.hbm.xml``` mapping file does the work of knowing that the Concept object contains a collection of ```ConceptSet objects```, a collection of ```ConceptName objects```, etc.

However, also note that Hibernate enforces lazy loading - it will not load all associated objects until they are needed. For this reason, you must either ```fetch/save/manipulate``` your object in the same session (between one open/closeSession) or you must hydrate all object collections in the object by calling the **getters** (getConceptAnswers, getConceptNames, getSynonyms, etc).

### Spring MVC

OpenMRS strongly subscribes to the [Model-View-Controller](https://en.wikipedia.org/wiki/Model–view–controller) pattern. Most controllers included in the OpenMRS core will be ```SimpleFormControllers``` and be placed in the ```org.openmrs.web.controller package```. However, some controllers have been rewritten to use Spring 2.5+ annotations, and we recommend that you use these in the future. The model is set up in the controller's formBackingObject, and processed/saved in the processFormSubmission and onSubmit methods. The ```jsp``` views are placed in ```/web/WEB-INF/view```.

Furthermore, not all files served by the webapp are run through Spring. The ```/web/WEB-INF/web.xml``` file maps certain web page extensions to the SpringController. All ```*.form```, ```*.htm```, and *```.list``` pages are mapped. The SpringController then uses the mappings in the ```openmrs-servlet.xml``` file to know which pages are mapping to which Controller.

There are no ```jsp``` pages that are accessed directly. If a page's url is ```/admin/patients/index.htm```, the jsp will actually reside in ```/web/WEB-INF/view/admin/patients/index.jsp```. This is necessary so that we can do the redirect with the SpringController. Because the file being accessed ends with ```.htm```, the SpringController is invoked by the web server. When the SpringController sees the url, it simply replaces ```.htm``` with ```.jsp``` and looks for the file in ```/web/WEB-INF/view/``` according to the jspViewResolver bean in ```openmrs-servlet.xml```. If the page being accessed was patient.form, the mapping in the urlMapping bean would have told spring to use the PatientFormController and the ```patientForm.jsp``` file. 

### Authentication and Authorization

OpenMRS has a very granulated permissions system. Every action is associated with a Privilege, which in turn can be grouped into Roles. Examples of such privileges are "Add Patient", "Update Patient", "Delete Patient", "Add Concept", "Update Concept", and more. A Role can also point to a list of inherited roles. The role inherits all privileges from that inherited role. In this way, hierarchies of roles are possible. A User contains only a collection of Roles, not Privileges. These privileges are enforced in the service layer using AOP annotations. In a way, this
also enssures Confidentiality of patients' Data by putting restrictions on the data Access. 

### Build Management

OpenMRS uses **Apache Maven** for build management of the OpenMRS core and modules. 

All information regarding the module being built, its dependencies on other external modules and components, the build order, directories, and required plug-ins are stored in the modules' ```pom.xml``` file. 

Following release, these build artifacts are uploaded and maintained in a maven repository manager. A maven repository manager is used for this purpose due to a number of advantages that it provides. These advantages include:

* Faster and more reliable builds
* Improved collaboration
* Component usage visibility
* Enforcement of component standards 
* The Maven Repository used by OpenMRS is SonaType Nexus, which can be accessed at http://mavenrepo.openmrs.org/nexus/. 
* Artifacts maintained in the OpenMRS repository are:

## Releases

* Maven built releases (1.8.0 and later)
* Ant built releases (1.5.0 up to 1.7.X)

#### Snapshots

* Maven development versions

#### Modules

* Module releases

#### 3rd Party Artifacts

* Libraries not found in other Maven repositories (HAPI)
* Modified libraries (DWR, Hibernate, Liquibase, Simple XML)
* Custom Maven plugins (OpenMRS omod plugin)

## Summary

As you read the next section, keep in mind the important parts from this chapter:

* OpenMRS consists of a core system, with a modular architecture to extend its functionality.
* There are three main layers to the system: User Interface (Presentation), Service Layer and Data Access Layer.
* OpenMRS makes extensive use of a number of frameworks including Spring and Hibernate.
* We use Apache Maven for build management, JIRA for issue management and Github for version control.
* Authentication/Authorisation is ensured by grouping different priviledges into roles which then are assigned to
 defined users and in turn it ensures the confidentiality of patients data and security of the system.
