<center><h1>Setting Up </h1></center>
**********
<center><img src="/assets/Get Set Up.jpg"></center>

Now that we know all of the background and support information, let's set up a basic install of OpenMRS on your system!

## Java Version Check

Before we get started, check that you have the **Java Development Kit (JDK)** installed. Open up a console/terminal and enter:
``` shell
javac -version 
```
You should see output like this:

```javac 1.8.0_112```

Note: Java 1.6 or above is required to run OpenMRS 1.x. OpenMRS Platform 2.0+ (including Reference Application 2.5+) require Java 1.8. If you plan to use the **OpenMRS Software Development Kit** (SDK) installation, Java 1.7 or higher is required. (See below for more information on install options.)

If you do not have similar output to what is shown above, it means that you are missing the JDK, so go ahead and install it. Below is a list of external tutorials for installation, based on your platform.

 
| Platform | Tutorial Link |
| -- | -- |
|  Windows  |  http://www3.ntu.edu.sg/home/ehchua/programming/howto/JDK_Howto.html#zz-1.   |
| OS X |http://www3.ntu.edu.sg/home/ehchua/programming/howto/JDK_Howto.html#zz-2. |
| Linux | http://www.webupd8.org/2011/09/how-to-install-oracle-java-7-jdk-in.html |  

## Choosing An Approach

There are several options for installation, so read through each one and decide which is best for you.

* If you're getting started, we highly recommend using the **OpenMRS SDK**, which comes with a complete environment for using OpenMRS. This means that you won't need to have much else on your system installed other than Java. This is the easiest and quickest path to getting OpenMRS running so that you can start developing modules.

* The **OpenMRS Standalone Application** bundles OpenMRS with Tomcat and MySQL which will be ready to run by simply running the standalone JAR file. The Standalone does not bundle Maven, so you'll need to run and install the [Maven](https://maven.apache.org/) Module Archetype yourself to begin creating new modules. If you're planning to work on a pre-existing module, rather than creating a new module, then the Standalone may be a good option for you.

* If you want to develop code for the OpenMRS core application, you should use a manual install. The SDK and Standalone only include binary versions of the code, so getting your own development environment set up is necessary if you want to be a core developer.


## OpenMRS SDK Installation

### Set Up Maven

Ensure that you have Maven installed and configured to support building OpenMRS software. You can use the instructions at [Maven in Five Minutes ](http://maven.apache.org/guides/getting-started/maven-in-five-minutes.html)

### Download and Install

It's time to install the SDK. Open up a terminal window or command line console and type the following (for the most recent instructions on using the SDK, see http://om.rs/sdk:

```mvn org.openmrs.maven.plugins:openmrs-sdk-maven-plugin:setup-sdk```

Wait for the installation to finish then check to see if the SDK is working. To do so, open up a terminal window or command line console and type the following: 

```mvn openmrs-sdk:help```

The output it gives, should be similar of that below:
```
OpenMRS SDK 3.5.0 
For more info, see SDK documentation:
https://wiki.openmrs.org/display/docs/OpenMRS+SDK
...
```

If that is the case, you have successfully installed the OpenMRS SDK!

If you're having trouble, take a look at the [SDK documenation](https://wiki.openmrs.org/display/docs/OpenMRS+SDK) on the OpenMRS Wiki for more assistance, or join the **#OpenMRS IRC** channel for help. 


## Create OpenMRS Instance

You need to start from creating a new OpenMRS server. Run the following command and follow the wizard:

```
mvn openmrs-sdk:setup
```
* Choose ```Distribution``` if you want to setup the 'Reference Application' or any other distribution. 
* Choose ```Platform``` to setup the OpenMRS Platform without any modules to start with.


## Create OpenMRS Module

You can customize and extend OpenMRS by creating your own module. You can create a module by running:
```
mvn openmrs-sdk:create-project
```
Choose ```Platform module``` or ```Reference Application module``` depending on what kind of server you setup in the previous step.

## Run OpenMRS Locally

Within the module that you just created, you can choose to run OpenMRS to test the module you are working on. This command will build the module and launch the web server. 
```
mvn clean install openmrs-sdk:run -DserverId=your_server_id_here
```
Replace ```your_server_id_here``` with the id you used when setting up the server.

OpenMRS is now fully running on your computer at ```http://localhost:8080/openmrs``` and can be tested. Log in with the following credentials: 

**User: admin, Password: Admin123 **
 
### Troubleshooting

Detailed documentation and troubleshooting help can be found on the OpenMRS Wiki [here](https://wiki.openmrs.org/display/docs/OpenMRS+SDK) or try IRC for a great place to ask for help!


## Standalone Setup

OpenMRS Standalone is a great way to evaluate and explore OpenMRS capabilities. It may also be useful for small-scale production environments. The best place to learn about the standalone in full is on the OpenMRS Wiki at [OMRS Standalone docs]( https://wiki.openmrs.org/display/docs/OpenMRS+Standalone) but we'll go through the set up here too.

**Step 1:** Download OpenMRS Standalone from [OpenMRS Download page](http://openmrs.org/download/) and unzip the downloaded file.

**Step 2:** Execute the JAR file in that folder. You can do this by typing the following in the terminal/command line:

```java -jar openmrs-standalone.jar```

You can add the ```-commandline``` switch to make it run in full command-line mode:

```java -jar openmrs-standalone.jar -commandline```

Be careful not to delete or rename folders after decompressing the standalone package! They are used by the standalone JAR file and need to be in their exact locations for things to work correctly.

**Step 3:** OpenMRS will configure itself the first time it is run. The initial setup installer will offer an option to install a demo concept dictionary, the demo concepts plus demo patient data, or no demo data. 

**Step 4:** After running the standalone jar, it will take you to the OpenMRS log in web page where you can log in with the following default username and password:

* Username: **admin**
* Password: **Admin123**
 
The MySQL database has these credentials by default:

* MySQL username: **openmrs**
* MySQL password: Randomly generated during initial startup. 

Look in the ```openmrs-runtime.properties``` file for the value of ```connection.password.```
 

You now have a local copy of OpenMRS running with both an embedded database and a web server! At any time, you can upgrade the standalone version. Check out the wiki for details on [Upgrading OpenMRS](https://wiki.openmrs.org/display/docs/Upgrading+OpenMRS)


## Manual Installation


#### Set Up MySQL

You must have a MySQL database set up for OpenMRS to be installed successfully. To point your OpenMRS project to the database, should either know your MySQL root password, or have a database schema pre-configured and ready with a username and password to provide during the OpenMRS setup. More information about installing and setting up MySQL is available at [Getting Started with MySQL](http://dev.mysql.com/usingmysql/get_started.html)


#### Set Up Maven

Ensure that you have Maven installed and configured to support building OpenMRS software. You can use the instructions at [Maven in five Minutes]( http://maven.apache.org/guides/getting-started/maven-in-five-minutes.html)

#### Set Up Git

Ensure that you have installed and configured Git for source code management. You can use one of the following relevant instruction pages:

* [Atlassian Git Tutorial](https://atlassian.com/git/tutorials/)
* [Getting Started with Git](http://git-scm.com/book/en/Getting-Started-Installing-Git)
* [Setting Up Git on Mac](http://help.github.com/mac-set-up-git/)
* [Setting Up Git on Windows](http://help.github.com/win-set-up-git/)
* [Setting Up Git on Linux](http://help.github.com/linux-set-up-git/)

OpenMRS developers generally agree that the command line is the best way to interact with GIT, and we recommend that you set up your Git instance to be able to do so. 

#### Get The Core Source Code

You must clone the openmrs-core repository on GitHub using your Git client in order to start working on the project. In a directory that you keep your code in, run the following:
```shell
git clone https://github.com/openmrs/openmrs-core.git 
cd openmrs-core 
```
You are now in the main working source code directory for OpenMRS.

More detailed steps are necessary if you are checking out OpenMRS code to fix a particular ticket. Please refer to Git instructions listed under the Development process on how to check out the required source code. 


#### Compiling Your Code

Compile the source code to be able to run it. First make sure that you are in the top-level openmrs-core directory, then run:

```mvn clean install ```

This will take a few minutes, while it downloads dependencies and builds OpenMRS. Make sure you are connected to the Internet so Maven can download the necessary dependencies from our repositories.

##### Start The OpenMRS Webapp

To run the code, you have to start the webapp. The OpenMRS source code contains a dependency to the Jetty server, so you can start the application by running a simple command. to do so, complete the following steps:

```
  cd webapp 
  mvn jetty:run
```

Now you may access OpenMRS using the url ```http://localhost:8080/openmrs```. This should let you run a wizard which will guide you through setting up your database. The Wizard will allow you to configure you instance in a number of ways, and offers multiple options to help you point to what database you want to use, and what data you wish to include by default.


> **NOTE:** If you run into issues with Out of Memory exceptions from Java, try running:
```
export MAVEN_OPTS="-Xmx1024m -Xms1024m -XX:PermSize=256m -XX:MaxPermSize=512m"
 ```

Then run Jetty again using the command above. This should increase the effective memory of the running Java Virtual Machine, thereby preventing the re-occurrence of this error.

## Conclusion

You've now installed OpenMRS on your computer. You're ready to learn about developing.
