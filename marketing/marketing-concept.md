# Marketing concept

This file will explain the concept of marketing and how the different channels will be used.
For starters we take a look at all the different channels we will use.

## Channels

Overview:

* Website: 2martens
* Google+: +2martensDev
* YouTube: youtube.com/c/2martensDev
* Twitter: #2martensWebPlatform, @2martens

We will first look at the website in this concept.

### Website

The website will be the core of our web presence. The community will be found there
but also the project website and my personal information. There will be multiple phases
of the website. The first is the initial development of the platform. During this phase
we can't use the platform for the website but we need a website regardless. Most importantly
we have to be able to post news there and give an overview over the project for newcomers.
Therefore this part of the website concept will explain what software will be used to deliver
just that. 

The second phase will start after the Core bundle is finished. At that point the website 
will be switched to the platform with a preliminary mini-CMS at the front that allows us 
to continue the website usage. The community aspect will remain on the previously used 
forum. As the website will be based on the very platform it promotes, we will be able to 
gradually expand the website functionality as more functionality is developed.

The third phase starts when the entire 2martens Web Platform is finished and some applications 
exist. At that point the remaining part of the website will be switched to 100% web platform 
powered. From there on we can easily expand the website for our needs.

The timeline for all these phases is difficult to give, because it depends on many variables. 
One thing is certain however: The first phase must be reached ASAP. Currently there are several 
independent websites under 2martens.de:

* 2martens.de -> personal profile
* 2martens.de/web-platform -> pitch website for the platform
* 2martens.de/talks -> my "talks" (only one which I didn't actually held)
* 2martens.de/doc/ -> the rendered documentation for the platform

The goal of the first phase initiative will be to bring order into the chaos. In the upcoming
section I will show what the structure under the 2martens.de domain will be, what the feature
requirements for each of the areas are and last what software will be used to fulfill them.

#### First Phase

Structure:

* 2martens.de - landing page with latest news about the project
* 2martens.de/news/ - dedicated news archive
* 2martens.de/features/ - explains the features
* 2martens.de/about/ - about me page
* 2martens.de/community/ - community area (forum)
* 2martens.de/doc/ - rendered documentation (integrated)

Requirements:

The CMS part of the website must support media posts which embed YouTube videos (more on that later)
and above that the standard functionality of a CMS. Most importantly is the easy migration
to a custom solution later on (the data must be stored as minimalistic as possible).
Furthermore it must be possible to customize the look of the website in an easy way to represent
the "corporate indentity" of the 2martens Web Platform. Since the forum might be a different
application with a different structure, it must be easy to synchronize the user accounts.

The community part of the website will be a forum and must support the easy customization of
the look in a way that it matches the look of the CMS. The forum must be easy to use for
users, moderators and admins.

Both parts together must allow easy setup so that we don't have to invest time into setting up
the website, which could be spent better developing the platform itself.

After considering many applications, the final decision is presented below.

Software:

* CMS:
* Forum: