<center><h1>Working Cooperatively</h1>
********************************************
<center> 
![](http://write.flossmanuals.net/openmrs-developers-guide/working-cooperatively/static/Working%20Cooperatively.jpg)

## Getting things done

Regardless of whether or not you've participated in large software development projects, if you're new to open source projects you may be in for some surprises. The leadership of such projects is very "flat" -- meaning that there isn't a lot of bureaucracy to deal with. On the other hand, you'll find that as a developer, you're given great freedom in finding interesting work and designing what gets built. The more code and ideas you contribute, the more you'll become a leader in the project.


> "People should feel that their connection to a project, and influence over it, is directly proportional to their contributions." - **Karl Fogel, Producing Open Source Software **

Free and open source software projects offer an ideal setting for coordination and crowd-sourcing of ideas and solutions. You should always try to be open to what others might have to say about your ideas and code -- great ideas don't necessarily have a single owner or contributor! Listen to what others have to say, and pay attention to what they're doing ... there's a lot to learn from everyone in the OpenMRS community. Working together can be hugely beneficial to everyone involved, and the sharing of ideas can yield rich results.

One of the easiest ways to build functionality in the OpenMRS ecosystem is to use our modular architecture, which is covered in more detail later in this book. Add-on modules allow you to try lots of different ideas to solve problems. Modules also let you to build upon the work of others through dependencies.

## Play nicely

The OpenMRS community has established a [Code of Conduct.](https://wiki.openmrs.org/display/docs/Code+of+Conduct) It's less of a list of rules as much as it is some useful guidance about ways to work in the community to help each other and be successful. You should take a moment to read it and be familiar with the values mentioned there, which include:

* Be considerate
* Be respectful
* Be collaborative
* When you disagree, consult others
* When you are unsure, ask for help
* Step down considerately


## Working Asynchronously

You'll find lots of people willing to help and give advice in the OpenMRS community, but they might be located across the planet from you. That means you should try to plan your work tasks to work asynchronously. For a quick answer, searching Google, our [Wiki pages](https://wiki.openmrs.org) finding someone to chat with on our [IRC channel](https://wiki.openmrs.org/display/IRC/Home) or [Telegram Group](https://telegram.me/OpenMRS) works well. However, it's more likely that you'll need to write a question to one of our mailing lists and end up waiting for an answer before you can continue. Having a few tasks, issues, or projects going in parallel will help you to feel more productive while you wait for answers or supplemental information to get your work accomplished.

## Collaboration vs. Cooperation

People often speak of working collaboratively on a project when large groups are involved. Before using these terms, it's important to understand the differences between the words collaboration and cooperation. When people collaborate, they work closely together on a single goal. When people cooperate, however, they coordinate their work on "selfish" but similar goals. Collaboration works well in small groups, but cooperation allows large software projects to support both individual and group goals.

Both types of work happen in the OpenMRS community. When looking at the development of code for the OpenMRS core software, you'll find lots of collaboration. Core developers need to frequently communicate their ideas in detail to avoid causing problems for other core developers. The same holds true when there are several developers working on an OpenMRS add-on module.

Cooperation happens when looking at the different teams who develop OpenMRS modules. Those teams are most successful when they cooperate to prevent duplicate efforts, such as the creation of two modules that provide the same functionality.


> As an OpenMRS developer, you should plan to cooperate more than you collaborate. This means you'll need to have a good understanding of your personal or small group goals, and you'll need to communicate more than you might be accustomed. This chapter will review some tips on how best to do so.



### Find mentors

Mentors are a great way for new developers to learn about participating in the OpenMRS community. We're a very friendly group of people, and there are plenty of people who, not too long ago, were new to our project just like you. They can help you find interesting work, answer questions about getting your environment set up, or help connect you to other people in the community who share your interests.

The easiest way to find a mentor is to simply write to our developers [mailing list](https://wiki.openmrs.org/display/RES/Mailing+Lists) with a short description of what interests you and some of the questions you're having as you get started. If you get stuck or have issues at any time, send an e-mail to our community management team at community@openmrs.org and they will help answer any questions you have.

The OpenMRS community also regularly participates in two formal mentoring programs. [Google Summer of Code (GSoC)](https://summerofcode.withgoogle.com) is a summer (in the northern hemisphere) program for university students age 18 and over, offering a stipend to do development work on open source projects such as OpenMRS. Applications generally open each spring.[ The FOSS Outreach Program for Women (OPW) ](https://gnome.org/opw/)is a program for all women age 18 and over that offers 3-month projects on development, documentation, project management, and other tasks in open source projects. Check out the web sites for both programs to learn more about them.

### Forming Questions

One of the greatest things about a free and open source software project is the large community of developers, contributors, and users available to help you find answers to questions or inspire you. 

Our project has been around many years, so there is a lot of reference material available to understand why certain design decisions were made. Some of this material is current and much of it can be useful for a historical perspective. When developing questions to ask others in the community, it's important to do some background research first to make sure that there isn't already a readily-available answer. 

### Communicate publicly &amp; productively

In an open source project, all decisions happen in public. This means you should avoid private conversations such as instant messages, phone calls, and face-to-face meetings -- particularly when brainstorming or making decisions about software design. We have many different public tools available for our community to support these conversations, and those tools are described in detail elsewhere in this book. Ensuring that decisions are made in public venues maximizes participation and exposes those decisions to as many brilliant minds as possible. Try not to make decisions in private, or you might miss out on interesting ideas.

Because we're a large project, much written communication gets generated every day for other developers to read. To help, try to do your part in maintaining a high signal-to-noise ratio on mailing lists or other communication tools. Think before you post a message, and make sure what you're writing adds value to the conversation. Responses like "me too!" or "+1" are rarely productive. 

### Avoid bikeshedding

Although we encourage public discussions about our software design, it's also important to avoid non-productive conversations about trivial details. This type of anti-pattern best described by the concept of [bikeshedding](https://en.wiktionary.org/wiki/bikeshedding), which gets its name from a 1960s book about management. In the book, C. Northcote Parkinson described how it might be often easier to get approval for an expensive nuclear power plant than it could be to discuss what color to paint a bike shed. Everyone feels they have a valid opinion of what color to paint the bike shed, but only certain qualified people can comment on the design of a reactor. Don't let yourself fall into this trap -- avoid these wasteful conversations on trivial topics.

See http://om.rs/newdev-bikeshed for more information about bikeshedding. 

### Commit Early and Often

One of the biggest (and often most difficult) lessons for open source developers to learn is commit changes to your source code repository early and often. Don't wait until you are finished with a project,or even a single feature. In the past, OpenMRS used the Subversion version control system which made this more painful. However, with DVCS systems like [GitHub](https://github.com) in use now for most of our software, it's much easier to get your work-in-progress published online as you go. There are a few reasons to embrace this behavior. 

* First, by committing early you'll have more chance for others to stumble across your work. They may have very valuable feedback or ideas that you might want to consider to make your project more useful. They may also have already written something very similar and may prevent you from duplicating effort.

* By committing your work often, you'll be protected in case of an accidental data loss. You'll also be able to share your progress with others, so they can get a better idea how much work remains. If you're committing code regularly and a lot of work remains, you might find someone to help you by squashing bugs or adding additional features.

* Don't be afraid that your work appears "not ready". After all, it probably isn't ready yet! In free &amp; open source projects, one of the most important practices is to share your work in progress. Make sure you do your part. 

### Share &amp; license your work

We recommend naming your source code repository to include the word "OpenMRS" so others can more easily find your work. For example, if you're creating the FooBar module, you might name your repository "openmrs-module-foobar". Similarly, when you're at a point that you want to introduce your project or projects to others in the community, we strongly encourage you to do so! The easiest way to do this is to write a short description of your project along with links to more information, 

It's also important to consider what type of license your work will have. If you don't provide a license with your software, it might remain copyrighted and its use might still be restricted in ways which you may not intend. (The specifics of what would happen depend on the laws where you are.)

Many different free and open source software licenses exist, and sometimes it can be hard to choose one. The creators of GitHub have created http://om.rs/newdev-choose which is an easy way to compare some of the popular FOSS licenses currently in use.

The OpenMRS core application is licensed under the [Mozilla Public License (MPL) version 2,](https://www.mozilla.org/en-US/MPL/2.0/) along with an additional disclaimer of warranty and limitation of liability (essentially a disclaimer for how the software is used in health care settings). We encourage use of this license for consistency across our community-developed software ecosystem and license compatibility between add-on modules. However, you are free to choose any license you wish. Just make sure to choose a license.

## Summary

In this section, we reviewed some of the unique aspects of working together in an open source project like OpenMRS. In the next section, we'll cover more details of the tools we use to do so. If any time you have questions about how best to work cooperatively, ask a more senior member of the community for guidance, or write to a mailing list with your questions. You'll find everyone very friendly and ready to help you be productive! 