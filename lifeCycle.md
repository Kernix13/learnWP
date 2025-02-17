# WordPress request lifecycle

> https://learn.wordpress.org/tutorial/the-wordpress-request-lifecycle/

> I think this was covered in a WP User course or a WP Dev course

learn the basics of the WordPress request lifecycle, walking through the process that happens on the web server when a browser makes a request to a WordPress URI

1. Describe how query strings or permalinks affect the request lifecycle.
2. Identify the main files loaded during a request lifecycle.
3. Explain how the main WordPress query data is generated.
4. Describe the process of determining which template file to load.

### Comprehension questions

1. Which file is the main entry point to every WordPress front-end request?
2. Which file sets up the WordPress environment?
3. How does the template loader determine which template file to load?

### A note on query strings and query variables

Before you dive into the WordPress request lifecycle, it's important to understand how query strings and permalinks.

A query string is a part of a URL that assigns values to specified parameters. The query string appears at the end of the URL and is indicated by a question mark. For example, the following URL contains a query string:

    	http://example.com/?page_id=2

The query string can contain multiple parameters, each separated by an ampersand

Typically, a WordPress install has permalinks enabled, which means that the query string is not part of the URL

Either way, the permalink or the query string contains information about the data that needs to be queried. During a typical WordPress request, the query string or permalink will be converted into query variables, that WordPress will use to fetch the relevant data

### The WordPress request lifecycle

1. **index.php**:

- The entry point of any WordPress front-end request is the index.php file. This is the file that will run whenever a request is made to anything not under the wp-admin directory
- If permalinks are enabled, the code in the `.htaccess` file will rewrite the request to the index.php file. If permalinks are disabled, the query string will be passed to the index.php file
- Here, the `WP_USE_THEMES` constant is set up, and then the first additional file is required, wp-blog-header.php

### A note on require, require_once, include, include_once

- `require` is a special php statement that will include the contents of the file being required.
- There's a similar statement in PHP called `include`, which does the same thing.
- The difference is that using require will throw an error and end execution if the file can't be required.
- There's also a supplementary statement called `require_once` (or `include_once`) that will only include the file if it's not been included already.

2. **wp-blog-header.php**:

- The `wp-blog-header` file sets up the WordPress environment by requiring the `wp-load.php` file
- It then calls the `wp()` function, which sets up the WordPress query, and then loads the theme template by requiring the `template-loader.php` file

3. **wp-load.php**:

- Here the `ABSPATH` constant is defined, which is used by most plugins as a check if the plugin is indeed being run in a WordPress environment
- This file then sets some `error_reporting` levels
- After that it finds and loads the `wp-config.php` file OR attempts to redirect to `/wp-admin/setup-config.php`, to inform the user to create the `wp-config.php` file

> **INCREDIBLY IMPORTANT NOTE**: You'll also note that this code allows the `wp-config.php` file to be moved outside of the WordPress directory, which is a common security best practice. By moving the `wp-config.php` file outside of the WordPress directory, you can prevent the file from being accessed by a malicious user

> I moved it for FPS from `/public_html/Blog` up 1 level to `/public_html`

4. **wp-config.php**:

- This file defines the DB constants, debugging constants, and other constants that your WordPress installation might need.
- It then requires the `wp-settings.php` file which sets up the WordPress environment

5. **wp-settings.php**:

wp-settings.php is the file that sets up the WordPress environment. It does quite a lot of work, so this will just be a high-level summary of all the things it sets up

- First, it sets up some version information then it requires all files needed for initialization
- Then there are a few functions that set up most default constants
- It registers a fatal error handler if anything goes wrong, sets things like timezone, and fixes the server variables
- It checks for maintenance mode and checks for debug mode
- Next, it requires the core WordPress files needed for the core WordPress functionality
- It sets up the database layer and any global database variables and initializes multisite if multisite is enabled
- Then if the `SHORTINIT` constant is defined, and set, it will stop the rest of WordPress being loaded. This is handy if you need to create custom requests which only need the core WordPress functionality, but not things like custom post types or custom taxonomies
- It then loads the localization libraries and runs the installer if WordPress is not installed and then it loads the rest of any WordPress files needed
- Eventually, it loads any must-use plugins. These are plugins that WordPress requests must always use and have a special `mu-plugins` directory where they are located.
- It then loads any network-activated plugins. This is specifically if they are installed on a multisite
- It sets up any specific cookie constants or SSL constants and then includes a `vars.php` file which creates any common global variables
- Next, it calls two functions which create the initial taxonomies and custom post types. So this would be page and post types and any initial taxonomies. This allows these taxonomies and posts to be available to plugins and themes
- After that, it registers the theme directory root
- And then eventually it loads all the active plugins
- After that, it loads pluggable functions
- After that, it defines any additional constants which may be required
- And then it calls a function which adds magic quotes to any `GET` or `POST` request variables and sets up the request array
- Then it creates an instance of the WordPress query object, the WordPress rewrite object, the main WordPress object, the widget factory object, and the user roles object
- Then goes ahead and creates any template-related constants and any default text localization domains, creates a locale object, a locale switch object, and then loads the functions for the active theme, both parent and child themes if necessary - You'll see it does this by getting the active and valid themes looping through them
- And then including the theme's functions.php file
- It then creates an instance of the WP Site Health object so that it can fire off any current events, sets up the current user, checks the site status, and eventually runs the `wp_loaded` action hook so that any callback functions hooked into that hook can be run

6. **wp() function**:

Once the WordPress environment has been set up, the wp function is called. This function determines what needs to be rendered and fetches the relevant data from the database

Inside the function itself, you'll see that it accesses the global `$wp`, `$wp_query` and `$wp_the_query` objects that the settings file created and then runs the main method on the `$wp_object` passing in the query variables.

If we go to the `main` method of the WP class, you'll see that it runs the `init` method which calls the `$wp->get_current_user` function and sets up the current user object. It then runs the `$wp->parse_request` method which parses the request and sets up any query variables based on the request. Inside `parse_request`, it first matches the request to the rewrite rules and creates a `query_vars` array based on the match rules. If no rewrite rules match the `query_vars` array is populated based on the request, whether it's a query string, or anything else.

If the `parse_request` method returns `true`, the main method will then query the posts, handle any 404 response and register any globals.

If we dive into `query_posts`, you'll see that it accesses the `wp_the_query` object, builds the query string, and then queries the data, based on the `query_vars`.

Inside of `build_query_string`, this is where it sets up the query based on permalinks or any query strings or anything else that's been passed.

Then looking into the query method of `$wp`, the query that first runs any kind of initialization, passes the arguments, sets the `query_vars`, and then runs the `get_posts` method

This will then retrieve an array of posts based on the query variables. You'll see it triggers hooks like `pre_get_posts` so that you can access the query object and make changes should you need to

And then if you scroll through all this code, you will see that it is basically looking for any kind of parsed query variables, any parameters, any kind of complex combinations, and creating the SQL query string that can be run on the database

Eventually, right at the bottom of this function, it returns the `current_posts` array

Going back to the main function of the WP class, once query_posts is run, it'll handle any 404 problems. This is if no posts are found, it effectively sets any headers for a 404 request. Back to the main method, it'll then send any headers to the browser. And then last but not least, fire any callbacks hooked into the wp action hook passing in the `$wp` object by reference so that any callbacks can access that object

### template-loader.php

After all the query data is set up the template loader is required. This finds and loads the correct template based on the visitor's URL

As you can see, there is a `template_redirect` action hook which fires before the template is loaded, and allows plugins and themes to interact should they need to. It then checks for certain things; so is a request being made for the `robots.txt` file, is a request being made for the `favicon`, is a request being made to an RSS feed, then perform actions for the RSS feed and exit execution. Or is the request to trackback in which case include the trackback functionality and exit execution

After that's all checked, it'll loop through each of these template conditionals and find the appropriate template file. You'll see that this is an array of template tags, and template functions. Below that, you'll see that it loops through all the tag templates and calls the tag templates. And then if a response is true, calls the template getter function to find that template

...After that, there is a `template_include` filter that gets fired. And then last but not least the template is included. You will notice here that it uses the `include` statement and not `require`. This means that if that file doesn't exist, for whatever reason, the functionality will still continue. If it doesn't find a template file, and the currently `logged-in` user is an admin user — in other words, they can change themes –, it'll then get the theme and report some errors to the admin user

> Good to very good to very important for development
