---
title: Creating Your First Module
---

## Amani Clinic Case Study

To put this book in perspective, we'll walk through a fictional scenario that reflects the real world process of identifying the need for, designing, and building a module. Maintaining a modular architecture allows developers to add and remove special functionality into OpenMRS without having to modify the core project.

**Lets get started!**

## Overview

Let's suppose there is an established health clinic called **Amani Clinic** in East Africa with a few staff members who are experienced in ICT and medical informatics. They are very talented and very busy. You find and read a ticket they created when they realized functionality for adding, editing, saving, and listing of departments would be helpful to their implementation. For the purposes of this task, we will define a department as a hospital ward designed to perform a specific purpose.

Someone has left a comment ***"This would be a good module project!"* **on the ticket. You would love a new project to work on and happen to have an interest in the larger issue of "departments" as they relate to health informatics, so you are interested in taking up this task.

You send an email to Mrs. Zuma, the clinic's lead informatics person and ticket requester, expressing your interest and asking for some clarification about how a user would interact with the proposed Departments module. It is a good idea to touch base with the ticket requesters or would-be users before starting a project whose scope is likely more work and background than a straightforward bug-fix. While you wait for a reply (you might not know where in the world Mrs. Zuma lives), you decide to catch up on some emails of your own. You subscribed to the developers' mailing list a few days ago because you want to stay informed about what other people are working on and what issues they run into. You are excited about learning and watch a few OpenMRS University recordings too.

Mrs. Zuma is enthusiastic about you building this module for their clinic and potentially many others. She invites you to keep in touch as you go along. You have already worked your way through the Getting Started chapter, so you get to work using the OpenMRS SDK to start building your module.

You officially begin work on the module by clicking on the button to "claim" the ticket on the OpenMRS JIRA. 

## Pre-development issues

While you may be ready to begin development right away, it is important to take a step back and plan out your work. Will this be a module which may be useful to all OpenMRS implementers, or implementers of the Amani clinic only? This factor may decide where the completed module will be hosted, and what kind of requirements/standards you need to maintain.

It is best not to begin development until you have discussed your design plans with other community developers, and made sure that your plans meet our requirements. 

## Creating A Basic Module

The OpenMRS SDK, as explained in the Technology Chapter, allows you to get started with a basic module in a few minutes. The `mvn openmrs-sdk:create-project` command helps you execute the maven archetype, creating a module directory with a framework of all the necessary module files by prompting you for specific information.

However, in order to execute this command, we assume that you're using JDK 1.7. No other pre-requisites are necessary.
To complete the `mvn openmrs-sdk:create-project` workflow, you will be prompted to enter the following data:

* **`What kind of project would you like to create?:`** You may choose to create a platform module, which can be run on any server or an OpenMRS Reference Application module, which needs to be run on a server with the OpenMRS Reference Application distribution installed. For this example, choose type `1`.
* Next, you will be prompted for `module id`, `module name`, `description`, `groupId`, `initial version` and the lowest version of `platform support`. For this example, you can stick with the default provided values.


For more info, see [module conventions](https://wiki.openmrs.org/display/docs/Module+Conventions).

N.B. in the Module Activation class, The SDK will implement the  ModuleActivator interface. 
For more about the Module Activator class,see [Module Activator](https://wiki.openmrs.org/display/docs/Module+Activator)


## Basic Module Structure

The `mvn openmrs-sdk:create-project` command creates the basic module structure and components that it requires for use. Below is a detailed overview of these components, their structure and how they can be used.

* **api** - non-web-specific 'maven module' project
   * **src** 
       * **main** - Java files in the module that are not web-specific.  These will be compiled into a distributable mymodule.jar
   * **target** - folder built at runtime that will contain the distributable jar file for the module
* **omod**
   * **src**
     * **main**
        * **java** - web specific java files like controllers, servlets, and filters 
        * **resources** - 
           * [config.xml](https://wiki.openmrs.org/display/docs/Module+Config+File)
           * [*.hbm.xml files](https://wiki.openmrs.org/display/docs/Module+Hibernate+Mapping+Files)
           * [liquibase.xml](https://wiki.openmrs.org/display/docs/Module+liquibase+File) (or the old [sqldiff.xml](https://wiki.openmrs.org/display/docs/Module+sqldiff+File) )
           * [messages_*.properties files](https://wiki.openmrs.org/display/docs/Module+messages.properties+Files)
           * [modulesApplicationContext.xml](https://wiki.openmrs.org/display/docs/Module+Application+Context+File)
           * log4j.xml - optional file to control logging in your module
      * **webapp** - jsp and html files included in the ```omod```
         * [portlets](https://wiki.openmrs.org/display/docs/Module+Portlets) -
         * [resources](https://wiki.openmrs.org/display/docs/Module+Resources) - image, js, and css files that your jsp files reference
  * **target** - Contains the distributable omod file
* **pom.xml** - Maven build file.  Delegates to `pom.xml` files in the omod and api project


## Compiling Your Module 

The basic module structure comes ready to be compiled and installed onto the OpenMRS framework. To do this, navigate into the `basicexample` (your module id) directory and execute the following command:

 `mvn clean install`

This creates a `jar` file, and then package that jar into a `omod` file. The omod file is what you need to care about. It will be named `basicexample-1.0.0-SNAPSHOT.omod`, and located under the `basicexample/omod/target/` folder. The omod file is the module binary, which you will install into your OpenMRS application.

Executing the maven clean install command also runs any unit tests. If you want to skip unit tests, use the following command instead:

`mvn clean install -Dmaven.test.skip=true`


## Try Out Your Module

To install your module go to the Admin interface of OpenMRS.

* Go to `http://localhost:8080/openmrs/admin/`. 
* On the right side, is a **Modules section**. Click the **Manage Modules** link.
* Near the top, you will see an Add or Upgrade Module button, click it.
* Under the **Add Module** heading, click the **Browse...** button.
* In the file browser, select your `omod` file from `basicexample/omod/target/basicexample-1.0.0-SNAPSHOT.omod`
* **Click Upload**.


You should now see your module under the Manage Modules heading.
Another alternative would be to drop the compiled omod file into the `~/.OpenMRS/modules` folder.  (Where `~/.OpenMRS` is assumed to be the Application Data Directory that the running openmrs is currently using.)  After putting the file in there simply restart OpenMRS and the module will be loaded and started.

When you navigate back to the main Administration page, you should see your module listed with a Basic Example Module heading, and a single sub-option of Manage module.


## Customize Your Module 

Now that you have a basic module running, you want to add your own features which would allow it to `Hello World`, or what ever you want! Where to start?


### Add a New Field To Your Data Model

Let's assume that your hello world task involves adding a new field titled '`name`' to your data model. 

In`department/api/src/main/java/org/openmrs/module/department/Department.java`, add new fields called name and description along with appropriate getters and setters for them. The file should now look as follows: 
```java
public class Department extends BaseOpenmrsObject implements Serializable {
	private static final long serialVersionUID = 1L;
	private Integer departmentId;
	private String name;
	private String description;
	public Integer getDepartmentId() {
		return departmentId;
	}
	public void setDepartmentId(Integer departmentId) {
		this.departmentId = departmentId;
	}
	@Override
	public Integer getId() {
		return getDepartmentId();
	}
	@Override
	public void setId(Integer id) {
		setDepartmentId(id);
	}
	public String getName() {
		return name;
	}
	public void setName(String name) {
		this.name = name;
	}
	public String getDescription() {
		return description;
	}
	public void setDescription(String description) {
		this.description = description;
	}
}
``` 


#### Update Hibernate ORM File to Work With Your New Field

In `department/api/src/main/resources/Department.hbm.xml`, uncomment the central block of code add new properties as shown below anywhere in the file. This lets Hibernate knows about the name and description fields you just created. Your file should look like the following:
```xml
 <?xml version="1.0"?>
<!DOCTYPE hibernate-mapping PUBLIC
    "-//Hibernate/Hibernate Mapping DTD 3.0//EN"
    "http://hibernate.sourceforge.net/hibernate-mapping-3.0.dtd" >
<hibernate-mapping package="org.openmrs.module.department">
	<class name="Department"
		table="${project.parent.artifactId}_Department">
		<id name="departmentId" type="int" column="department_id" unsaved-value="0">
			<generator class="native" />
		</id>
		<discriminator column="department_id" insert="false" />
		<property name="uuid" type="java.lang.String" column="uuid" length="38" unique="true" />
		<property name="name" type="java.lang.String" column="name" length="255" unique="true" />
		<property name="description" type="java.lang.String" column="description" length="255" />	
	</class>
</hibernate-mapping>
```

To reflect this change in the existing database, add an appropriate change set into the `department/api/src/main/resources/liquibase.xml`. This is the code that actually changes the database for your project to reflect your name field. A sample changeset will generally look like this:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<databaseChangeLog xmlns="http://www.liquibase.org/xml/ns/dbchangelog/1.9"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://www.liquibase.org/xml/ns/dbchangelog/1.9
                  http://www.liquibase.org/xml/ns/dbchangelog/dbchangelog-1.9.xsd">
    <!--
        See http://www.liquibase.org/manual/home#available_database_refactorings
        for a list of supported elements and attributes
    -->
    <changeSet author="yourname" id="20131010-1">
        <comment>Create the department table</comment>
        <createTable tableName="department_department">
            <column autoIncrement="true" name="department_id" type="int">
                <constraints primaryKey="true" nullable="false" />
            </column>
            <column name="name" type="varchar(255)" />
            <column name="description" type="varchar(255)" />
            <column name="uuid" type="char(38)" />
        </createTable>
    </changeSet>
</databaseChangeLog>
```

#### Modify DAO And Service Layer Classes Support End to End Interactions

The Module Maven Archetype or SDK option to add a service layer gives the module four files that make up the service layer: 

```
* DAO (data access interface)
* HibernateDAO
* Service and 
* ServiceImpl. 
```

The `HibernateDAO` is home to the `sessionFactory`, which actually connects to the database. The ```ServiceImpl``` will instantiate a DAO and then the module controller is free to instantiate a Service. Here is the code you will add to each file:

**DAO:**
```java
/**
 * Database methods for {@link DepartmentService}.
 */
public interface DepartmentDAO {
	/**
	 * @see org.openmrs.module.department.api.DepartmentService#getAllDepartments()
	 */
	List<Department> getAllDepartments();
	/**
	 * @see org.openmrs.module.department.api.DepartmentService#getDepartment(java.lang.Integer)
	 */
	Department getDepartment(Integer departmentId);
	/**
	 * @see org.openmrs.module.department.api.DepartmentService#saveDepartment(org.openmrs.module.department.Department)
	 */
	Department saveDepartment(Department department);
	/**
	 * @see org.openmrs.module.department.api.DepartmentService#purgeDepartment(org.openmrs.module.department.Department)
	 */
	void purgeDepartment(Department department);
}
```

**HibernateDAO:**
```java
/**
 * The default implementation of {@link DepartmentDAO}.
 */
public class HibernateDepartmentDAO implements DepartmentDAO {
	protected final Log log = LogFactory.getLog(this.getClass());
	private SessionFactory sessionFactory;
	/**
	 * @param sessionFactory the sessionFactory to set
	 */
	public void setSessionFactory(SessionFactory sessionFactory) {
		this.sessionFactory = sessionFactory;
	}
	/**
	 * @return the sessionFactory
	 */
	public SessionFactory getSessionFactory() {
		return sessionFactory;
	}
	/**
	 * @see org.openmrs.module.department.api.db.DepartmentDAO#getAllDepartments()
	 */
	@Override
	public List<Department> getAllDepartments() {
		return sessionFactory.getCurrentSession().createCriteria(Department.class).list();
	}
	/**
	 * @see org.openmrs.module.department.api.DepartmentService#getDepartment(java.lang.Integer)
	 */
	@Override
	public Department getDepartment(Integer departmentId) {
		return (Department) sessionFactory.getCurrentSession().get(Department.class, departmentId);
	}
	/**
	 * @see org.openmrs.module.department.api.db.DepartmentDAO#saveDepartment(org.openmrs.module.department.Department)
	 */
	@Override
	public Department saveDepartment(Department department) {
		sessionFactory.getCurrentSession().save(department);
		return department;
	}
	/**
	 * @see org.openmrs.module.department.api.db.DepartmentDAO#purgeDepartment(org.openmrs.module.department.Department)
	 */
	@Override
	public void purgeDepartment(Department department) {
		sessionFactory.getCurrentSession().delete(department);
	}
}
```

**Service:**

```java
/**
 * The service for managing departments.
 */
@Transactional
public interface DepartmentService extends OpenmrsService {
	/**
	 * Gets a list of departments.
	 *
	 * @return the department list.
	 */
	@Transactional(readOnly = true)
	List<Department> getAllDepartments();
	/**
	 * Gets a department for a given id.
	 *
	 * @param id the department id
	 * @return the department with the given id
	 */
	@Transactional(readOnly = true)
	Department getDepartment(Integer departmentId);
	/**
	 * Saves a new or existing department.
	 *
	 * @param department the department to save.
	 * @return the saved department.
	 */
	Department saveDepartment(Department department);
	/**
	 * Deletes a department from the database.
	 *
	 * @param department the department to delete.
	 */
	void purgeDepartment(Department department);
}
```

**ServiceImpl:**

```java
/**
 * It is a default implementation of {@link DepartmentService}.
 */
public class DepartmentServiceImpl extends BaseOpenmrsService implements DepartmentService {
	protected final Log log = LogFactory.getLog(this.getClass());
	private DepartmentDAO dao;
	/**
	 * @param dao the dao to set
	 */
	public void setDao(DepartmentDAO dao) {
		this.dao = dao;
	}
	/**
	 * @return the dao
	 */
	public DepartmentDAO getDao() {
		return dao;
	}
	/**
	 * @see org.openmrs.module.department.api.DepartmentService#getAllDepartments()
	 */
	@Override
	public List<Department> getAllDepartments() {
		return dao.getAllDepartments();
	}
	/**
	 * @see org.openmrs.module.department.api.DepartmentService#getDepartment(java.lang.Integer)
	 */
	@Override
    public Department getDepartment(Integer departmentId) {
	    return dao.getDepartment(departmentId);
    }
	/**
	 * @see org.openmrs.module.department.api.DepartmentService#saveDepartment(org.openmrs.module.department.Department)
	 */
	@Override
	public Department saveDepartment(Department department) {
		return dao.saveDepartment(department);
	}
	/**
	 * @see org.openmrs.module.department.api.DepartmentService#purgeDepartment(org.openmrs.module.department.Department)
	 */
	@Override
	public void purgeDepartment(Department department) {
		dao.purgeDepartment(department);
	}
} 
```


## Coding Conventions And Standards

When editing the DAO and service layer classes, don't forget to ensure that your code adheres to our general standards. Refer to the 'Development process' chapter, which will give you detailed instructions on how to ensure this.

Also, don't forget to add `Junit Unit tests` to validate that the methods you introduced behave exactly as they should. 


### Creating The Web Interface For Your Module

To make these changes to be accessible to users, you need to make changes to the module controller. You will also need to introduce a new file named `addDepartment.jsp` into the `/omod/src/main/webapp` directory. This will contain the `.jsp` page that lets you edit your name. The general contents of this class will be as follows: 

```html
<form method="post">
<fieldset>
<table>
    <tr>
        <td><openmrs:message code="general.name"/></td>
        <td>
            <spring:bind path="department.name">
                <input type="text" name="name" value="${status.value}" size="35" />
                <c:if test="${status.errorMessage != ''}"><span class="error">${status.errorMessage}</span></c:if>
            </spring:bind>
        </td>
    </tr>
    <tr>
        <td valign="top"><openmrs:message code="general.description"/></td>
        <td valign="top">
            <spring:bind path="department.description">
                <textarea name="description" rows="3" cols="40" onkeypress="return forceMaxLength(this, 1024);" >${status.value}</textarea>
                <c:if test="${status.errorMessage != ''}"><span class="error">${status.errorMessage}</span></c:if>
            </spring:bind>
        </td>
    </tr>
</table>
<br />
<input type="submit" value="<openmrs:message code="department.save"/>" name="save">
</fieldset>
</form>
```

Once the `.jsp` is complete, don't forget to modify the controller to point to this. It is also useful to add validations to asses user input when the controller is triggered.

```java
 @RequestMapping(value = "/module/department/departmentForm.form", method = RequestMethod.POST)
    public String submitDepartment(WebRequest request, HttpSession httpSession, ModelMap model,
                                   @RequestParam(required = false, value = "action") String action,
                                   @ModelAttribute("department") Department department, BindingResult errors) {
        
        MessageSourceService mss = Context.getMessageSourceService();
        DepartmentService departmentService = Context.getService(DepartmentService.class);
        if (!Context.isAuthenticated()) {
            errors.reject("department.auth.required");
        } else if (mss.getMessage("department.purgeDepartment").equals(action)) {
            try {
                departmentService.purgeDepartment(department);
                httpSession.setAttribute(WebConstants.OPENMRS_MSG_ATTR, "department.delete.success");
                return "redirect:departmentList.list";
            }
            catch (Exception ex) {
                httpSession.setAttribute(WebConstants.OPENMRS_ERROR_ATTR, "department.delete.failure");
                log.error("Failed to delete department", ex);
                return "redirect:departmentForm.form?departmentId=" + request.getParameter("departmentId");
            }
        } else {
            departmentService.saveDepartment(department);
            httpSession.setAttribute(WebConstants.OPENMRS_MSG_ATTR, "department.saved");
        }
        return "redirect:departmentList.list";
    }
 ```
 
Now that your module is completed, it is the perfect time to go ahead and test it. First test it yourself to make sure that there are no obvious mistakes before asking a target end user to try it out. The end user's feedback may result in further design discussions or reviews. Once these have been completed, the module can be implemented at the clinic, and also made available publicly. Refer to the guidelines specified in the 'Development Process' chapter to find out the best way to do this.

Once your module is released, you may think that your work is over. However, there is no such thing. As health systems, requirements, and technology change, so must the software.This makes medical informatics a viable career option, but does not mean you are responsible for maintaining `Hello World` for the rest of its life with OpenMRS.


### Sharing Your Module 

When done with developing and testing your module, you can release it for developers by deploying to the Maven repository using instructions at: http://om.rs/newdevtagging

For end users, you can release your module via GitHub Releases, Bintray, Maven, etc. Now, your published module will be added to the [Add-ons index](https://addons.openmrs.org/), which is available to everyone. Read more on the [Module Release process here](https://wiki.openmrs.org/x/zIMmAQ). Also read more about our rules and regulations for it here: http://om.rs/newdevmodrepo 
 