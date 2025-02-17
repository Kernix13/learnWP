# An introduction to developing for WordPress securely

## Securely developing plugins and themes

- https://learn.wordpress.org/lesson/securely-developing-plugins-and-themes/

Summary:

- `Sanitization` (always sanitize early): sanitize_text_field, sanitize_email
- `Validation`: (int)
- `Escaping` (always escape late): esc_html(), esc_html_e = `esc_html(__)`, esc_attr(), esc_url(), esc_textarea(), wp_kses(),
- `Nonce`: wp_nonce_field, wp_verify_nonce, wp_nonce_url, wp_create_nonce, check_admin_referer
- `Authentication`: current_user_can

1. learn the benefits of ensuring your code is secure,
2. what steps to follow to secure your code, and
3. where to find more information around developing with security in mind

### Disclaimer

The code used in this lesson is very simplified. You should not use any of the code used in this tutorial in your plugins or themes. Please make sure to read the full documentation on [Security](https://developer.wordpress.org/apis/security/) in the WordPress Developer handbook.

### What is developing with security in mind?

Developing with security in mind is the process of ensuring your code not only works but also does not introduce any security vulnerabilities

When writing code, it's important to develop a security mindset and to think about how your code could be used maliciously.

- Don't trust any data, whether it's user input, third-party API data, _or even data in your database_. Always be checking to make sure it's valid and safe to use.
- WordPress has a number of APIs that can help you with common tasks, such as sanitizing user input, validating data, and escaping output. _Rely on using these APIs to help validate and sanitize your data instead of writing your own functions_.
- `Keep up to date with common vulnerabilities and keep your code up to date to prevent them`.

### Where does security fit in the development process?

- Security should be a consideration at every stage of the development process
- the largest number of security vulnerabilities that are found take place at the PHP layer, which is executed on the server

### Sanitizing inputs

One of the first steps to take when developing is to ensure that any user input is sanitized. This means that any data that is being passed from the user, such as a form submission, or a URL parameter, is checked to make sure it's safe to use

- sanitize_text_field() and sanitize_email()

```php
// instead of
$name = $_POST['name'];
$email = $_POST['email'];
// Sanitize before inserting into the database
$name = sanitize_text_field( $_POST['name'] );
$email = sanitize_email( $_POST['email'] );
```

> Notice that the code follows a key principle of sanitizing data, in that you do so _as early as possible_

- check out the [Sanitizing Data](https://developer.wordpress.org/apis/security/sanitizing/) page in the WordPress Developer Documentation

### Validating Data

Validating data is the process of testing it against a predefined pattern (or patterns) with a definitive result, either valid or invalid.

Untrusted data can come from many sources, users, third-party API data, even your database data can be considered untrusted, especially if something else has modified it. Even site admins can make a mistake and enter incorrect or insecure data

```php
add_action( 'wp_ajax_delete_form_submission', 'wp_learn_delete_form_submission' );
function wp_learn_delete_form_submission() {
    if ( ! isset( $_POST['id'] ) ) {
        wp_send_json_error( 'Invalid ID' );
    }
    $id = $_POST['id'];

    global $wpdb;
    $table_name = $wpdb->prefix . 'form_submissions';

    $sql    = "DELETE FROM $table_name WHERE id = $id";
    $result = $wpdb->get_results( $sql );

    return wp_send_json( array( 'result' => $result ) );
}
```

Here the ID is being used directly in the SQL query, without any validation. Again, this means that if a user were to submit an ID of 1; DROP TABLE form_submissions; the same SQL DROP query would be run after the delete, and the table would be dropped

To prevent this, you can use PHP’s type-casting functionality, to ensure that the value of $id is always an integer value. This can be done by adding (int) before the variable name: $id = (int) $\_POST['id'];

Note that this will only work if the first character in the string passed via the `$_POST` array can be cast as an integer, otherwise the value of $id will be 0

```php
if ($id === 0){
  // return early with an error
  return wp_send_json( array( 'result' => 'Invalid ID passed' ) );
}
```

- check out the section on [Validating Data](https://developer.wordpress.org/apis/security/data-validation/) in the WordPress Developer Documentation

### Escaping outputs

Another aspect of security is to ensure that any information you output to the browser is safe, including any text, HTML or JavaScript code, or data from the database

Even if your code is not responsible for the source of the data being displayed, it is responsible for displaying it safely

- esc_html()
- (int)
- check out the section on [Escaping Data](https://developer.wordpress.org/apis/security/escaping/) in the WordPress Developer Documentation

> Notice that this code follows a key principle of escaping data, in that you _escape the data as late as possible_

### Preventing invalid requests

Whenever a request is made, it's important to check that the request is valid. This means checking that the request is coming from a trusted source

For example, you might have a shortcode that renders a form, where users can submit their information

When the user submits the form, the data is sent to the server. The data is then processed, sanitized, and stored in the database

Because the form might appear on any page where the shortcode is used, it's possible that a malicious user could attempt to send a POST request to the form, either looking for a vulnerability in the plugin, or by sending multiple requests to the form

To prevent this, you can check that the request is coming from a trusted source. To do this, you can implement something called a `nonce`, or a number used once

First, in the form itself, you can add a nonce field by using the `wp_nonce_field` function, and passing a nonce action and nonce name to the function

When the form is rendered on the front end, a hidden field is added to the form, using the nonce name as the id and name attribute of the hidden field, and the generated nonce as the field value. This data is posted when the form is submitted.

Then, in the function that processes the form data, you can verify that the nonce is valid by using the `wp_verify_nonce` function, and by passing the POSTed nonce field and the nonce action to this function. If the result of this verification is false, you can exit early, preventing any further code execution

> Any time your code makes a web request, be it via redirection to a new URL, POSTing data to a form, or making an AJAX request, you should check that the request is valid

- check out the section on [Nonces](https://developer.wordpress.org/apis/security/nonces/) in the WordPress Developer Documentation

### Preventing unauthenticated users

Depending on your code's functionality, it's a good idea to restrict certain features only to users with a specific permission level. For example, you may have a function that deletes data from the database.

While you might do your best to prevent anyone who doesn't have permission to run this function, it's still a good idea to include checks against this situation

WordPress includes a robust [User Roles and Capabilities](https://developer.wordpress.org/apis/security/user-roles-and-capabilities/) system, which allows you to either use the default user roles and capabilities or create custom ones

```php
if ( ! current_user_can( 'manage_options' ) ) {...}
```

. . . . . . .

## Fixing common security vulnerabilities

- https://learn.wordpress.org/lesson/fixing-common-security-vulnerabilities/
- learn how to apply the above principles when developing your WordPress plugins and themes, by fixing an insecurely coded form submission plugin

. . . . .

### The badly coded form submission plugin

- download the [Learn Plugin Security plugin](https://github.com/wptrainingteam/beginner-developer/blob/main/wp-learn-plugin-security.1.0.0.zip), and install the plugin to your local development environment
- open the main plugin file in your code editor, and take a look at the code

### SQL Injection

- The first common vulnerability
- SQL injection happens when values being inputted are not properly sanitized allowing for any SQL commands using the inputted data to potentially be executed on the database
- look at the wp_learn_maybe_process_form Fx

1. make sure that any `$_POST` data is sanitized before being used in the query
2. either use the `wpdb` prepare or insert functions

This will ensure that the name and email field values are both sanitized as they are accepted from the form submission request and that they are sanitized before being used to store the record in the database. While this might seem like overkill, if you just sanitize the inputs, and the code is later changed to use the values in a different way, you could still be vulnerable to a SQL injection

- wp_learn_delete_form_submission Fx - same as above except `wpdb` prepare or delete functions

### Cross-Site Scripting (XSS)

- The next common vulnerability
- Cross-Site Scripting (XSS) happens when a nefarious party injects JavaScript into a web page, which can be used to launch multiple different attacks or malicious activities from the website
- You can avoid XSS vulnerabilities by escaping output, stripping out unwanted data.
- Your code should escape dynamic content with the proper function depending on the type of the content being escaped
- look at some places where data is being outputted, and make sure it’s being escaped properly
- The first place is in the wrapper div of the wp_learn_form_shortcode shortcode callback
- Here the class attribute of the div is rendered based in the attributes passed to the shortcode. This is a potential XSS vulnerability, as the class attribute is not escaped - use `esc_attr`
- Next, we have the wp_learn_render_admin_page function, which renders the admin page - escape `$submission->name`, `$submission->email`, and `$submission->id` - use `esc_html` and `(int)`

### Cross-site Request Forgery (CSRF)

- Cross-site request forgery. CSRF is when a nefarious party tricks a user into performing an unwanted action within a web application they are authenticated in
- When developing with WordPress, becoming familiar with WordPress nonces is a must to help prevent CSRF
- a nonce provides a way to verify that the origin of the request is legitimate.

1. You create a nonce when you need to verify that the request is legitimate.
2. You output or pass the nonce to wherever needs to make a request
3. You verify the nonce when the request is made.

- There are two possible CSRF vulnerabilities in this plugin
- The first is when the form is submitted, and the data is processed
- we need to add a nonce to the form being rendered in the shortcode, and then verify it when the form is submitted.
- In the form, we use the `wp_nonce_field` function to add a hidden field with the nonce
- Notice how you pass in an action and a name. The action is used to identify the nonce, and the name is the name of the field that will be added to the form.- If you inspect the form, you can see the nonce field, which uses the name you passed to the function, and the nonce value.- Then in the form submission function, you verify the nonce, using the `wp_verify_nonce` function, passing in the value of the nonce field, and the action
- The other place we need to prevent CSRF is in the Ajax callback used to delete a form submission: wp_learn_delete_form_submission
- we need to manually create a nonce using `wp_create_nonce` and then pass the nonce to the JavaScript layer using `wp_localize_script`
- Then, we need to include the nonce in the jQuery POST request
- Note how we specify the nonce in the POST request as \_ajax_nonce. This is the name of the nonce that WordPress expects when processing an Ajax request.
- Lastly, in the Ajax callback, we verify the nonce, using the handy `check_ajax_referrer` function

### Broken Access Control

- BAC is when a user is able to access a resource they should not be able to access
- we have a broken access control vulnerability in Ajax function, at the present moment, anyone could make a request to the Ajax request URL with the right data, and it would delete a form_submission
- we can use the WordPress Roles and Capabilities API to check that the user has the correct permissions to delete a form submission: `current_user_can`
- Note that we’re doing two checks here, one against CSRF and one for access control. In this example, the order of execution is not super important, but in general, it’s a good idea to check for CSRF first, and then check for access control

### Bonus round – Open Redirect

It’s a tough one to spot, but all instances of `wp_redirect` should be replaced with `wp_safe_redirect`. This is because the code is redirecting to a local URL, and `wp_safe_redirect` checks whether the `$location` its using is an allowed host if it has an absolute path. This prevents the possibility of malicious redirects if the redirect `$location` is ever attacked.

. . . . .

## Tools to detect security vulnerabilities

- https://learn.wordpress.org/lesson/tools-to-detect-security-vulnerabilities/

### Plugins

1. [Plugin Check](https://wordpress.org/plugins/plugin-check/) (`plugin-check.1.3.1.zip`) is a WordPress plugin that you can use to test whether your plugin meets the required standards for the WordPress.org plugin directory, with one of those requirements being that your plugin code is secure - you can access the Plugin Check admin page from the Tools menu in your WordPress admin dashboard - Select the plugin you want to test, and make sure the Security checkbox is checked - The results are displayed in a table, with a list of issues that need to be addressed, including file names and line numbers
2. [Theme Check](https://wordpress.org/plugins/theme-check/) (`theme-check.20231220.zip`): Once this plugin is installed, you can access the Theme Check admin page from the Appearance menu in your WordPress admin dashboard - you select the theme to be checked, and click the Check it! button to run the test. The results are displayed at the bottom of the page, with a list of issues that need to be addressed

I also have in WebDev/wordpress/plugins

1. `plugin-inspector.1.5.zip`
2. `theme-check.zip` (same as above? YES)
3. `theme-sniffer.zip`

### Command line

1. [PHP_CodeSniffer](https://github.com/PHPCSStandards/PHP_CodeSniffer) with the [WordPress Coding Standards](https://github.com/WordPress/WordPress-Coding-Standards) rules - This combination not only checks your code against the WordPress Coding Standards **but also checks for security vulnerabilities** - To use PHP_CodeSniffer with the WordPress Coding Standards, you need to install Composer, which is a dependency manager for PHP projects - For Composer to work, you also need PHP installed on your computer, so that you can use the PHP CLI binary, which allows you to run PHP scripts in the terminal, instead of just in a browser

### Code Editor

- Visual Studio Code has a number of extensions that run the PHP_CodeSniffer tool inside the editor - search "phpcs" for an extension: phpcs: by `shevaua`
- Additionally, there are third party services that can scan your code for vulnerabilities inside your code editor, like [Sonar's](https://www.sonarsource.com/) SonarLint tool - SonarLint is entirely free for all open-source projects. You only pay if you want to analyze private repositories - SonarLint is entirely free for all open-source projects. You only pay if you want to analyze private repositories
- `SonarQube for IDE` is available as a plugin for Visual Studio Code

### OWASP

OWASP is a nonprofit foundation that works to improve the security of software. They provide a number of resources, including the [OWASP Top 10](https://owasp.org/www-project-top-ten/), which is a list of the top 10 most critical security risks to web applications

> wordpress/local/twenty24/app/public/wp-content/plugins
