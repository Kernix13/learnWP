# Debugging in WordPress

## The built-in WordPress debugging options

- https://learn.wordpress.org/lesson/the-built-in-wordpress-debugging-options/

### What is debugging?

Debugging is the process of finding and fixing errors in your code.

As the two primary programming languages of WordPress are PHP and JavaScript, you need to be able to debug both.

With JavaScript code, which is executed in the browser, it’s fairly straightforward to use to console.log() to write messages to the browser console for the purposes of testing and debugging.

PHP on the other hand, is executed on the server and so you need ways to find out what’s happening when things go wrong.

### Debugging PHP

In WordPress, during any WordPress request lifecycle, the `wp_debug_mode()` function is run to set up the debugging environment. This function is located in the `wp-includes/load.php` file.

If you look at this code, you can see that if the `WP_DEBUG` constant is set to `true`, then it sets the PHP error reporting level to `E_ALL`, which means turn on all error reporting.

Additionally, if `WP_DEBUG_DISPLAY` is set to `true`, then it sets the display_errors PHP setting to 1, which means turn on the display of these errors on screen.

Finally, if `WP_DEBUG_LOG` is set to `true`, then it sets the `error_log` PHP setting to the `wp-content/debug.log` file. It is also possible to configure a custom `debug.log` file location, other than the default.

If this log file is enabled, it will set the PHP `log_errors` setting to `1`, and set the `error_log` setting to the path of the log file, meaning that all errors will be logged to this file.

Using this knowledge, you can configure your `wp-config.php` file to enable WordPress debugging

### Enabling debugging

To enable debugging, open the wp-config.php file and scroll down to where the `WP_DEBUG` constant is set:

```php
define( 'WP_DEBUG', true );
define( 'WP_DEBUG_DISPLAY', false );
define( 'WP_DEBUG_LOG', true );
```

This configuration will:

1. Enable debugging
2. Disable displaying errors on screen
3. Enable logging errors to the `wp-content/debug.log` file

Depending on your personal preference, you can enable displaying the errors on screen, but this can lead to the errors either being missed or overlaying other important content on screen, which is not ideal.

Additionally, if you’re ever debugging an issue on a production site, you don’t want to display errors on screen, as this can lead to sensitive information being displayed to the user

### Debugging with `error_log`

In addition to logging errors to the `debug.log` file, you can also log messages or variables to the `debug.log` file using the PHP `error_log` function.

This function accepts a single string parameter. For example, if you wanted to log a SQL query being run to the debug.log file, you could use the following code:

```php
error_log( $wpdb->last_query );
```

If you refresh the request and view the debug.log file, you see the query being logged to the file.

    [02-Jun-2023 13:55:35 UTC] SELECT * FROM wp_form_submissions

### Using the SAVEQUERIES constant

In addition to logging the last query, you can also log all queries that are run during a WordPress request lifecycle

To do this, you can enable the SAVEQUERIES constant in your wp-config.php file.

```php
define( 'SAVEQUERIES', true );
```

Once you’ve enabled this constant, you can log all queries by using the following code

```php
error_log( print_r( $wpdb->queries, true ) );
```

This uses the `error_log()` function combined with the PHP `print_r()` function to log the `$wpdb->queries` array to the `debug.log` file.

This array contains all the queries that have been run during the WordPress request lifecycle and is only available if the `SAVEQUERIES` constant is enabled.

> check out the [Debugging in WordPress](https://developer.wordpress.org/advanced-administration/debug/) section

. . . . . .

## Examining the state of your PHP code

- https://learn.wordpress.org/lesson/examining-the-state-of-your-php-code/

When you’re debugging PHP code, it can be helpful to examine the state of your code at a specific point in time. This can help you understand what’s happening in your code and identify any issues that may be causing problems.

### Using error_log() to log messages

As discussed in the lesson on the built-in WordPress debugging options, you can use the `error_log()` function to log messages to the WordPress debug.log file.

This can be useful for debugging purposes, as it allows you to see what’s happening in your code without displaying it on the screen.

The `error_log()` function is not specific to WordPress, it’s a PHP function that you can use in any PHP code to log messages to the PHP error log file configured on the server.

However, once you enable the WordPress specific debugging options in your wp-config.php file, anything passed to `error_log()` will be logged to the WordPress debug.log file.

```php
error_log( $some_variable );
```

This will log the value of $some_variable to the debug.log file, so you can see what it contains at that point in your code.

The benefit of using error_log() is that it allows you to log messages to a file without displaying them on the screen. If you display them on screen, especially in a production environment, you risk exposing sensitive information to users.

It’s also sometimes quicker to be able to see the output in a log file, rather than having to search through a long list of output on the screen

### Using print_r()

Another useful function for examining the state of your PHP code is `print_r()`. This function outputs the value of a variable, array, or object in a human-readable format, so you can see what it contains.

```php
$some_array = array( 'apple', 'banana', 'cherry' );
print_r( $some_array );
```

This code will output the following to the screen:

    Array ( [0] => apple [1] => banana [2] => cherry )

Developers will often wrap print_r() in `<pre>` tags to make the output easier to read

```php
echo '<pre>';
print_r( $some_array );
echo '</pre>';
```

Notice that by default print_r() outputs the value of the variable, but does not return it. If you want to use the output of print_r() with error_log(), you need to set the second parameter to true.

```php
error_log( print_r( $some_array, true ) );
```

### Using var_dump()

The var_dump() function is another useful function for examining the state of your PHP code. This function outputs the value of a variable, array, or object in a human-readable format, along with additional information about the variable type and length.

```php
$some_array = array( 'apple', 'banana', 'cherry' );
echo '<pre>';
var_dump( $some_array );
echo '</pre>';
```

    array(3) {
      [0]=>
      string(5) "apple"
      [1]=>
      string(6) "banana"
      [2]=>
      string(6) "cherry"
    }

Notice that var_dump() outputs the value of the variable, along with additional information about the variable type and length. This can be useful for debugging purposes, as it provides more detailed information about the variable than print_r().

Unlike print_r(), var_dump() does not have an option to return the output to a variable, so you can’t use it directly with error_log().

However, you can use something called output buffering to capture the output of var_dump() and then log it to the debug.log file.

```php
$some_array = array( 'apple', 'banana', 'cherry' );
ob_start();
var_dump( $some_array );
$output = ob_get_clean();
error_log( $output );

// Developers will often use this type of code in a special logging function, to be able to use both var_dump and error_log together.
function log_var_dump( $variable ) {
    ob_start();
    var_dump( $variable );
    $output = ob_get_clean();
    error_log( $output );
}
```

. . . . . .

## Examining the state of your JavaScript code

- https://learn.wordpress.org/lesson/examining-the-state-of-your-javascript-code/

### Server-side vs client side

One of the main differences between debugging PHP and JavaScript is that PHP is a server-side language, so you can log messages to a file on the server.

JavaScript, on the other hand, is a client-side language, so you can’t easily log messages to a file in the same way.

Fortunately, there are ways to examine the state of your JavaScript code using the browser’s Developer Tools, specifically the Console tab.

### Opening the browser’s developer tools

> skip

### The console object

...The console output also includes a link to the location of the code in the source file, which can be helpful for tracking down where the message was logged from.

You can also log more complex data types, such as arrays or objects

There are a number of other methods you can use to log messages to the console, such as `console.error()`, `console.warn()`, and `console.info()`.

One of the most underused methods is `console.table()`, which logs an array or object as a table, making it easier to read.

. . . . . .

## Useful debugging plugins

- https://learn.wordpress.org/lesson/useful-debugging-plugins/

### Debug Bar

[Debug Bar](https://wordpress.org/plugins/debug-bar/) is a plugin built and maintained by the WordPress developer community. It adds a debug menu to the admin bar that shows query, cache, and other helpful debugging information.

**When the WP_DEBUG constant is enabled, it also tracks PHP Warnings and Notices to make them easier to find, and when SAVEQUERIES is enabled, the MySQL queries are tracked and displayed**.

### Query Monitor

Another option is [Query Monitor](https://wordpress.org/plugins/query-monitor/), which also adds a debug menu to the admin bar and displays information about the current page request.

Query Monitor enables debugging of many things, including database queries, PHP errors, hooks and actions, block editor blocks, enqueued scripts and stylesheets, HTTP API calls, and more.
