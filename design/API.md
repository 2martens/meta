# API

## Packages

### Package Structure
There is no classical package structure. A 'package' is basically just an entry in an XML file with some meta information including but not limited to composer-relevant info, description, author info, license.

The system gets this information with a monitored XML file that only contains tested and approved packages.

### Package Installation

#### Distribution Application

The distribution is an application that requires the web platform bundles itself and 
all additional packages that can be installed from the ACP. That way we can use Composer 
even though it can only handle requirements.

#### Installation steps

##### User

In the following you will see the steps for the installation (user perspective).

1. Search for package
2. Click on install
3. Package requirements check
4. Download the package
5. Performing the installation
6. Fire successful installation event
7. Finish installation and show success message to admin
8. Optional packages offer (packages can offer recommended/optional packages, here you can select them for installation)
9. Optional: Rate installation experience and give your opinion (will be used to improve the product)

##### Technical

1. Download the bundle
2. Adding the bundle to the requirements of the distribution application
2. Install bundle (composer)
3. Adding the bundle to the AppKernel file
3. Finish the installation

#### Dependency management

Each package defines it's package requirements in it's package.xml file. This information is used during the installation process to show the requirements to the user. Under the hood however, each package is a bundle which contains the source code. These bundles can be easily managed by Composer and there is no reason to not use Composer.

To make Composer usage easy, all packages of the web platform will be submitted to Packagist.

By using Composer for managing the bundles in the background, the package system itself stays relative clean and straightforward. It is however open for confirmation, if this technique would actually work.

#### Technical structure of installation process

The installation process contains several areas. The first area contains predefined forms and pages before the actual installation. Next is the installation via Composer. Last is a phase which shows predefined forms and pages again.

### Package servers

There will be one official package server that provides an XML file with all approved packages.
To add a package here, a formal addition process will be developed. For this process a package.xml will be used. The information of this file will be added to the package server xml on approval. Admins can search the available packages through the ACP.

## Events

### General placement of events

Events allow the inclusion of new code in existing old code without modifying it. They can be used to add features (e.g. do something when a new user is registered) or to extend the existing functionality (modify a restricted set of variables). Another use-case is the explicit usage to gather content from various listeners in one place for unified processing. They are NOT to be used to redefine the execution and change the behaviour of the code that hosts the events. Therefore they are not allowed to change the state of the class/object (alter it's properties).

This leads to these placements:
* before changes of persistent data
* after changes of persistent data
* before showing a new page to the user
* before form validation
* after form validation
* custom locations that have to be documented in the bundle's documentation

### General Usage

Now that we know where to find events, we will go into how to use them. This does not mean the technical usage but the semantic usage. It also explains when alternative solutions are at hand. 

You can use the PHP events for mere execution points of your functionality (e.g. do A when B happens) or for specific additions to the functionality providing the event. In the case of a form you could add a form field. This includes several things:

* add the field by using the form builder provided by the event object
* adding code to validate the input (includes reading the parameters and throwing an exception if input invalid)
* saving the input
* assigning the input to the template (ensures that input is not lost on validation exception and is required anyway in an edit form)

All the PHP code is assigned to different events, so it is perfectly viable to have one plugin being stretched over multiple events in one class or even multiple classes.

### Bringing it to life

The event system uses the EventDispatcher component of Symfony. Each controller will use the dispatcher to dispatch events as described above. Services will do the same. So far so easy. The listener part is covered by the respective bundles themselves. The listeners are defined as services in the services.yml and are connected to the events with tags.

The listeners themselves will get the provided Event object, the event name and a reference to the EventDispatcher itself. Via the EventObject they have the chance to communicate with the providing class.

### Examples

An example for the usage of the EventSystem is the group system or more specifically the group options. The service responsible for returning the value of a group option will first look in the database. If it can't find the answer there and under the premise that only group options of installed packages are asked for, it will use an event to gather the necessary information. The event object will contain the information what option is required. The event listeners will then look if this options falls into their area of responsibility. If it does not, they won't process. If it does however, they will return the options of the entire bundle so that next time, options of this particular bundle will be available from database.

This procedure is called lazy initialization: The database is filled when needed. This is possible, because MongoDB does not require predefined schemas and is incredibly fast.
