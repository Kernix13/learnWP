# Local development requirements

## Local development environment

- https://learn.wordpress.org/lesson/local-development-environment/
- live/production vs staging vs local environment
- local lets you focus on the code without having to set up a server and DB
- 2 types of local dev for WP:
  - those created & maintained by the WP community
  - those created & maintained by non-profits or companies

wp-env

- The [@wordpress/env](https://www.npmjs.com/package/@wordpress/env) package (wp-env) lets you set up a local WordPress environment (site) for building and testing plugins and themes, without any additional configuration
- this is the recommended environment
- you need an installation of Docker

vvv

- https://varyingvagrantvagrants.org/
- another local environment maintained by members of the WP community
- you need to install Virtual Box and Vagrant

XAMPP

- problematic though
- developed by Apache community

**Others**:

- localwp.com
- Studio by WordPress.com: https://developer.wordpress.com/studio/
- DevKinsta: https://kinsta.com/devkinsta/

## WordPress Installation

- localwp, devkinsta, and vvv all include a way to automatically create a local site and install WP for you
- for XAMPP you need to install WP yourself
  - you need to know the DB server name, the DB name, DB user name, DB PW
  - On local development environments, the DB server name is usually `localhost`
  - and the database username is usually `root`
  - The database password is either blank or `password`
- d\l the wp files as a zip file
- extract them and go into the `wordpress` folder - there are the core files/folders
- copy the files to the root of your local environment
- then go to the url of your local site to install WP
  - choose a language > continue
  - you see a screen with what you will need > let's go
  - enter the DB name, username (root), PW, BD host (leave as localhost), and table prefix > submit
  - you get an error message if the details are wrong that y ou entered
  - if correct - that creates wp-config.php which is used by WP to connect to the DB > Run installation
  - then enter site title, admin username and password, admin email address
  - click Install WordPress > log in

## Code editor

- VS Code
- VIM, Brackets, Sublime Text, Notepad++, TextMate, PhpStorm

## Other useful development tools

- the [WordPress.org Theme Test Data](https://codex.wordpress.org/Theme_Unit_Test) provides an option to import XML files containing dummy data for testing your themes
- the [Theme Check plugin](https://wordpress.org/plugins/theme-check/), which tests your theme for compliance with the latest WordPress standards and practices
- Similar for plugin developers there is the [Plugin Check plugin](https://wordpress.org/plugins/plugin-check/), which tests your plugin to ensure that it’s up to the base required standards from the WordPress Plugin Review team
- [Debug Bar](https://wordpress.org/plugins/debug-bar/) which adds a debug menu to the admin bar that shows query, cache, and other helpful debugging information.
- [Query Monitor](https://wordpress.org/plugins/query-monitor/) which enables debugging of database queries, PHP errors, hooks and actions, block editor blocks, enqueued scripts and stylesheets, HTTP API calls, and more..
- There is also [Log Deprecated Notices](https://wordpress.org/plugins/log-deprecated-notices/) which logs incorrect function usage, deprecated file usage, and deprecated function usage in your plugin or theme
