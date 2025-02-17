# WordPress Hooks

## WordPress Hooks

- One of the most regularly used developer features in WordPress is its Hooks system.
- Hooks are what make WordPress so extendable and allow you to build anything on the foundation of WordPress, from a blog to an online ecommerce platform
- Hooks allow your theme or plugin code to interact with or modify the execution of a WordPress request at specific, predefined spots.
- There are two types of hooks, action hooks, and filter hooks. These are more commonly known as actions and filters
- in the `wp-settings.php` file ~ line 643 is `do_action( 'init' );`
  - the `do_action` function defines an action hook, with the hook name `init`
  - see the [docs](https://developer.wordpress.org/reference/hooks/init/) to learn more about this
  - As a developer, you can hook into this action and run your own code when this init action is fired
  - It’s essentially like being able to add your own code inside the wp-settings.php file at that point, but without actually modifying the core file

You can use hooks in your WordPress themes and plugins to add your own functionality to WordPress, or to modify the default functionality

To see this in action, browse to your `wp-content/plugins` directory, and create a new file called `wp-learn-hooks.php` then add:

```php
<?php
/**
 * Plugin Name: Thanks For Reading
 * Description: A simple plugin to demonstrate how to use hooks in WordPress.
 * Version: 1.0
 */

add_filter( 'the_content', 'wp_learn_amend_content' );

function wp_learn_amend_content( $content ) {
    return $content . '<p>Thanks for reading!</p>';
}
```

- Then activate your plugin that ads to pages as well though
- that is a filter hook to modify a post
- I created a folder `thanks-for-reading` with `thanks-for-reading.php` inside

## Action Hooks

- actions allow you to perform some action at a specific point during the execution of a WordPress request, for example
- When developing a WordPress theme, it’s possible to enable support for different post formats
- Depending on the chosen post format, a different template layout can be rendered, displaying the post in a different format
- To enable post formats, the documentation indicates you need to use the `add_theme_support` function, and recommends that this be registered via the `after_setup_theme` action hook
- This hook is defined in the `wp-settings.php` file, after the theme is loaded: `do_action( 'after_setup_theme' );`
- Here the `do_action` function defines the action hook, with the hook name `after_setup_theme`
- this hook is fired during each page load, after the theme is initialized, and is used to perform basic setup, registration, and initialization actions for a theme

Using action hooks

- In order to make use of an action, you register a function in your code to a pre-existing action hook, which is known as a callback function
- To register your callback function on an action you use the WordPress `add_action` function
- You will need to pass the hook name and the name of your callback function as arguments to the `add_action` function
- you can use actions to perform something, either enabling some already existing feature, or adding something to the request execution

```php
add_action( string $hook_name, callable $callback, int $priority = 10, int $accepted_args = 1 )
```

## Filter Hooks

- Filters allow you to modify, or filter, some data at a specific point, which will be used later on
- In order to make use of a filter, you register a function in your code to a pre-existing filter hook, which is known as a callback function
- look at a filter called `the_content`
- This filter is defined in the `wp-includes/post-template.php` file, inside the function which is used in theme templates whenever the template needs to render any post or page content

```php
$content = apply_filters( 'the_content', $content );
```

- Here the `apply_filters` function defines the filter hook, with the hook name of `the_content`
- You will notice that a `$content` variable is passed as an argument of `apply_filters` and that the value of `apply_filters` is assigned back to a variable, in this case, again, the `$content` variable
- If we look a little higher in this function, the `$content` variable is assigned the value of the `get_the_content` function, which is a WordPress core function that retrieves the value of the `post_content` field for the current post or page in the posts table.
- So the `apply_filters` function registers the filter hook, passes the value of `$content` at this point in the code execution to any callback functions registered on this hook, and requires the updated value to be passed back

Using filter hooks:

- To register your callback function on a filter you use the WordPress `add_filter` function
- You will need to pass the hook name and the name of your callback function as arguments to the `add_filter` function
- in functions.php:

```php
add_filter( 'the_content', 'wp_learn_amend_content' );

// adding some text in a paragraph block, which renders at the bottom of each post on the front end
function wp_learn_amend_content( $content ) {
    $additional_content = '<!-- wp:paragraph --><p>Filtered through <i>the_content</i></p><!-- /wp:paragraph -->';
    $content = $content . $additional_content;

    return $content;
}
```

- You don’t have to name the argument the same as the variable name passed from the filter, but it does make it easier if you do

> It’s very important to always return something back from a filter callback, ideally, the modified content of the variable passed to the filter. Not returning something will cause a fatal error on your WordPress site

## Working with hooks

Besides knowing how to register a callback function to a hook, there are a few other things you need to know about working with hooks in WordPress

### Hook Priority

- ...additional function parameters...
- The third parameter is the hook priority (`add_action` and `add_filter`), which is an integer which defaults to `10`. This means if you register an action in your code without specifying a priority, it will be registered with a priority of `10`
- Hook priority allows you to determine the order in which your hook callback is run, relative to any other hook callbacks that may be registered on the given hook, either by WordPress core, or other themes or plugins
- Hooks run in numerical order of priority, starting at 1. It’s usually safe to leave the priority to the default of 10, unless you specifically want to change the order in which your callback function is run.
- Because WordPress core registers any hook callbacks with the default priority of 10, if you specify a priority of 11, you can make sure my callback function is run after any core callbacks have completed
- Alternatively, if you want to make sure the callback is run before WordPress core’s, you would set a lower priority, say 9.

```php
add_action( 'after_setup_theme', 'wp_learn_setup_theme', 11 );
```

- Often you might see callbacks being registered with a high priority, like 99, or 9999
- This is because the plugin or theme developer wants to be sure that this callback is run after all other callback functions. However, one can never know at what priority other third-party plugins or themes might register their callbacks

### Hook Parameters

- The fourth parameter in the `add_action` and `add_filter` functions is the number of accepted arguments the callback function can accept
- take a look at a content-related filter hook, `get_the_excerpt`
- The filter is defined in the `wp-includes/post-template.php` file and is defined in the `get_the_excerpt` function, which in turn is called from the `the_excerpt` function
- The apply_filters function is registering the filter hook with two variables that are associated with the filter, the `$post_excerpt` string variable and the `$post` object

```php
return apply_filters( 'get_the_excerpt', $post->post_excerpt, $post );
```

- When defining an action or filter hook, any number of possible arguments can be added. However, the number passed to the accepted arguments parameter determines how many of them are passed to the hook callback function
- If you look at the documentation for `add_filter` you will see the default value for number of accepted arguments is `1`, which means that if you don’t specify a value for this parameter, the first argument will be available to be passed to the callback function.
- In the get_the_excerpt filter, there are two possible variables to be accepted.
- If you were to register the callback without setting the number of arguments, only the first will be available in the callback function, in this case, the `post_excerpt`.
- In order to accept more of the available arguments, you need to specify the number of arguments to accept
- Then you can use those arguments in your callback function

```php
add_filter( 'get_the_excerpt', 'wp_learn_amend_the_excerpt', 10, 2 );
function wp_learn_amend_the_excerpt( $post_excerpt, $post ) {
  // code here
}
```

- Being able to determine which arguments you need for your callback function, and setting the number in the hook registration is a valuable skill

### Hook Order

- Depending on your specific requirements, you may first need to determine which action or filter is the correct one to use
- the WordPress Developer documentation has a page on [Hooks](https://developer.wordpress.org/apis/hooks/) in the Common APIs section, which contains a list of all action and filter hooks, and in the order that they are run during different requests on a WordPress site

> You can use this list to check when the hook you want to use is run, and then use this information to determine if it’s the correct hook for your requirements
