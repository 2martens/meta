# Functionality

This page covers the functionality of the web platform.

First we have a brainstorming on the functionality of the web platform.
The result of that is then clustered and organized into groups of features.

Content:

* [Brainstorming](Functionality.md#brainstorming)
* [Clustering](Functionality.md#clustering)

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
        * these are basically the Bootstrap LESS variables
    * LESS support
    * the own styles are basically just a custom Bootstrap theme
        * the variables and mixins are injected by the compiler
    * common policy for general structure
        * styles shouldn't add new classes
        * semantic classes shouldn't get a new meaning
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
    * activity points (measurement for activity)
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
* option support
    * packages can introduce configuration options that can be modified by
      the admin
    * these options are available throughout the defining package and
      packages that require that package
    * support for dynamically set configuration of lower packages
        * packages below the application level can't provide options by
          themselves, but they might expose a semantic configuration
        * it should be possible to set this configuration dynamically from 
          a package in a higher level
* ACP
    * configuring and controlling via graphical user interface
    * just ONE kind of accessing the underlying functionality
* Console
    * access to some functionality (mostly administrative tasks) that
      don't require user input
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
* cronjobs
    * actions that are performed regularly without user input
    * Console command which can be used for creating real cron task
    * underlying system for packages to register their regular tasks
    * option to call cronjobs even without real cron

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
The features sorted by level:

Core

* required 3rdParty javascript libraries
    * jQuery
    * jQueryUI
    * (Backbone)
    * (Twitter Bootstrap)
* offers different CDNs plus local version
* object type API
    * there can be different object types
    * useful when the same code should be applied to different types of 
      content
    * provides a way to create a object type definition, which defines an
      object type

Utility

* support for uploads
    * templates for general uploads and attachments
    * API to differentiate between upload modes
* media support
    * media provider (oembed and simple share link)
    * API to retrieve HTML for given share link/HTML5 include link
* multiple languages
    * API to save contents of any kind
    * support for different object types
    * API to translate contents automatically to selected language

High-End API

* package system
    * API for installing, updating, deleting packages
    * provides API for package servers
    * provides functionality to filter for stability
    * provides validation API
        * validates package archives (can be used to check if own package
          is valid, before applying it to a package server)
        * allows validation of to-be-installed packages
    * provides API to search for updated packages
    * each package consists of one or more bundles, which are handled internally
        * the user only sees packages
        * the system handles the bundles and updates them via Composer
        * the package itself is only some xml files used for transporting 
          meta data
        * a package can be updated, when one of it's bundles is updated
* style system
    * LESS compiler (lessc.inc.php)
    * compiler
        * style variables are added prior to each compile process
        * mixins are added prior to each compile process
    * provides API to retrieve stylesheet of given style
    * support for CDNs
        * configure a CDN and the link to the stylesheet is changed
    * FontAwesome for icons
        * semantic css classes for icons
    * default semantic css classes based on Bootstrap
    * provides default style that uses default Bootstrap colors
    * each style provides a layout HTML that is inserted into a layout.twig
        * this layout HTML has to contain specific blocks (each empty)
        * it can contain additional blocks (must be documented to allow
          usage by others)
* option system
    * API for saving and editing options
    * provides way to dynamically edit configuration of bundles
    * provides API to check for certain options
* project system
    * provides API to create and delete projects
        * creates skeleton tables in a project database for all selected
          applications
        * API to register more things that can be saved per-project
    * handles multiple database connections
    * provides API to retrieve current project
    * provides abstract controller that saves information about current
      project in session (valid for one request only)
* user and group system
    * provides API for adding group options (e.g package installation)
        * supports wrapper for ROLE_* rights (boolean group options)
        * many more kinds of group options (integer, string, etc.)
    * provides API for checking/retrieving group options (the non-ROLE ones)
        * the ROLE options are already covered by default Symfony
    * provides API for assigning users to groups
    * provides API for creating/editing/deleting groups and users
        * groups:
            * user-created groups
            * admin-created groups
        * users
    * supports various ways of registration/login
        * LDAP
        * OpenID (e.g. GitHub, Facebook)
        * registration form
            * no activation
            * email activation
            * admin activation
    * password hashing
        * bcrypt
        * double salted hash
    * credentials validation API
        * can be used for all sorts of validation
        * by default used for user validation
    * provides API to add more elements to UCP
    * uses option system to save user settings
        * predetermined domain used for these settings
        * adding/removal of options directly through options system
    * user profile
        * API for adding new segments of the profile
        * API for retrieving those segments
    * API for adding/retrieving/removing activity
    * API for adding/retrieving/removing activity points
    * API for following users
        * retrieve who follows which user
* menu system
    * provides API for adding/updating/deleting menu items
        * supports different menu item types
        * each saved menu item must provide a way to retrieve a valid route
          to access it
        * menu items can be actually sub menus
            * one sub menu level supported by default, more could be possible
              based on the chosen style
    * provides API for adding/updating/deleting menus
        * menus are abstract container for all types of menu items
        * each menu gets assigned a twig block name (headerMenu and footerMenu
          supported by default, more blocks might be supported based on
          chosen style)
    * provides API for retrieving menus and items
* cronjob system
    * provides API for adding/updating/deleting cronjobs
    * provides API for calling cronjobs
        * Console command
        * service
    * provides API for (de-)activating cronjobs 
