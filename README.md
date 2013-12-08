Drywall Angular
===============

A website and user system for Node.js using Angular JS and Jade based on Drywall (by jedireza). What you create with Drywall Angular is more important than Drywall Angular. [See a bird's eye view.](http://vchatterji.github.io/drywall/)


Technology
------------

| On The Server | On The Client  | Development |
| ------------- | -------------- | ----------- |
| Express       | Bootstrap      | Grunt       |
| Jade          | Backbone.js    |             |
| Mongoose      | jQuery         |             |
| Passport      | Underscore.js  |             |
| Async         | Font-Awesome   |             |
| EmailJS       | Moment.js      |             |
|               | Angular JS     |             |
|               | Noty           |             |

Live Demos
------------

We do not have any live demos of Drywall Angular, but you can see the demos of the original Drywall project by jedireza below:

| Platform                       | Username | Password |
| ------------------------------ | -------- | -------- |
| https://drywall.herokuapp.com/ | root     | h3r00t   |
| https://drywall.nodejitsu.com/ | root     | j1ts00t  |
| https://drywall.onmodulus.net/ | root     | m0dr00t  |

__Note:__ The live demos have been modified so you cannot change the root user, the root user's linked Administrator role or the root Admin Group. This was done in order to keep the app ready to test at all times.

Requirements
------------

You need [Node.js](http://nodejs.org/download/) and [MongoDB](http://www.mongodb.org/downloads) installed and running.

We use [Grunt](http://gruntjs.com/) as our task runner. Get the CLI (command line interface).

```bash
$ npm install -g grunt-cli
```

Installation
------------

```bash
$ git clone git@github.com:vchatterji/drywall.git && cd ./drywall
$ npm install
$ mv ./config.example.js ./config.js #set mongodb and email credentials
$ grunt
```

Setup
------------

You need a few records in the database to start using the user system.

Run these commands on mongo. __Obviously you should use your email address.__

```js
use drywall;
db.admingroups.insert({ _id: 'root', name: 'Root' });
db.admins.insert({ name: {first: 'Root', last: 'Admin', full: 'Root Admin'}, groups: ['root'] });
var rootAdmin = db.admins.findOne();
db.users.save({ username: 'root', isActive: 'yes', email: 'your@email.addy', roles: {admin: rootAdmin._id} });
var rootUser = db.users.findOne();
rootAdmin.user = { id: rootUser._id, name: rootUser.username };
db.admins.save(rootAdmin);
```

Now just use the reset password feature to set a password.

 - `http://localhost:3000/login/forgot/`
 - Submit your email address and wait a second.
 - Go check your email and get the reset link.
 - `http://localhost:3000/login/reset/:token/`
 - Set a new password.

Login. Customize. Enjoy.

Single Page Application Customization
-------------------------------------
After logging in to the system, the user is presented with an SPA for core functionality.

 - The client side (Angular) routes are defined in /angular/js/app.js
 - Angular controllers, services, directives and filters can also be found in /angular/js
 - The partials loaded by the routes above are located in /angular/partials
 - The menu shown on the left is loaded from /angular/partials/menu.jade

The core functionality can be customized by adding more routes, partials and changing the menu.jade file to include more links to the routes defined. 

Philosophy
------------

 - Create a website and user system.
 - Write code in a simple and consistent way.
 - Only create minor utilities or plugins to avoid repetitiveness.
 - Find and use good tools.
 - Use tools in their native/default behavior.

Features
------------

 - Basic front end web pages.
 - Contact page has form to email.
 - Login system with forgot password and reset password.
 - Signup and Login with Facebook, Twitter and GitHub.
 - Optional email verification during signup flow.
 - User system with separate account and admin roles.
 - Admin groups with shared permission settings.
 - Administrator level permissions that override group permissions.
 - Global admin quick search component.
 - Single Page Application using Angular JS (for the account page)
 - Loading animation while performing XHR Request using Noty

License
------------

MIT
