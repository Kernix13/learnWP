# Advanced Theme Development

## Child themes

> https://learn.wordpress.org/lesson/child-themes/

Sometimes, you may need a way to modify or extend an existing theme, without making changes to the theme's code. This is where child themes come in

### What is a child theme?

A child theme is an extension of its parent theme.

Using a child theme allows you to extend or modify any part of the parent theme, without making any changes to the parent theme code.

### Why use a child theme?

...change the footer credit to reference your company name and update the URL...what if you wanted to reuse those same changes on a different site? You would have to manually make these changes in the Site Editor every time

By creating a child theme, which includes only the specific changes you need, you can activate the child theme, and the change will be applied

If there are any future updates to the parent theme, the modifications in the child theme will still be applied, and the changes will remain

### Creating a child theme

In the wp-content/themes directory, create a new empty theme directory called twentytwentyfourchild.

Inside that directory, create a style.css file. Then, add the following Theme header to that file

```css
/**
 * Theme Name: Child theme of Twenty Twenty-Four
 * Template:   twentytwentyfour
 */
```

- activate the child theme

### How child themes work

All WordPress themes — unless they are specifically a child theme — are technically parent themes

Child themes are slightly different to parent themes in that they have a special theme header field in the style.css file that defines which parent them they are a child of

This header field is the `Template` field. The value of this field must match the folder name (or slug) of the parent theme, relative to the wp-content/themes directory

This is also sometimes referred to as the theme's slug.

Then select which specific parts of the parent theme you want to modify

if you just want to modify the footer, you can create a new footer.html file in the child theme directory, in the same relative location as the footer.html in the parent theme, and make the changes you need to the child theme footer.html

One way to generate the child theme footer, is to make the changes you need to the footer template in the Site Editor.

Then, switch to the Code Editor view, copy the code, and paste it into the child theme `footer.html` file.

It's worth noting that a child theme can extend practically every part of its parent theme, not just templates. You can extend template parts, patterns, styles, and even custom theme functionality via a child theme

### Using Create Block Theme

While it's possible to create a child theme manually, you can also use the Create Block Theme plugin to create a child theme, based on changes you've made in the Site Editor

open the Create Block Theme options by clicking on the Create Block Theme icon in the top right corner of the Site Editor

Select Create Theme, and then Create Child Theme.

Give the child theme and name, and optionally add any relevant theme meta data.

Then click Create Child Theme.

The Child Theme will be created, and the Editor will be reloaded.

If you navigate to the Themes page in the WordPress admin area, you'll see the new child theme listed there, installed and activated.

And finally, if you look in your code editor, you'll see the child theme files have been created.

Check out the [Child themes page](https://developer.wordpress.org/themes/advanced-topics/child-themes/) under Advanced Topics in the Theme Developer Handbook

. . . . . . .

## UI Best Practices

> https://learn.wordpress.org/lesson/ui-best-practices/

### What is User Interface Design?

The User Interface (UI) of a website is the space where interactions between humans and your website occur. This is more commonly known as the website front end

The goal of good user interface design is to allow for effective interactions, also known as a good user experience (UX), so that the website provides good feedback that aids the user's decision-making process.

Bad user interface design can lead to a frustrating user experience and a potential loss of site visitors. When designing a theme, it's important to ensure that the elements of the theme provide a good user experience

### Logo Homepage Link

The logo of your theme should link to the homepage of your site. If you are using the `custom_logo()` function in a classic theme, or the `site logo block` in a block theme, the logo is automatically linked to the homepage - you should ensure that the logo links to the homepage:

```php
<a href="<?php echo esc_url( home_url( '/' ) ); ?>">
    <img src="<?php echo get_stylesheet_directory_uri(); ?>/logo.png" alt="<?php esc_attr_e( 'Home Page', 'textdmomain' );?>" />
</a>
```

### Descriptive Anchor Text

When creating links to things that appear in your theme, make sure to use descriptive anchor text.

The anchor text is the visible text for a link. Descriptive anchor text should give the reader an idea of the action that will take place when clicking it.

```html
<!-- bad anchor text -->
The best way to learn WordPress is to start using it. To Download WordPress,
<a href="https://wordpress.org/download/">click here</a>.
<!-- good anchor text -->
The best way to learn WordPress is to start using it.
<a href="https://wordpress.org/download/">Download WordPress</a> to get started.
```

### Style Links with Underlines

While on the topic of links, good theme design means retaining the default link style displaying with underlines.

Some designers use CSS to disable underlines for links. However, doing so causes usability and accessibility problems, as it makes it more difficult to identify hyperlinks from the surrounding text.

### Different Link Colors

The use of color on links is a visual cue that text is clickable.

HTML links are one of the few elements that have states. The two primary states are visited and unvisited. Visited means the user has clicked on the link and visited the page it points to, and unvisited means the user has not yet clicked on the link.

By default, unvisited/default links are blue, and `:visited` links are purple.

Having different colors for these two states helps users identify the pages they've visited before.

Additionally, are 3 other states that links can have:

- `:hover`, when a mouse is over an element
- `:focus`, similar to hover but for keyboard users
- `:active`, when a user is clicking on a link

Since hover and focus have similar meanings, sometimes designers give them the same styles.

However, hover and focus have different interaction patterns.

If you choose a subtle hover state, you should have a more easily identifiable focus state.

Hovering over a link is a directed activity, where the user knows where they are in the page and only needs to identify whether that spot is linked.

Focus is an undirected activity, where the user needs to discover where their focus has moved to after shifting focus from the previous location.

Notice how the menu links in the Twenty Twenty-Four theme add the underline style when hovering over them with the mouse, but have a border when focus changes via the keyboard.

### Color Contrast

WebAIM, a non-profit web accessibility organization, provides a color [contrast calculator](https://webaim.org/resources/contrastchecker/) to help you determine the contrast in your website design.

You can enter the background color and foreground color to see if the contrast ratio meets the Web Content Accessibility Guidelines (WCAG) 2.0.

The WCAG 2.0 requires a ratio of 4.5:1 on normal text to be AA compliant.

### Sufficient Font Size

Make your text easy to read.

By making your text large enough, you increase the usability of your site and make the content easier to understand. 14px is the smallest text should be.

### Associate Labels with Inputs

When working with elements that accept input, make sure to associate labels with inputs using the for attribute. This will allow the user to click the label and focus on the input field.

```html
<!-- the label "for" attr needs to equal the input "name" attr -->
<label for="name">Name</label>
<input type="text" id="name" name="name" placeholder="John Smith" />
```

### Placeholder Text

Developers will often use placeholders on input elements to show the user an example of what to type.

```html
<label for="name">Name</label>
<input type="text" id="name" name="name" placeholder="John Smith" />
```

When a user puts their cursor in the field and starts typing, the placeholder text will disappear.

However, when done incorrectly, placeholders can be a user experience and accessibility nightmare.

So make sure to use placeholders correctly, or not at all.

If you do decide to use a placeholder, make sure that it suggests the type of data a field requires, and not as a substitute for the field label.

### Descriptive Buttons

The web is filled with buttons that have unclear meanings. Remember the last time you used **'OK'** or **'submit'** on your login form?

Choosing better words to display on your buttons can make your website easier to use. Try the pattern `[verb] [noun]`. For example Submit Form, instead of just Submit.

This describes what will happen when the user clicks the button.

A great example of this is the comments form on the single post template, the use of Post Comment, instead of just Submit

Check out [UI best practices doc](https://developer.wordpress.org/themes/advanced-topics/ui-best-practices/) under the Advanced Topics section of the WordPress Theme Developer Handbook

. . . . . . .

## JavaScript in Themes

> https://learn.wordpress.org/lesson/javascript-in-themes/

JavaScript is a programming language that is used to add interactivity to web pages. Theme developers will often use JavaScript to provide interactivity, animation, or other enhancements to their themes...learn about using third-party JavaScript libraries, some best practices to follow when writing JavaScript, whether or not you should use jQuery, and where to find more information

### JavaScript libraries

If you need to use any third-party JavaScript libraries in your theme, make sure to check whether it's already available via the WordPress install.

WordPress includes several JavaScript libraries that you can use. These libraries are included with WordPress and are available for you to use in your theme.

A common mistake made by beginning theme developers is to bundle their theme with their own version of the library.

However, this may conflict with plugins that enqueue the version bundled with WordPress.

You can find a full list of the default Scripts and JavaScript Libraries included and registered by WordPress in the [wp_enqueue_scripts](https://developer.wordpress.org/reference/functions/wp_enqueue_script/#default-scripts-and-js-libraries-included-and-registered-by-wordpress) function reference.

### Writing JavaScript

for more common tasks, you may not need to use a JavaScript library at all, and can just write plain JavaScript. Here are some things to consider when writing your JavaScript:

1. Try to avoid using global variables.

- To avoid using global variables, you can use a number of alternatives, but the most straightforward is to use an Immediately Invoked Function Expression (IIFE). This allows you to define variables in a local scope, preventing them from polluting the global namespace

```js
(function () {
  var greeting = 'Hello, World!';
  console.log(greeting);
})(); // Outputs: "Hello, World!"
```

2. Keep your JavaScript unobtrusive

- Make sure your JavaScript doesn't interfere with the content of the page or produce unnecessary errors. This means that your JavaScript should be separate from your HTML, and should not rely on specific elements or classes in your HTML
- use the `addEventListener()` method to add the event listener, rather than using the `onclick` attribute in the HTML
- Additionally, you should check that the element exists on the page before adding the event listener.

```js
(function () {
  let button = document.getElementById('myButton');
  if (button) {
    button.addEventListener('click', function () {
      alert('Button clicked!');
    });
  }
})();
```

3. Use a coding standard.

- WordPress has a [JavaScript Coding Standard](https://developer.wordpress.org/coding-standards/wordpress-coding-standards/javascript/) that you can use to ensure that your code is consistent with the rest of the WordPress codebase

4. Validate and Lint Your Code

Use a linter to check your code for errors and potential issues. This can help to catch bugs early, and ensure that your code is consistent and easy to read.

[ESLint](https://eslint.org/) is a popular linter for JavaScript and can be used to check your code for errors and potential issues. It is possible to configure your theme to use EsLint to check your JavaScript code via the `@wordpress/scripts` [package](https://developer.wordpress.org/block-editor/reference-guides/packages/packages-scripts/).

5. Ensure your theme works without JavaScript

Ensure your site theme works without JavaScript first – then add JavaScript to provide additional capabilities. This is a form of [Progressive Enhancement](https://developer.mozilla.org/en-US/docs/Glossary/Progressive_Enhancement), which is a strategy that puts emphasis on web content first, allowing everyone to access the basic content and functionality of a web page

6. Asset loading

Use [Lazy loading](https://developer.mozilla.org/en-US/docs/Web/Performance/Lazy_loading) for assets that aren't immediately required. To do this, identify resources that are not critical for the content and load these only when needed

### jQuery

jQuery is a JavaScript library that saw an increased use in the early days of web development. However, with the improvements in JavaScript, it is often no longer necessary to use jQuery for many common tasks

Don't use jQuery if you don't need to — [You might not need jQuery](https://youmightnotneedjquery.com/) is a great site that shows you how to do many of these common tasks with plain JavaScript

A good example is if you need to make an AJAX request, you can use the `fetch()` method in plain JavaScript, or better yet, the WordPress `apiFetch` package

```js
// jQuery
$.ajax({
  url: 'https://example.com/wp-json/wp/v2/posts',
  success: function (data) {
    console.log(data);
  },
});

// Plain JavaScript
fetch('https://example.com/wp-json/wp/v2/posts').then(data =>
  console.log(data)
);

// apiFetch
apiFetch({ path: '/wp/v2/posts' }).then(posts => {
  console.log(posts);
});
```

If you must use jQuery in your theme, you should use the version of jQuery that is included with WordPress.

When enqueuing your theme's scripts, you should specify jQuery as a dependency, by including it in the dependencies array.

```php
add_action( 'wp_enqueue_scripts', 'my_theme_scripts' );
function my_theme_scripts() {
    wp_enqueue_script(
        'my-script',
        get_template_directory_uri() . '/js/my-script.js',
        array( 'jquery' ),
        '1.0',
        true
    );
}
```

This will ensure that jQuery is loaded before your script is loaded, and uses the version included with WordPress.

Because the copy of jQuery included in WordPress loads in noConflict() mode, you should also wrap your code in an Immediately Invoked Function Expression, or IIFE.

```js
(function ($) {
  // Your jQuery code goes here
})(jQuery);
```

Check out the [JavaScript Best Practices Handbook](https://developer.wordpress.org/themes/advanced-topics/javascript-best-practices) page under the Advanced Topics section of the WordPress Developer Handbook

. . . . . . .

## Build Process

> https://learn.wordpress.org/lesson/build-process/

When developing a WordPress theme, it's useful to consider whether you will need a build process to help you manage your theme's assets and optimize your theme for performance

### What is a build process?

A build process is a method of converting source code files into a final build/production version that can be read by the computer.

In particular, themes will most often be minifying or converting source code into CSS or JavaScript so that they can be read by the browser.

### Why use a build process?

Depending on what technologies you use in your theme, you may need a build process to help you manage your theme's assets and optimize your theme for performance.

For example, if you choose to use Sass for your styling, you will need a build process to compile your Sass files into CSS files that can be read by the browser.

**If you chose to write your JavaScript using the more modern syntax, you will need a build process to transpile your JavaScript files into a format that all browsers can execute**.

Even if you don't use these options, a build process can still be useful for optimizing your theme's assets, such as minifying your CSS and JavaScript files and optimizing images.

When creating a WordPress theme, you may find yourself in need of a build process to handle more complex projects. There are many systems to choose from, and you can use whatever you prefer.

But WordPress also offers the [@wordpress/scripts package](https://developer.wordpress.org/block-editor/reference-guides/packages/packages-scripts/) that you can be assured is continually updated and should cover most of your needs.

### Prerequisites

Most of WordPress theme development doesn't require any additional software. You just need a code editor, a local development environment, and a WordPress installation.

But to work with a build process, there are some other requirements:

- You need to have Node.js and npm installed on your local machine, which is also a requirement for building WordPress blocks.
- A basic understanding of webpack is also recommended.
- Some familiarity with the @wordpress/scripts package.

These are more advanced tools than what is normally required to build themes, but they are necessary if you want to work with the standard WordPress build process

### Setting up your files and folders

The @wordpress/scripts package was originally created for block development. Over time, it has evolved to also work with themes.

By default, it expects that development files live in the `/src` folder and will output build files in the `/build` folder.

However, most theme authors utilize a custom system for working with assets such as `/public` as opposed to `/build` and `/resources` as opposed to `/src`

### Setting up your package.json file

1. initialize the npm project: `npm init` - Once you have completed the setup, you will have a package.json file in the root of your theme
2. Next, you need to install the @wordpress/scripts package

```sh
npm install @wordpress/scripts path webpack-remove-empty-scripts --save-dev
```

3. Lastly, update the scripts section of the package.json file to include the following

```json
"scripts": {
  "start": "wp-scripts start --webpack-src-dir=resources --output-path=public",
  "build": "wp-scripts build --webpack-src-dir=resources --output-path=public"
},
```

- This creates two npm script commands, `start` and `build`, that will run the @wordpress/scripts package with the correct configuration for your theme
- In this case it will look for files in the resources folder and output them to the public folder
- If you have a different folder structure, you can adjust the `--webpack-src-dir` and `--output-path` parameters to match your setup

### Configuring webpack

The @wordpress/scripts package is built on top of webpack. If you were building a block, everything would already be in place for you.

However, because you are building a theme, you need to overwrite some default configuration of the @wordpress/scripts package with your own.

To do this, create a custom `webpack.config.js` file in the root of your theme.

```js
// WordPress webpack config.
const defaultConfig = require('@wordpress/scripts/config/webpack.config');

// Plugins.
const RemoveEmptyScriptsPlugin = require('webpack-remove-empty-scripts');

// Utilities.
const path = require('path');

// Add any new entry points by extending the webpack config.
module.exports = {
  ...defaultConfig,
  ...{
    entry: {
      'js/editor': path.resolve(process.cwd(), 'resources/js', 'editor.js'),
      'css/screen': path.resolve(
        process.cwd(),
        'resources/scss',
        'screen.scss'
      ),
      'css/editor': path.resolve(
        process.cwd(),
        'resources/scss',
        'editor.scss'
      ),
    },
    plugins: [
      // Include WP's plugin config.
      ...defaultConfig.plugins,

      // Removes the empty `.js` files generated by webpack but
      // sets it after WP has generated its `*.asset.php` file.
      new RemoveEmptyScriptsPlugin({
        stage: RemoveEmptyScriptsPlugin.STAGE_AFTER_PROCESS_PLUGINS,
      }),
    ],
  },
};
```

- The custom webpack config can be found in the [Configuring webpack section](https://developer.wordpress.org/themes/advanced-topics/build-process/#configuring-webpack) of the [Build process](https://developer.wordpress.org/themes/advanced-topics/build-process/) page under the Advanced Topics section of the WordPress Developer Handbook
- This configuration file sets up the entry points for your custom JavaScript and Sass files and tells webpack where to find them.
- It also configures the webpack-remove-empty-scripts, so that there are no leftover JavaScript files mapped to your CSS.

### Running the build process

- To start the development server, run the following command in your terminal: `npm run start`
- To build your theme for production, run the following command in your terminal: `npm run build`

### Loading scripts and styles

- When using a build process, you will need to enqueue the compiled files instead of the source files
- If you open up the public/js folder, you will see that the build process has created the following files:

  editor.js
  editor.asset.php

- The asset file returns a PHP array which contains an array of dependencies and a version number for the editor.js file.
- You can then use this array to enqueue the script in your theme.
- First, use the relevant hook and specify the hook callback in your functions.php file

```php
add_action( 'enqueue_block_editor_assets', 'themeslug_editor_assets' );
function themeslug_editor_assets() {
    $script_asset = include get_theme_file_path( 'public/js/editor.asset.php'  );

    wp_enqueue_script(
        'themeslug-editor',
        get_theme_file_uri( 'public/js/editor.js' ),
        $script_asset['dependencies'],
        $script_asset['version'],
        true
    );
}
```

The process is similar for any stylesheets you want to enqueue. Also refer to the [Build process](https://developer.wordpress.org/themes/advanced-topics/build-process/) page under the Advanced Topics section of the WordPress Developer Handbook

. . . . . . .

## Plugin API Hooks

> https://learn.wordpress.org/lesson/plugin-api-hooks/

- WordPress provides a number of hooks that allow plugins to “hook into” the functionality of WordPress.
- Your theme should support these hooks, to allow plugins developers to extend your theme

### A note on block themes

If you are developing a block theme, you should not have to worry about implementing these template tags.

The blocks that implement the functionality described in this lesson already support the relevant hooks.

> Using these template tags is only necessary if you are developing a classic theme, or custom functionality outside of the core blocks.

### Template tags

Most hooks are executed internally by WordPress, so your theme does not need special tags for them to work.

However, a few hooks need to be supported in specific theme templates.

These hooks are fired by specific template tags:

1. `wp_head()` fires the wp_head action, which is used by plugins to add code to the `<head>` section of your theme.

This tag should always at the end of the `<head>` element of a theme's `header.php` template file.

2. `wp_body_open()` fires the wp_body_open action, which is used by plugins to add code to the `<body>` element of your theme.

This tag goes at the beginning of the `<body>` element of a theme's `header.php` template file.

3. `wp_footer()` fires the wp_footer action, which is used by plugins to add code to the footer of your theme.

This tag should be in the theme's `footer.php` file, just before the closing `</body>` tag.

4. `wp_meta()` fires the wp_meta action. This action can have several purposes, depending on how you use it, but one purpose might be to allow for theme switching.

This tag typically goes in the `<li>`Meta`</li> `section of a Theme's menu or sidebar.

5. `comment_form()` is used to display the comment form at the end of posts

This tag goes in the `comments.php` template file, directly before the file's closing `</div>` tag.

. . . . . . .

## Testing your themes

> https://learn.wordpress.org/lesson/testing-your-theme/

Before releasing your theme to the public, you should test it thoroughly to ensure that it works as expected.

Some things you should do before releasing your theme:

- Testing your theme in a local development environment.
- Using the _Theme Test Data_ to ensure your theme can handle a variety of content.
- Useful plugins for debugging and testing.
- Tools for Accessibility and Performance testing.

### Testing your theme in a local development environment

One of the benefits of this is that you can enable the WordPress debugging options, and see if your theme generates any errors or warnings

### Using Theme Test Data

Part of testing your theme includes ensuring that it can handle a variety of content. By default, a new WordPress install only has a single sample page, post, and comment.

Instead of manually creating different types of content, you can download and install the WordPress project's [Theme Test Data](https://github.com/WordPress/theme-test-data/tree/master).

This test data includes a set of posts, pages, and other content that you can use to test your theme.

To install the Theme Unit Test Data, follow these steps:

1. Download the Theme Unit Test Data file from the GitHub repository by clicking on the Download raw file button and saving the file to your computer's hard drive.
2. In your WordPress admin, go to Tools > Import.
3. Under the WordPress section, click on Install Now. This will install the WordPress XML importer.
4. Once it's installed, click on the Run Importer link.
5. Click on the Choose File button, and select the Theme Unit Test Data file you downloaded earlier.
6. Click on the Upload file and import button.
7. Assign the content to an existing user or create a new user to assign it to, _and make sure to check the Download and import file attachments checkbox_. Then click on the Submit button.

Once the import is complete, you should see a variety of content on your site, including posts, pages, and other content types.

You can then test your theme with this content to ensure that it displays correctly.

### Useful plugins for debugging and testing

There are several community plugins that you can use during theme development to help you test and debug your theme.

During theme development, there are several plugins that you can use to help find and fix issues, including:

1. Query Monitor
2. Debug Bar
3. [Log Deprecated Notices](https://wordpress.org/plugins/log-deprecated-notices/)

When you're ready to distribute your theme, the Theme Check plugin evaluates your theme code against the WordPress Theme Review Guidelines.

Following these guidelines is a requirement for submitting a theme to the WordPress theme directory.

Even if you don't plan to distribute your theme through the theme directory, it's still a good baseline test of your theme's structure and code.

### Cross-browser testing

For effective cross-browser compatibility testing of block themes, it is important test your theme across all major browsers, including Firefox, Chrome, Safari, and Edge.

You can also use third-party tools like [BrowserStack](https://www.browserstack.com/) or [BitBar](https://smartbear.com/product/bitbar/) to test your theme on different browsers and devices.

Additionally, most modern browsers have developer tools that allow you to inspect everything about the pages being rendered, including JavaScript errors, network usage, and the performance of your theme.

Using the browser developer tools also allows you to use the responsive design mode, which offers you the option of testing your theme on different devices and screen sizes.

### Tools for Accessibility and Performance testing

Ensuring that your theme is accessible is a key aspect of responsible theme development.

You should strive to make sure your theme meets the [WordPress Accessibility Guidelines](https://wordpress.org/about/accessibility/). This includes aspects like keyboard navigation, screen reader compatibility, and proper use of ARIA roles.

You should also test your theme to ensure that it's not loading unnecessary resources, and that it's optimized for performance.

To test this, you can use tools like [Google Lighthouse](https://developers.google.com/web/tools/lighthouse), which can be run from ChromeDevTools, from the command line, or as a Node module.

You can also install your theme on a live website, and use tools like PageSpeed Insights, or GTmetrix to test your theme's performance. Be sure to not only test the homepage, but also other templates for things like pages and posts.

Check out the [Testing](https://developer.wordpress.org/themes/advanced-topics/testing/) page under Advanced Topics in the Theme Developer Handbook
