# An introduction to developing WordPress plugins

## What is a plugin?

- a package of code that can be installed on a WordPress website to add new features or functionality
- to add to or extend a theme's functionality
- you will often need to create custom functionality for a WordPress website
- it is possible to add this functionality to a theme or child theme’s functions.php file, it often makes more sense to add this code to a WordPress plugin because a plugin can be activated or deactivated without affecting the theme

### The structure of a WordPress plugin

Most WordPress plugins in the plugin directory are composed of many files, but to create a valid plugin you only really need one main PHP file with a specifically formatted comment block, also known as a DocBlock, at the top of that file

```php
<?php
/**
 * Plugin Name: Example Plugin
 * Plugin URI: https://kernixwebdesign.com/plugins/example-plugin
 * Description: This is an example plugin.
 * Author: James Kernicky
 * Author URI: https://kernixwebdesign.com
 * Version: 1.0
 */
```

The [WordPress plugin developer handbook](https://developer.wordpress.org/) is a great resource for learning how to create a WordPress plugin. It contains information on how to create a plugin, how to use the various WordPress APIs, and how to submit a plugin to the WordPress plugin directory

I just tried creating a plugin to add post formats called add-post-formats and it worked.

## Plugin requirements

- The minimum requirements for a valid WordPress plugin are at least one PHP file, the main plugin file, with an opening PHP tag
- Inside the main plugin file, the first piece of code should be the Plugin Header, which is a PHP comment block - At a minimum, it should contain a field for the plugin name

How WordPress identifies and stores active plugins:

- Once a plugin is activated, it is added to the list of active plugins stored in a serialized array in the options table. You can find this array by running the following SQL query in phpMyAdmin

```sql
SELECT * FROM `wp_options` WHERE `option_name` LIKE 'active_plugins'
```

- it stores the filename of the PHP file as the plugin slug and is how WordPress identifies your plugin during execution
- If you move your main plugin file inside a directory, the plugin slug changes to include the directory name

### Plugin header fields

While the plugin name field is the basic requirement for a valid plugin, there are additional fields available for you to add to the plugin header.

It’s generally recommended to also add a description and version to the plugin header. This allows users to get a bit more information about your plugin, and it looks better when displayed in the Plugins list

### Plugin best practices

Check out common [best practices](https://developer.wordpress.org/plugins/plugin-basics/best-practices/)

- One of these suggestions is to include a check to ensure that the plugin code is only executed when part of a WordPress request - it's best to include that check right after the plugin header:

```php
if ( ! defined( 'ABSPATH' ) ) {
    exit; // Exit if accessed directly
}
```

- What this code does is check if the ABSPATH constant is defined, which is a WordPress-specific constant. If it’s not defined, then exit the code execution of the plugin.
- This way, if someone tries to browse to the main plugin file in a browser directly, none of the PHP code in the plugin will be executed, preventing any security risks

## Custom post types

- https://learn.wordpress.org/lesson/custom-post-types/
- One of the more common use cases for developing a custom plugin is to take advantage of the WordPress Post API to create custom post types

### Building an online bookstore (e.g.)

- you want to store data about the books that are for sale
- The WordPress core Post API allows you to register custom post types. These custom post types extend the core post data type, which is stored in the `posts` table in the WordPress database
- An example of a custom post type is the `page` data type, which is registered by WordPress core
- Using the WordPress POST API, you could create a custom post type to store information about books
- When you register a custom post type correctly, WordPress will automatically create a new admin menu item for your custom post type, and admin pages to manage the data

### Custom post types

- To register a custom post type, you use the WordPress `register_post_type` function
- this function takes two parameters: the name of the custom post type, and an array of arguments that define the custom post type
- Add a directory in the `wp-content/plugins` directory called `bookstore`
- create a new PHP file called `bookstore.php` inside

```php
<?php
/**
 * Plugin Name: Bookstore
 * Description: A plugin to manage books
 * Version: 1.0
 */

if ( ! defined( 'ABSPATH' ) ) {
    exit; // Exit if accessed directly
}

function bookstore_register_book_post_type() {
     $args = array(
        'labels' => array(
            'name'          => 'Books',
            'singular_name' => 'Book',
            'menu_name'     => 'Books',
            'add_new'       => 'Add New Book',
            'add_new_item'  => 'Add New Book',
            'new_item'      => 'New Book',
            'edit_item'     => 'Edit Book',
            'view_item'     => 'View Book',
            'all_items'     => 'All Books',
        ),
        'public' => true,
        'has_archive' => true,
        'show_in_rest' => true,
        'supports' => array( 'title', 'editor', 'author', 'thumbnail', 'excerpt' ),
    );

    register_post_type( 'book', $args );
}

add_action( 'init', 'bookstore_register_book_post_type' );
```

> Notice the use of the `bookstore_` prefix in the function name. This is an example of prefixing function names to avoid conflicts with other plugins or themes

### Custom Post types and performance

- It’s important to note that registering too many custom post types can have a performance impact on a WordPress site
- This is because the custom post type registration process is executed on every site request, even if the custom post type is not being used on that page
- So be careful of overusing custom post types and consider when you should use them vs creating custom tables to store custom data
- You can learn more about creating and using custom tables in the [Creating Tables with Plugins](https://developer.wordpress.org/plugins/plugin-basics/creating-tables-with-plugins/) page in the Plugin developer handbook

## Custom taxonomies

- https://learn.wordpress.org/lesson/custom-taxonomies/
- taxonomies are a way to group things together. In a default WordPress install, there are two types of registered taxonomies: categories and tags
- When developing a plugin that registers a custom post type, you can also register custom taxonomies
- This adds some additional flexibility to your plugin, as it allows your custom post types to be grouped independently from the default categories or tags

### Why use custom taxonomies?

- there are times when your plugin might need to group data in a different way
- you might want to group books by genre
- when you register a custom taxonomy for a specific post type, that taxonomy will only be available to that post type and will appear associated to the post type in the admin menu and the edit screens

### Registering a custom taxonomy

- use the `register_taxonomy` function
- and call the `register_taxonomy` function, passing in the relevant arguments to create the taxonomy
- Once this is added to your bookstore plugin, you’ll see a new Genre menu item in the admin menu, and you’ll be able to add genres to your books

```php
<?php
/**
 * Plugin Name: Bookstore
 * Description: A plugin to manage books
 * Version: 1.0
 */

if ( ! defined( 'ABSPATH' ) ) {
    exit; // Exit if accessed directly
}

function bookstore_register_book_post_type() {
    // see code from previous lesson
}
add_action( 'init', 'bookstore_register_book_post_type' );

function bookstore_register_genre_taxonomy() {
    $args = array(
        'labels'       => array(
            'name'          => 'Genres',
            'singular_name' => 'Genre',
            'edit_item'     => 'Edit Genre',
            'update_item'   => 'Update Genre',
            'add_new_item'  => 'Add New Genre',
            'new_item_name' => 'New Genre Name',
            'menu_name'     => 'Genre',
        ),
        'hierarchical' => true,
        'rewrite'      => array( 'slug' => 'genre' ),
        'show_in_rest'           => true,
    );

    register_taxonomy( 'genre', 'book', $args );
}
add_action( 'init', 'bookstore_register_genre_taxonomy' );
```

## Custom post type data

Sometimes, the default custom post type fields might not be enough, and you need to store additional data on a custom post type. WordPress supports something called post metadata, which allows you to store additional information about a post.

### What is post metadata

- Post metadata is a way to store additional information about a post in the WordPress database
- Post metadata is stored in the `postmeta` table
- it has four columns: `meta_id`, `post_id`, `meta_key`, and `meta_value`
- `post_id` is the ID of the post that the metadata is associated with. `meta_key` is the name of the metadata field, and `meta_value` is its value

### Adding post metadata

- You can add post meta to a post using the `add_post_meta` function.
- This function takes three parameters:
  - 1. the ID of the post,
  - 2. the name of the metadata, and
  - 3. the value of the metadata
  - e.g., `add_post_meta( 1, 'location', 'London' );`
- There are other functions for working with post meta, such as `update_post_meta`, `delete_post_meta`, and `get_post_meta`

### The Custom Fields panel

It is also possible to enable site administrators to add post metadata via the WordPress admin interface. One way to do this is the _Custom Fields panel_ for the post type.

- To enable the Custom Fields panel, you will first need to make sure your custom post type supports metadata
- you need to add or update the `supports` argument, to include support for `custom-fields`
- Then, when editing a custom post type, click on the editor’s `Options` icon, select `Preferences`, click `Panels`, and enable the `Custom Fields` toggle
- This will refresh the editor, and you’ll see the Custom Fields panel at the bottom of the screen
- Here you can add a new custom field, and give it a name and a value
- This panel uses the `add_post_meta` function to add the metadata to the post

### Pre-populated field names for the Custom Fields panel

It is also possible to populate the Name field of the Custom Fields panel with a list of predefined meta fields.

To do this, you need to hook into the `postmeta_form_keys` filter and add the names of the meta fields that you want to display in the `Custom Fields` panel.

- The `postmeta_form_keys` filter is fired before the HTML of the Custom Fields panel is rendered, and passes in two parameters: an array of meta keys, and the `$post` object
- If no other keys are defined, a query will be run to fetch the keys of any existing metadata for the post
- So by updating the array of meta keys, you can add meta field keys to the Custom Fields panel to make it easier for your users to add the correct metadata

```php
function bookstore_add_isbn_to_quick_edit( $keys, $post ) {
  if ( $post->post_type === 'book' ) {
    $keys[] = 'isbn';
    }
    return $keys;
}
add_filter( 'postmeta_form_keys', 'bookstore_add_isbn_to_quick_edit', 10, 2 );
```

### Custom Meta Boxes

Another way to allow site administrators to add post meta is to use custom meta boxes. Working with custom meta boxes however also requires a good understanding of developing with security in mind, but for now you can read about them in the [Custom Meta Boxes](https://developer.wordpress.org/plugins/metadata/custom-meta-boxes/) page in the Plugin developer handbook

## Enqueuing CSS or JavaScript

- https://learn.wordpress.org/lesson/enqueuing-css-or-javascript/
- if you need to make use of custom CSS or JavaScript, you need to follow a process called enqueuing
- In order to add custom CSS or JavaScript, a WordPress plugin needs a way to add script or style tags to the HTML being rendered
- to start you need to register a callback function on a specific hook and use the callback to enqueue your scripts or styles
- The correct hook to use is the `wp_enqueue_scripts` action hook, e.g.

```css
.single-book h1 {
  color: red;
}
```

- Any time a single book is rendered, it will add the single-book class to the body element of the HTML page
- use `wp_enqueue_style` function
- At minimum, you need to pass at least the first two arguments to the function
  - the handle, a unique name for the stylesheet that’s used when the stylesheet is added to the HTML
  - the src, which is the full URL of the stylesheet, or path of the stylesheet relative to the WordPress root directory.
- For a plugin, you can use the plugins_url function to get the URL of the plugins directory, and then concatenate that with the path to your CSS file
- During a WordPress request, this will add the stylesheet handle and URL to a `wp_styles` object
- WordPress will loop through each stylesheet in the `wp_styles` object, and output an HTML style element

### Enqueuing JavaScript

- instead of using `wp_enqueue_style`, you can use `wp_enqueue_script`
- you pass a **_unique handle_** and src arguments to `wp_enqueue_script` for it to enqueue your JavaScript file

```php
/*
  wp_enqueue_style( string $handle, string $src = ”, string[] $deps = array(), string|bool|null $ver = false, string $media = ‘all’ )
*/
add_action( 'wp_enqueue_scripts', 'bookstore_enqueue_scripts' );
function bookstore_enqueue_scripts() {
    wp_enqueue_style(
        'bookstore-style',
        plugins_url() . '/bookstore/bookstore.css'
    );
    wp_enqueue_script(
        'bookstore-script',
        plugins_url() . '/bookstore/bookstore.js'
    );
}
```

- `wp_enqueue_script` will add the script handle and URL to a `wp_scripts` object, and output an HTML script element for each one, using the handle in the `id` attribute and the URL in the `src` attribute

### Enqueuing on the admin dashboard

You can also enqueue styles and scripts on the admin dashboard, using the `admin_enqueue_scripts` action instead of the wp_enqueue_scripts action

```php
add_action( 'admin_enqueue_scripts', 'bookstore_admin_enqueue_scripts' );
function bookstore_admin_enqueue_scripts() {
  // code here
}
```

- Once you’ve registered the callback function on the hook, the process of enqueuing scripts and styles is the same as for the front end using wp_enqueue_style and wp_enqueue_script

### Selective Enqueuing

In the examples in the lesson, the bookstore CSS and JavaScript is enqueued on every page of the site. This is not ideal. In the case of the CSS for example, it’s specifically targeting h1 elements on the single book view, so you don’t need to enqueue the CSS for anything other than books.

It is possible to perform selective enqueuing, where you determine the specific scenario when the file should be enqueued.

For example, in the case of the bookstore.css, you could use the WordPress `is_singular()` function to check if the content being rendered is a book custom post type

There are a number of other ways to make sure that your plugin stylesheet or script files are only loaded when needed. Doing this means that your plugin won’t add any unnecessary overhead or loading times to any WordPress site it’s installed on

```php
add_action( 'wp_enqueue_scripts', 'bookstore_enqueue_scripts' );
function bookstore_enqueue_scripts() {
    if ( ! is_singular( 'book' ) ) {
        return;
    }
    wp_enqueue_style(
        'bookstore-style',
        plugins_url() . '/bookstore/bookstore.css'
    );
    wp_enqueue_script(
        'bookstore-script',
        plugins_url() . '/bookstore/bookstore.js'
    );
}
```
