# Section 1: A brief overview of how WordPress works

## WordPress and web servers

- How WordPress and web servers work together
- a web server is connected to the internet and configured to serve web pages
- they are just computers with special software
- WordPress runs on a tech stack called LAMP: Linux, Apache, MySQL, PHP
- Linux is the OS
- Apache is the web server software that serves the info on a web server
- Nginx is an alternative to Apache which is faster with static content (LEMP)
- by default Apache and Nginx are configured to serve static files
- PHP is used to create dynamic web pages
- when you install Apache or Nginx on a server, there are some files you can configure to change the way the web server works
- one configuration set that allows a single instance of a web server to serve content from multiple websites, to serve different content for different websites
  - on Apache that's called a Virtual Host
  - on Nginx is called a Server Block
- here is an example of a virtual host

```apache
Listen 80
<VirtualHost *:80>
  DocumentRoot "/www/example1"
  ServerName www.example.com
</VirtualHost>
```

- here is Nginx

```nginx
server {
  listen 80;
  server_name www.example.com;
  root /www/example1;
}
```

- NOTE: port 80 is the default port for web requests
- by default the web server is configured to look for a Directory Index file - if it finds one it will serve that file, otherwise a 404 error
- the default file is usually index.html
- when PHP is installed and enabled it's possible to configure a PHP file as the Directory Index file
- the default is usually index.php
- with Apache: `DirectoryIndex index.php index.html`
- with Nginx: `index index.php index.html;`
- when a user visits a url of a WP site, the following happens:
  - the browser sends a request to the web server for the data at the url
  - the web server receives the request and determines which file s\b executed
  - in a WP site, the index.php file in t he root directory
  - the PHP interpreter then executes the PHP code
  - if required, the PHP code will interact with the MySQL database
  - the PHP will then output HTML with associated CSS and JS
  - the web server will send those back to the browser
  - the browser then renders that code and display the page to the user

## The WordPress file structure

- in the root: 3 folders and a series of files
- `.htaccess`: a special file used to configure the Apache web server for a specific WP install - an extension of the Apache Virtual Host - any vlid Apache directives can be added to the file - Nginx does not allow an htacess file like configuration
- `license.txt`: the open source license for WP
- `readme.html`: info about WP
- `index.php`: includes code to require wp-blog-header.php
  = `wp-blog-header.php`: requires wp-load.php
- `wp-load.php`: requires wp-config.php
- `wp-config.php`: the main configuration file for a WP site and requires:
- `wp-settings.php`: sets up all the core WP functionality
- there are other php files in the root directory that perform specific functions outside of regular WP requests - usually accessed directly by a user or another Fx and are not included in a normal WP flow
- wp-activate.php: to confirm the activation key that is sent to an email after a user signs up for a new site
- wp-comments-post.php: to process comments submitted on a WP site
- wp-cron.php: to run any scheduled tasks - run every time a wp page is requested and checks to see if any scheduled tasks need to run
- wp-links-opmi.php: genearates an xml file of links but that features was removed in WP version 3.5 (included for backwards compatibility)
- wp-load.php:
- wp-login.php: displays the login form & processes login requests
- wp-mail.php: used by the post via email feature
- wp-signup.php: the signup form for a new site on a multi-site network
- wp-trackback.php: process trackback requests
- xmlrpc.php: processes any xml-rpc requests sent to a WP site - that protocol is used by the WP mobile app but you can disable it if you don't use that app to manage your site
- wp-admin/: all the files that power the admin interface
- wp-content/: includes files that can be added to a WP install like plugins, themes, uploaded files
- wp-includes/: the bulk of the core WP files - PHP core files, JS and CSS files, ...

## The WordPress database

- WP uses a DB to store, retreive, and display all the content you create on your website - posts, pages, commnets, ...
- it also stores info about your users, and options
- phpMyAdmin: web-based tool that allows you to interact with the DB
- Adminer is an alternative to phpMyAdmin
- SQL Buddy plugin is another option - but delete wehn done using it because installed it is a security risk
- the db has different tables - each table stores a different type of data
- each table has the same prefix which is defined in wp-config.php
  - by default it is `wp_` but you can change that

Most important tables:

- `wp_posts`: stores the info for your posts, pagees, and custom post types - each row represents a single post
  - `wp_postmeta`: to store additional info about each post - postmeat also referred to as custom fields (?)
- wp_comments: each row is a single comment
  - wp_commentmeta
- `wp_users`: info about your users
  - wp_usermeta:

For all WP database tables, there are FXs you can use to interact with them - these FXs form part of the WP database API - they generally follow the same pattern:

1. there is an insert, update, and delete Fx
2. usually have the same prefix: `wp_` followed by the action and name of the table:
3. `wp_{action}_{table_name}`

Some of these Fxs for posts:

- wp_insert_post(): to create a new post
- wp_update_post(): to update a post
- wp_delete_post(): to delete a post

Then there are FXs to fetch all the records from a table or a single record

1. usually have the same prefix: `get_`
2. followed by the singular or plural name of the table
3. `get_{table_name}`

- `get_posts` is a Fx to fetch a collection of posts
- `get_post` is a Fx to fetch a single post

There are FXs to interact with meta tables usually to insert or update meta fields

1. usually have the same format: the action followed by the table name followed by `_meta`
2. `{action}_{table_name}_meta`

- `add_post_meta` is the Fx to add a meta field
- `update_post_meta`
- `delete_post_meta`

Terms tables (tables that manages cats and tags)

- wp_terms
- wp_termmeta
- wp_termrelationships
- wp_termtaxonomy - stores info about what page/post they belong to
- Functions: get_term, edit_term, get_terms, is_term, term_link, tern_name, the_terms - search for `term` or `taxonomy` to see al lthe FXs

wp_options table:

- stores info about your site's settings
- each row is for a separate setting
- key: value > option_name: option_value
- it is possible to store serialized data in the options table
- serialized data is a string that contains multiple values
  - they are often used to store arrays and objects of data
  - the list of active plugins is stored this way
- the Options API is typically used (along with the Settings API) to create settings pages for the admin area

wp_links table - stores info about w sites links (removed in version 3.5)

> It's extremely useful to be able to interact with the DB tables

## Permalinks, rewriting urls on Apache and Nginx

How they are used to rewrite dynamic urls...

- the Directory Index file is executed when a user browses to a URL
- but with WP it's possible to have different types of content rendered like posts, pages, or products via the same Directory Index file
- the key feature behind how that works is Permalinks

Query Strings:

- a query string is a way to pass data to the web server, e.g. `?s=dog+walk` where the variable `s` is being set to `dog walk`
- it is possibel to get the value of `s` using the super global `$_GET['s']`

```php
$s = $_GET['s'];
```

- the PHP code can then use that for some sort of data lookup
- so Permalinks (aka key urls) are a way to make dynamic urls more human readable
- instead of using a Queery String, Permalinks use a URL structure that is based on the content being rendered
- but how does the web server know what content to serve
- based on the expected url structure, the webserver can be configured to perform URL mapping which uses a web server feature called URL rewriting
- you can set a custom permalink structure then WP stores that structure in the DB
- on Apache this is handled typically in `.htaccess`
- Nginx does this in the block configuration file in a locati

## Front-end page request

- https://learn.wordpress.org/lesson/front-end-page-request/
- there are 2 types of requests that can be made to a WP site - a front-end request and an admin request
- aay request for ontent on a WP site is handled by the index.php file in the root directory
- WP_USE_THEMES followed by a `require` `wp-blog-header.php`
- require vs include - they do the same thing but require will throw an error if the file can't be required
- require_once and include_once will only include the file if it hasn't already
- `wp-blog-header.php`: sets up the WP environment by requiring the wp-load file
- in `wp-load.php` the `ABSPATH` variable is defined - that is often checked to make sure the plugin is being run on a WP environment
- it sets up some error reporting then loads the `wp-config` file or asks the user to create that file if it doesn't exist
- this file allows wp-config to be moved out of the WP directory which prevents the file being accessed by hackers
- finally it requires `wp-settings.php`
- `wp-settings.php`: does a lot of work:
  - sets up WP version info
  - requires files needed for initialization
  - it calls FXs to set up constants, fatal error handling, default timezones, checks for maintenace mode for debug mode
  - then checks if it needs to load the advanced cache
  - sets up WP_LNAG_DIR
  - loads early WP files
  - it sets up the global DB object `$wpdb`, sets up the DB connection, then starts object cache
  - it initializes multisite if enabled, then SHORTINIT??? SHORTINIT can be used for custom requests in WP
  - it loads the localization libraries, runs the installer if WP is not installed
  - then runs most of the rest of the WP libraries
  - it then starts setting up any globally used libraries like WP_Embed and WP_Textdomain_Rigistry objects
  - loads multisite specific files
  - then sets up and installs any must-use plugins (mu_plugins)
  - if this is a multisite it will load network plugins
  - then fire mu plugins once they are loaded
  - it then sets up cookie and ssl constants and creates common global variables
  - it creates the taxonomies and post types
  - registers the theme root directory
  - then starts to load active plugins
  - then sets up default constants, add magic quotes and `$_REQUEST`
  - then creates more global objects: wp_the_query, wp_query, wp_rewrite, wp, wp_widget_factory, wp_roles
  - sets up templating constants, loads default textdomain, and sets the wp_locale
  - it thens loads functions.php and for the child theme if one is installed
  - creates a WP_Site_Health object and sets up the current user
  - checks the status of multisites
  - fires any cb FXs hooked into wp_loaded action hook
- back to wp-blog-header: once the wp environment has been set up, the wp() function is called - that fx determines what needs to be rendered and fetches it from the DB
- the wp() fx calls the main method of wp object which is found in wp-includes/class-wp.php - that calls its own init() method which calls the fx wp_get_current_user() which sets up the current user object > the main() method calls the parse_request() method
- that method does a lot but basically it matches the request to the rewrite rules and creates the query vars array based on the match rules
- if ($parsed) the main() method calls query_posts(), handle_404(), and register_globals()
- query_posts calls build_query_strings() then query() blah blah blah -> send_headers(), runs hooks tied to wp action hook > then template-loader.php
- note the use of include rather than require so that the rest of the file can run if the template isn't found

## Admin page request

- https://learn.wordpress.org/lesson/admin-page-request/
- handled by the files in `wp-admin/`
- instead of permalinks, query strings are passed
- /wp-admin will load the index.php file in the wp-admin directory
- to view posts it changes to wp-admin/edit.php
- to view pages though it becomes `wp-admin/edit.php?post_type=page`
- to edit a post you see post.php/?post=
- the query strings vars determine what content to display
- there are a lot of commonalities how these admin files work
- admin.php: sets up admin specific constants and includes the same wp-load.php file that is used on the front end which in turns includes wp-config, wp-load, and wp-settings
- it will then load specific functionality
- dashboard.php blah blah blah
