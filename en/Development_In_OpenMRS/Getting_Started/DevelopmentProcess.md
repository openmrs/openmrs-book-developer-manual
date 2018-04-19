<center><h1>Development Process</h1>
************************************

## Selecting Development Work

Selecting your initial task depends on your personal preferences and expertise. We recommend you work on at least a few introductory tickets so that you can better understand our development workflow when you start.

OpenMRS uses [Atlassian's JIRA](https://www.atlassian.com/software/jira) software for issue tracking purposes. The OpenMRS JIRA installation can be found at https://issues.openmrs.org/.

JIRA allows you to search for suitable tickets using a number of criteria. When choosing a ticket, identify one based on a programming language or task that you are already familiar with to reducing the learning curve involved.

You may also want to work on issues or limitations that you identified yourself. First, create a ticket for this task in JIRA by clicking on the "Create Issue" link. Next, wait for your issue to be reviewed by a core OpenMRS developer. Begin work on the issue after it has been assessed and discussed, and a core developer changes its status to "Ready for Work".

If you are selecting an existing ticket to work on, please make sure that:

* The issue is marked as "Ready for Work".
* The issue is not "In Progress" and claimed by someone else.
* The issue is not "blocked" waiting for the completion of another issue.

## Beginning Work 

We assume that you have already installed git on your computer, and that you are able to access it using the command line, which is often easier to interact with than IDE integration plugins.

[See https://www.atlassian.com/git/tutorials/ to learn git] 

Log in to JIRA with your OpenMRS credentials, and then claim the ticket by clicking on the **"Claim Issue"** button. This will indicate to others that you are working on this issue, so that they do not duplicate your work. You should also identify the OpenMRS version affected by this particular issue, and make sure to check out the appropriate version of the source code to complete your task. For most cases, you will need to check out the master branch. If you are not sure, just put a comment on the ticket asking for guidance. 

Use the following steps to check out source code onto your local machine:

**Step 1:** If you don't have a GitHub account, create one here: https://github.com/

**Step 2:** On GitHub, fork a project you want to work on. You may use the tutorial http://help.github.com/fork-a-repo

**Step 3:** Clone the project repository from your fork.
Fire up Terminal and enter the command:

```shell  
  git clone https://github.com/{yourusername}/openmrs-core.git
``` 
**Step 4:** Now, go into the folder just created and set up the **"upstream"** remote so you can eventually pull changes from the main repository.

``` shell
    git remote add upstream https://github.com/openmrs/openmrs-core.git 
 ```
## Using Git To Manage Your Work

You should use a separate branch for your development work on each JIRA issue. The following steps describe how to do so.

**Step 1:** Check out out a new local branch based on your master/tag recommended for the fix and update it to the latest. The convention is to name the branch after the JIRA issue key, for example, **"TRUNK-123"**. 

 To create a new branch, use the following commands:
```shell
  git checkout -b TRUNK-123 master
```
**Step 2:** Push the branch to your fork:
```shell
  git push -u origin TRUNK-123
```
Now you may begin work on your task on the newly created branch.

## Coding Conventions

In addition to basic Java coding conventions, use the following steps to ensure the quality of your code:

##### Managing Deprecation:

* Deprecate public methods instead of changing/deleting them in order to preserve backwards compatibility. We will delete all deprecated methods when we release a new major version (e.g., from 1.x to 2.0). 
Use both the **@Deprecated** annotation and the **@deprecated javadoc comment**.
The @deprecated javadoc annotation should point to the new method that is replacing the current one.
DAO methods do not have to go through a deprecation cycle. They can be changed/deleted outright.
 ##### Security:

* To enforce security, avoiding XSS scripting by using `StringEscapeUtils.escapeJavaScript()` and `StringEscapeUtils.escapeHtml()` to escape any user-generated data in pages.

##### Code Formatting Style:

* OpenMRS uses Eclipse auto-formatting features for managing the style of your code. These formatting rules are included in the `OpenMRSFormatter.xml` file which can either be downloaded from http://om.rs/newdevformatter or the source code checked out from GitHub. To apply these guidelines, use the command `Ctrl+Alt+F`. ```
Running the command mvn clean install will also enforce these formatting stylistics on your code.

## Quality Assurance Efforts

* **Meaningful use of comments:** Provide enough comments to cover the specific work you have undertaken in your code.
* **Javadoc comments for each method:** Provide a Javadoc comment for each new method you introduce. Also, you should update existing Javadoc comments to indicate any modifications you have made.
* **Unit testing:** Write proper unit tests to cover each alternative scenario introduced or modified by your changes. Your changes to the code may inadvertently affect other program code as well. Therefore, you should always be sure to run all the unit tests to validate your work.
* **Evaluating performance:** In the event that your changes may affect performance, we recommend that you evaluate its impact using a profiler such as YourKit. 

## Maintaining Your Code

To identify which files you have changed, run the following command:
```shell
  git status
```
This will return a list of all new or modified files which you can review to ensure that no unintentional changes made it into your commit.

#### Stage and Commit Your Changes

As you work on your code, you may want to periodically stage and commit your changes into your branch. To stage all changed and new files into your commit, use the command:
```shell
  git add -A
  #alternatively 
  git stage .
```
To pick only some files, use:

``` shell
  git add -i
  #alternatively 
  git add {filename}
```
Using this command displays a summary of changed and new files along with a list of options which you can carry out. To stage selected files, you need to choose the 'update' option. Choose the files which you want to stage, marking them either by entering their file id (as listed in the console). You may also specify a file range such as 1-3, or simply enter * to select all. Confirm your selections by pressing the ENTER key twice. Choose option '7' (quit) to complete the process.

Now these files are staged, and ready to be committed. 

**To commit your code into your branch, use the command:**
```shell
git commit -m "TRUNK-123: Put change summary here (can be a ticket title)"
```
Please remember to specify the current JIRA issue number in your commit message. The use of meaningful commit messages is important.

## Pushing Your Code And Requesting a Review


After multiple iterations of making changes to your code and committing them into your branch, push your code into your fork by running the following commands.

**Step 1:** Update your branch to the latest code using the following command:
```shell
  git pull --rebase upstream master 
```
**Step 2:** If you have made many commits, squash them into atomic units of work. Most JIRA issues, especially bug fixes, should have one commit only, making them easier to back-port. To do so, use the instructions at: http://om.rs/newdevsquash

**Step 3:** Make sure all unit tests still pass by running:
```shell
  mvn clean install
```
**Step 4:** Push your changes into your fork:
```shell
git push
```
Running this command will prompt you to authenticate into GitHub. After doing so, it will upload the changes into your fork. You may now visit your push on GitHub at a URL like
```
  http://github.org/{yourgithubname}/{fork}/ 
```
where "fork" will be something like "openmrs-core". Create a pull request using the create pull request link on GitHub.

After you make your pull request, go to the relevant JIRA issue and click the button to request a code review on that ticket. When doing so, add a comment to the ticket with a link to your pull request. This will automatically schedule the ticket to be reviewed by a core developer. Your code will not be reviewed until you follow this process in JIRA.

### About Attribution

In OpenMRS, attribution is done via commit comments only. When a committer applies a patch, the author or authors of the patch are attributed within the commit comment itself. We do not put attribution into source code. This avoids the challenges of deciding when someone's name should be added to a file and places the focus on everyone working together to create awesome code. OpenMRS will graciously refuse contributions from volunteers who require attribution of their work within source code.

## Code Review

A senior developer will review your code, and may suggest revisions. You may be asked to make changes to your patch, and re-submit it for review. Code review is an iterative process, and multiple review cycles may be required. Additional changes made to your patch can be built on the same branch used previously.

Review happens on GitHub, which allows your code to be evaluated by multiple developers, and detailed review comments added.

In other cases, reviewing a ticket may involve significant discussion which may lead to further refinement or redesign work. We believe that healthy discussions around our code will contribute towards identifying the best solution for a given task.

Ultimately, once all reviews have been completed, a patch will be accepted and merged into the OpenMRS core system. After this, the status of the JIRA issue will be changed to "Closed". Assuming your task represents a change in the current workflow, you should update the existing documentation to reflect these changes.

Closing a JIRA issue ends the official workflow, and now you are free to begin work on other tickets. Sit back, relax, and find a new ticket!


### Reopening Issues

A closed JIRA issue might be reopened if it causes the current build to fail, needs more work, or triggers a significant disruption of the existing system.

If further improvements to your work are identified at a later stage, these will be listed under a separate ticket which would be linked to the previous one. In such a case, you are welcome to either claim or ignore the new ticket. You may be contacted for your thoughts.


## How to Get Help

General questions regarding the task you are working on can be asked by adding comments to the issue on JIRA. Such comments are seen by the issue's requester and other people who specifically are "watching" the issue. You may also request help for your work by asking questions using the community discussion channels discussed previously in this book. The OpenMRS community is very extensive, and greatly encourages and assists newcomers, so feel free to ask constructive questions.

Check out the Support chapter of this book for more about how and where to get help. 

In the event that you feel that you are unable to complete a JIRA issue that you have claimed, feel free to unassign yourself from the issue, and select an different ticket to work on. Remember to put comments about any progress made or findings you feel relevant for whoever takes on the ticket. 
Suggesting process changes

Often, developers may wish to suggest changes to existing process. These discussions usually begin on the OpenMRS developers mailing list, and may be carried over to our weekly design meetings based on the significance or impact of the suggested changes. Code reviews performed on a given ticket may also result in the need for more detailed design discussions. In this case, the discussion should be moved over to a mailing list, and if necessary, into the weekly design meetings.

### Publicizing Your Work

We highly encourage developers to publicize their work so other community members are able to learn from and re-use their work. You should do so using one or more of these methods:

* Make your work publicly accessible via GitHub.
* Add appropriate documentation to the OpenMRS Wiki.
* Discuss your work on [OpenMRS Talk](https://talk.openmrs.org/), answering related questions, and joining in design discussion on the topic.
* Create and submit example videos to be published on the OpenMRS YouTube channel.

### Requesting tool licenses for your development work

OpenMRS encourages the use of open source tools for development work. However, in certain cases, you may require licenses to use some commercial tools. OpenMRS provides contributor licenses to community members in good standing who can demonstrate need for using these tools. Licenses may be available for a number of tools including IntelliJ IDEA and the YourKit profiler, among others. If you are able to demonstrate sufficient need to obtain such a license, please contact the OpenMRS help desk at [help.openmrs.org](https://help.openmrs.org).

## Understanding OpenMRS Releases

### What goes into a release

Release timelines and supported features are largely decided upon by the OpenMRS leadership group. Larger goals are discussed, agreed upon, and documented under the OpenMRS technical road-map, which is a set of predefined milestones for the core OpenMRS platform and sponsored modules.

More detailed on the release process can be found [on the wiki](https://om.rs/newdevrelease).

The latest technical road-map can also be found [on the wiki](https://om.rs/newdevtechmap).

The release process is managed by a release manager who is responsible for getting the source code stabilized, packaged, and released to the general public. 

## OpenMRS Release Types 

#### Alpha Release

An alpha release is a feature-complete release which has not yet been verified as bug free.

#### Beta Release

A beta release is made after obvious bugs found in the alpha release have been fixed. Therefore, a beta release is ready to be tested by a larger group of people. 

#### Release Candidate

A release candidate is only needed when non-trivial changes were required during the beta phase. If the beta release was tested and no significant changes were detected, developers may proceed directly to a full release.

#### Major Release

A major release is deemed tested and worthy of production environments.

#### Maintenance Release 

A maintenance release contains bug fixes and security patches for use between major releases, e.g., from 1.8.0 to 1.8.1. For maintenance releases, no additional branches are created. Developers simply begin where development work was left off in the current minor version series release branch. 

#### Release Rranch

A new release branch is created for each new major and minor release. As an example, a new release branch is created when preparing to release version 2.0.0, or version 1.3.0. However, when preparing to release 1.3.1 (a maintenance-version increment), the release branch created at the time of 1.3.0 is simply re-used. 

## Continuous Integration (CI) For OpenMRS

Continuous Integration Systems play an integral role in software development. OpenMRS adopted the CI tool Bamboo following our shift into the agile development process.

The use of CI has brought OpenMRS a number of benefits including:

* Automating the process to ensure that regression doesn't occur with new code changes. Often a change in the API or module results in 'breaking' other dependent modules. A CI System will rebuild OpenMRS after a change is committed, thereby providing information on how that change affects other dependent code.
* Providing an easily comprehensible user interface that provides statistics/status of successful and failing tests
* Providing an easy method of monitoring work done on different branches and modules. 
* Allowing users to easily identify 'test fails only for me' vs. 'test fails for everyone' scenarios. 
The OpenMRS continuous integration tools can be accessed at http://ci.openmrs.org/.

## Summary

You should now have an understanding of how to develop with OpenMRS. In the next chapter we will put these skills to use by getting your local development environment set up.
