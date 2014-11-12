# Bundles

## Core Bundle
### Contents
The Core bundle contains all core elements of the platform.

### Feature list
* javascript dependency management
* object type support
    * API to CRUD object type definitions, object types
    * API to check/retrieve object type
* upload support
    * API to upload files
    * API to CRUD upload targets (control how the upload is processed)
* package system
    * API to CRUD of packages
    * API for package servers
    * stability filter
    * validation
    * API to search for new versions
    * uses Composer for retrieving, updating and deleting of the packages
* option system
    * API to save, edit and delete options
    * API to dynamically edit configuration of bundles
    * API to check for options
* user and group system
    * API to CRUD group options
    * implements wrapper for ROLE_* rights
    * more kinds of group options (integer, string, etc.)
    * API to check/retrieve non-boolean options
    * API to assign users to groups
    * API to CRUD groups and users
    * password hashing
    * API for credentials validation
    * API to add custom registration fields
* search system
    * API to CRUD search provider
    * API to CRUD search algorithms
* menu system
    * API to CRUD menu items
    * API to CRUD menus
    * API to retrieve menus and items
    * API to CRUD menu item provider
* feature type system
    * API to check feature type (of package/bundle)
* ACP
    * Bootstrap-based layout
    * FontAwesome
    * user-friendly menu structure
    * access to Core bundle functionality
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
* cronjob system
    * provides API for adding/updating/deleting cronjobs
    * provides API for calling cronjobs
        * Console command
        * service
    * provides API for (de-)activating cronjobs

### Interfaces
* every API that is offered by this bundle
* package installation plugins for various systems

## Content Bundle
### Contents
This bundle implements content behaviour, includes a WYSIWYG editor (Redactor), provides standardized API to CRUD contents and associate them with third elements. It makes use of the Core object type system to distinguish different kinds of contents.

It organizes the caching of said contents in a very performant way.

### Feature list
* message parser
* bbcode support
* HTML support
* Redactor (OEM license required)
* versioning
* reverting changes
* support for "parent" structure -> can be used for category (these parent structures can then be used for structuring it further)
* support for series -> a previous and next content (can be used for series of articles in CMS or thread in forum)
* various user rights (e.g. change content after creation, edit 3rd party contents)
* support for different versions (as in same content but different languages)
    * therefore the database ID is unique but the contentID is actually not necessarily unique

### Interfaces
* template that contains all needed components to render WYSIWYG editor
* package installation plugin that allows for new editor features (proxy for Redactor plugins)
* group options
* API for CRUD* content operations (includes versioning, ...)

## Language bundle
### Contents
This bundle implements internationalization support, effectively allowing the creation of multilingual contents. It uses the object type system to associate objects with languages (can be used for contents but also for other things).
The bundle supports both the one language per object philosophy (useful for conversations, threads) and the multiple languages per object philosophy (useful for CMS articles).

### Feature list 
* API to associate objects of any kind with a language
* support for different object types
* API to translate objects automatically to selected language (result depends on philosophy)
    * single language: object is exclusively associated to selected language
    * multiple languages: selected languages is added to the associated languages of object

### Interfaces
* ACP area to add new languages and delete (CAUTION: associations are lost) languages
* API to retrieve objects

## Media bundle

### Contents
This bundle implements media functionality. It provides media provider and an API to add more providers. Each provider (e.g. YouTube) has it's own syntax for source URLs. Furthermore the bundle understands oembed, which is an open standard for media embedding. 

### Feature list
* media provider (oembed and simple share link)

### Interfaces
* package installation plugin to add new media providers
* API to retrieve HTML for given share link/HTML5 include link

## Upload bundle

### Contents
This bundle implements upload functionality. This functionality includes the upload, storage, removal and referencing of (uploaded) files.

### Feature list
* API to upload, store, remove files
* support for "parent" structure (can be used to assign an upload to a content)
* API to assign uploads to users/groups

### Interfaces
* API to retrieve file contents and links
* API to get all files which are associated with a given object
* group rights
* template with all required components for upload

## Mail bundle

### Contents
This bundle provides API to send emails to a set of recipients. They can be given explicitly by username and/or indirect by group ID. The bundle uses the swiftmailer for the mail sending. Furthermore it supports the double-opt-in mechanism with all implied requirements (storage of confirmation, etc).

### Feature list
* API to send mails
* API to send confirmation mails (double-opt-in compliant)
* API to log mails to more than a few recipients (make misuse of mass mailing discoverable)

### Interfaces
* option in the ACP to configure threshold for mass mailing (min amount of recipients)
* group options

## Frontend Essentials bundle

### Contents
This bundle provides frontend access to Core functionality (e.g. login, registration). It requires only the Core bundle. 

### Feature list
* templates for login, registration, member list, search (standalone pages)
* templates that can be included in others
    * JS login/registration initiation
    * JS search
* template for menus
* controller for such templates (including routes)

### Interfaces
* the templates can be embedded if needed
* the registration template provides blocks to add new registration elements
* group options

## Community bundle

### Contents
This bundle provides community-related features. It requires the Core bundle, the Upload bundle and the Mail bundle.

### Feature list
* user profile
    * avatar
    * signature
* UCP
    * privacy settings
        * by default on most restrictive
    * group management
        * ability to join/leave an open group
        * ability to moderate a moderated group (you are moderator)

* API for group joining conditions
* API for activity measurement
* API to CRUD activity providers
* group joining conditions
    * time
    * email confirmation (e.g newsletter group)
    * activity
* more group types
    * open and moderated
    * closed and moderated
* notification support
    * provides API for triggering notifications
    * API to CRUD notification providers
    * interfaces with UCP settings to allow users to set up their notification settings
    * uses Mail bundle for email notifications
    * provides API to retrieve notifications for user
    * clear disclaimer that the acceptance of mail notifications will lead to mails to the user email address
* moderation support
    * API to CRUD moderation task providers
        * uses object type API to support various kinds of tasks (e.g comment approval)
    * moderation queue
        * API to register queue ideologies
            * provided: priority queue (items with more reports will end up higher)
        * API to CRUD filters
            * provided; only show tasks for areas in which moderator is responsible
    * logging of moderation actions (using monolog)

### Interfaces
* templates for user profile, UCP and ACP stuff
* template blocks to extend the templates
* package installation plugins for group joining conditions, activity providers, moderation task providers, queue ideologies, queue filters, notification providers
* group options


## Poll bundle

### Contents
This bundle provides poll functionality that goes beyond the ordinary forum multiple-choice. The "normal" community poll can be realized with this bundle but if offers far more. For example intervals are supported (give a number between a and b).
The bundle requires the Core bundle and integrates with the WYSIWYG editor of the Content bundle, if installed.
 
### Feature list
* API to CRUD polls
* API to evaluate poll results
    * each question type evaluates questions of it's type
* API to CRUD question types (e.g. multiple-choice, interval)
* provided:
    * single-choice
    * multiple-choice
    * slider/interval
    * free integer
* API to build polls

### Interfaces
* group rights
* package installation plugin for question types

## Conversation bundle

### Contents
This bundle implements the conversation system. It requires the Core and Community bundle.

### Feature list
* API to CRUD conversations
* API to CRUD conversation entries
* API to change conversation participants
* UCP settings for notification settings

### Interfaces
* group rightd
* use package installation plugin to provide notification provider

## Sanction bundle

### Contents
This bundle implements various sanction principles. It requires the Core and Community bundle.

### Feature list
* API to CRUD sanction types
* provided
    * timed ban (user can't login)
    * permanent ban (can be revoked manually)
    * no signature (timed)
    * no new user groups (timed)
* each sanction type can be configured to be automatically+manually or manually-only
    * if automatically+manually: number of bad points required
* API to trigger apply sanction/warning to user
    * bad points responsible for sanction are marked for removal after sanction
    * they will be removed if sanction is lifted (manually or after time period) and no new sanctioned offense happened
* API to CRUD warning types
* API to change bad point account of user
    * each change requires a reason that is saved
    * notification for user is triggered after such change
        * who approved it
        * what is the reason
        * link to object in question
* API to retrieve bad points of user

### Interfaces
* group rights
* integrates with MCP and ACP
* package installation plugins for sanction types, warning types
