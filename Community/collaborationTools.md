<center><h1> Collaboration Tools</h1>
**************************************
<center>
![](http://write.flossmanuals.net/openmrs-developers-guide/collaboration-tools/static/Collaboration%20Tools.jpg)
<center><i>2013 OpenMRS Implementers Meeting, Eldoret, Kenya</i>

##Tools and tips

In the previous section, we examined some ways to work together in the OpenMRS community. This section will explore some of the tools we use to do so. We have many different ways we can work with one another. Our main collaborative tools include:

* OpenMRS ID
* OpenMRS Wiki
* OpenMRS Talk (a question-and-answer service)
* IRC
* Telegram
* Mailing Lists
* JIRA Issue Tracker 
* Git for version control

Most tools have specific functionality and purposes, and some tools are better suited for certain things than others. For example, you might have a specific question you want to ask, or are looking for a project to collaborate on, or want to report a bug, or simply want to say hello. 
Let's look at some of these collaboration tools, their functionality, and how to use them.

### 1. OpenMRS ID 

In order to use most of our community tools, you'll need to create an OpenMRS ID. (This isn't used for the OpenMRS software itself, but just our collaboration tools.) When you create your OpenMRS ID, you'll create a user profile with information about who you are. You can also create a personal space on the OpenMRS Wiki where you can detail your work and interests.


> Here's where you can sign up for your ID:  https://id.openmrs.org/
Learn more about the OpenMRS ID here: http://om.rs/id


### 2. OpenMRS Wiki

The vast majority of our documentation is stored on our wiki. If you have a question or want to learn more about anything, the wiki is a great place to turn. It contains both general and specific information about the core system, add-on modules, our community, and other project resources. Users, implementers, developers, contributors and curious people use the wiki to find and share information. 

You can search for information in the wiki using the search bar in the top right corner, or by using the links on the left of the page to navigate to the relevant section.

You can communicate directly with other community members by leaving comments on wiki pages. You also directly edit the wiki if you find an error, if it's out of date, if you've updated the project or if it just doesn't have complete or accurate information. If you're not sure or don't want to edit the page, feel free to leave your thoughts in a comment. You should create a new wiki page when you start a new project, or if you note that one doesn't exist (perhaps an interesting discussion on the mailing list deserves its own page). When you do this, make sure that the page doesn't already exist!  


> Always document what you're doing on the wiki- this helps everyone in the community! 



The OpenMRS Wiki is available at: http://wiki.openmrs.org/  

### 3. OpenMRS Talk

Another great resource for posting and searching for questions and answers is OpenMRS Talk, our online question-and-answer site. If you have specific problems or need help troubleshooting, this is a great space to browse others' questions and answers, and seek out help from other developers. You can answer questions on the site as you learn more about OpenMRS and become an experienced developer, earning points and badges along the way. 

OpenMRS Talk can be found online at: https://talk.openmrs.org/c/ask

### 4. IRC

[Internet Relay Chat](https://en.wikipedia.org/wiki/Internet_Relay_Chat) is a form of real time chat and conferencing. IRC is a great way to chat with other people in the OpenMRS community in real-time. IRC is a good place to ask questions, get help with a problem, discuss ideas, or just chat! Keep in mind that there are not always people actively watching the IRC channel, so if your question or comment isn't answered, it might be useful to send out an email to the mailing list as well. 

We use the #OpenMRS channel on the Freenode network. You can visit our chat room directly from the web, or use an IRC client. We recommend 
* **X-Chat** or **mIRC** for Windows
* **X-Chat** or **Irssi** for Linux and 
* **Textual**, **Colloquy** or **Adium** for Mac. 
* Or the web interface on https://webchat.freenode.net/ 

We keep up-to-date logs from our IRC channel on the OpenMRS Wiki. They are fully searchable, and can be a great place to check if you problem or question that someone might have already addressed. 
* View the logs here:  https://wiki.openmrs.org/display/IRC/Logs+-+OpenMRS
* For more information on the IRC channel: http://om.rs/irc 

### 5. Telegram 
[Telegram](https://telegram.org) is an open source messenger that syncs with our IRC channel and is great for communication. The sync in made possible by two Telegram Bots: OpenMRS Bot and our Telegram Bot. Telegram Messenger can be downloaded from the official website and supported is on Windows, Mac, Linux, iOS, &amp; Android.

### 6. Mailing Lists

We have several different mailing lists for groups of people within the community. As a new developer, you should start by joining the main developers mailing list. This is a great place for design discussions and development troubleshooting, and can facilitate long term (as well as short term) discussion among developers.

You can subscribe to the list by sending a blank e-mail to dev+subscribe@openmrs.org, or by updating your profile at http://id.openmrs.org/.
After subscribing, you can e-mail the list at dev@openmrs.org. 
There are other mailing lists you might be interested in, such as the implementers mailing list. 

More information about this and other lists are available online: http://om.rs/lists
We also keep archives of all of our mailing lists. This is a great resource to check if something has been discussed in the past. You can view all the logs before 2012 at http://listarchives.openmrs.org/ and everything beyond that date is available on each list's Google Groups page, such as:http:/om.rs/dev. The address for each list's archive is included at the bottom of every message to the list. 

### 7. JIRA Issue Tracker

[JIRA](https://www.atlassian.com/software/jira) is the software that tracks issues for the OpenMRS community. It records issues and bugs that people have noticed and need to be addressed, feature requests, as well as projects being worked on. Developers, users and implementers all use JIRA to report, comment and solve problems and create content. 

You should use JIRA to create a new issue if you find a bug. Be sure to include a clear description of how to recreate the error, the error message if applicable, the version of OpenMRS you are using, the type and version of the database you are using, any additional modules or customizations, and any other relevant information. If applicable, copy and paste the full Java stack trace. The easiest way to report an OpenMRS bug is by using the web form at http://issues.openmrs.org. If you'd like to be more specific, you'll need to use the appropriate JIRA project to report a bug for the OpenMRS core/trunk application, a specific add-on module, etc.

Bugs in JIRA have four specific phases of their life cycle. First, someone notices a bug and creates a JIRA issue to report it. Second, the bug is validated by other members of the community to makes sure enough details have been included. Third, a person begins to code a patch for the bug. Finally, upon the completion of the code, it goes through a code review to make sure it is a valid fix.   

You should also use JIRA to create a new issue if you start a new project. As a developer, JIRA is a great place to find a first contribution. The issue navigator also keeps track of introductory tickets that can be a good place for a new developer to get started. 

### 8. Git

[Git](https://www.atlassian.com/git/tutorials/) is a distributed version control system (DVCS) which allows many developers to work on one project without having a specific network connection. Most developers host their source code on GitHub, though feel free to host yours wherever makes sense for your needs. We recommend creating an account on GitHub so that you can clone (copy) repositories (folders of source code) to your local machine. You can then make changes on your local machine and push (send) them to [GitHub](https://github.com). Git can be very easy to use once you learn a few key commands, and is a great collaborative tool for developers. It allows you to write messages each time you commit (save) what you've done, and keeps a log of these messages.

Writing good commit messages is an important part of letting other developers know what you've been working on. Make sure that your commit messages are specific and concise. Each commit should address one ticket change. Don't combine multiple issues into one commit. Make sure the commit contains the ticket number. When in doubt, look at what other people have written in their commit messages! Reading through commit messages from other developers is also important to know what has been done and what is being done.

* For more in-depth training on how to use Git for OpenMRS, see: https://www.atlassian.com/git/tutorials/
* To learn more about OpenMRS coding conventions, see: https://wiki.openmrs.org/display/docs/Coding+Conventions
* For more information about our repositories: https://wiki.openmrs.org/display/docs/Core+Modules
* All OpenMRS modules are available on GitHub at:*  https://github.com/openmrs

## Let's Get Started 
As you've read in this section, there are many tools to help you work with other community members, so dive right in and introduce yourself on IRC and create your personal wiki space. You now have the tools you need to start working as a developer, so in the next section we'll guide you through that process. We're excited to meet you. **Welcome to our community!**

