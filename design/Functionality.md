# Functionality

This page covers the functionality of the web platform.

First we have a brainstorming on the functionality of the web platform.
The result of that is then clustered and organized into groups of features.

## Brainstorming

Functionality (no specific order):

* installing, updating and deleting packages
    * installing packages from package servers
    * automatic updates (requires package servers)
    * stability setting (e.g. install only stable updates)
    * modules which can be (de-)activated
        * ability to disable some features/packages globally
    * integrated package store
        * ratings of users
        * certified label (tested to ensure compatibility)
* change visual appearance with a click
   * user can select favourite style out of available styles
   * admin can set a style as default style
* create and edit your own styles
    * style variables for editing in editor
    * LESS support
    * converter for WCF 2.x compatible styles
    * converter for external styles (e.g. Bootstrap)
        * mapping of external CSS classes to CSS classes of web platform
        * copy and then replace external classes with own classes
* user and group management
    * login/registration
        * support for LDAP
        * email activation
        * admin activation
    * OpenID support (GitHub, Google, Facebook)
    * creating, editing and deleting user groups
        * default groups (everyone, registered users, moderators, admins)
        * custom admin created groups
        * custom user created groups (without own rights, can be upgraded
          and to full groups and degraded back to user groups by admin)
    * group assignment
        * manual (both by hand and programmatic)
        * condition-based
            * member for more than x time
            * member with more than x activity (calculated out of a variety
              of actions)
        * password based
    * group rights
        * best right wins (the less restrictive right over all groups the
          user is in wins)
        * divided into categories (e.g. frontend, backend)
        * multi-level rights (global, per-project, per-application, etc.)
    * email to all users (use rarely, refer to spam regulations)
    * email to members of specific user group
    * user control panel (UCP)
        * signature
        * avatar (Gravatar support)
        * privacy settings
            * user group specific settings who can see what
        * management of groups in which the user is the group leader
    * user profile (all shown things can be configured in UCP)
        * last activity
        * guestbook
        * wall for user created messages (with reply functionality)
        * best rated contents (depends on installed applications)
            * forum threads
            * answers/questions in a Stackexchange format
            * articles
        * latest activity from followed users
    * following other users
* multiple languages
    * support for multilingual user generated content
    * switching language as guest with a simple click
    * switching language as reg. user in the settings
    * display contents of selected languages only (e.g. limit visibility 
      to English and German contents)
* content system
    * support for BBCodes
    * support for WYSIWYG editor (e.g. Redactor [yes, not free software])
    * support for HTML
* support for uploads
    * attachments (uploads attached to an entity)
    * general uploads (globally available for all applications)
    * file management
        * deleting uploaded files (ATTENTION: might have large impact)
    * admin uploads (global uploads)
    * user uploads (could be used for a gallery)
* media support
    * support for HTML5 video/audio includes
    * support for video hosters (YouTube, Vimeo, etc.)
        * oembed support
    * API for packages to use, when they want to provide media functionality
* project support
    * manage multiple projects
    * attach each project a domain
    * select applications for each project (out of list of installed
      applications)
    * configure each project
        * database credentials for project database
        * project specific application settings
        * select existing user groups which are accessible within project
            * users in these groups are already member of the group in the
              project context
        * select existing user groups which are created new in project
            * users in these groups are not member in the project context
              and need to become members again
    * create new groups limited to this project
        * allows for separate projects with different user base
        * can be made globally accessible later on
* ACP
    * configuring and controlling via graphical user interface
    * just ONE kind of accessing the underlying functionality
* Console
    * access to some functionality (mostly administrative tasks) that
      doesn't require much user input
* Dashboard
    * a place in frontend where latest activity across the project can
      be seen
    * support for multi-project information
* Moderation support
    * moderation control panel (MCP)
    * support for different kinds of moderation (e.g. forum threads)
    * moderation queue
    * moderation log (who did what, when and why)
    * 4+ eyes support
        * voting for each moderation action
        * 2+ moderators must approve an action
* Notifications
    * API for sending notifications
    * includes settings for UCP
* Polls
    * creating polls (easy and advanced)
        * easy: standard community polls (question plus multiple answers)
        * advanced: boolean (yes/no), Likert scale, etc.
    * evaluating polls (easy and advanced)
        * easy: for each answer percent of total votes
        * advanced 
            * API to retrieve raw data
* Menus
    * modular menus
        * a CMS might offer the created contents/pages/categories as
          menu items
        * adding these items with a mouse click, no further settings
        * custom menu items (with route and text)
    * multiple menus
        * each project gets one central header and footer menu
        * more menus can be used by applications
    * global top menu (with UCP, notifications, MCP, link to ACP, etc.)
    * support for multi-level menus
        * the specific visual representation depends on style

## Clustering

In this section we will take this features, prioritize them and split them
up into different levels. One functionality might be covered by multiple
levels (e.g. the package system provides a general API and is represented
in the ACP). In such a case they are split up into different implementation
features.

These levels are available:

* Core level
    * these features are vital to all other features
* Utility level
    * these features are mostly self-contained and only require Core
    * these features can be used outside the web platform
* High-End API level
    * these features utilize many features below their level
    * they don't provide an accessible frontend/backend
        * they can provide controllers and templates which can then be
          accessed from higher level features
    * these features are the defining features of the web platform
* Application level
    * these features have accessible frontend/backend
    * they are integral part of the web platform and cannot be used separately
    * they have many dependencies to lower level features
    
TODO
