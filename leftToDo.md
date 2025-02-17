# More courses

LEFT TO DO GO HERE

......................................................................

## 5. **WooCommerce 101: How to Set Up a Store**

> https://wordpress.com/learn/webinars/woocommerce-101-how-to-set-up-a-store/

> https://wordpress.com/learn/webinars/woocommerce-101-how-to-set-up-a-store/#tab-video-replay

- 1 hr 11 mins video
- `DONE` - see ecommerce/woocommerce.md

......................... MORE: MISC: ................................

## AI-Assisted WordPress

> https://wordpress.com/learn/webinars/ai-assisted-wordpress/

- 58:41
- `DONE` See ai/aiWP.md

....................................................................

## Unlocking the Power of AI

> https://wordpress.com/learn/courses/unlocking-the-power-of-ai/

- 4 modules, 15 lessons
- `DONE` See ai/unlockingAI.md

> EXCELLENT

.................... PLUGIN DEVELOPER VIDEOS ...........................

Dev - plugins:

1. Introduction to securely developing plugins: https://learn.wordpress.org/tutorial/introduction-to-securely-developing-plugins/

- `DONE` See pluginDev/securePlugins.md

2. Using the create-block Tool: https://learn.wordpress.org/tutorial/using-the-create-block-tool/

- `DONE` See pluginDev/create-block-tool.md

3. Converting a Shortcode into a Block: https://learn.wordpress.org/tutorial/converting-a-shortcode-into-a-block/

- `DONE` See pluginDev/shortcodeBlock.md

4. Styling your WordPress Blocks: https://learn.wordpress.org/tutorial/styling-your-wordpress-block/

- `DONE` See pluginDev/styleBlocks.md

5. WordPress Action Hooks: https://learn.wordpress.org/tutorial/wordpress-action-hooks/

- `DONE` See pluginDev/actionHooks.md

........................ REST API VIDEOS ...............................

Dev - REST API:

1. WordPress REST API – custom routes & endpoints: https://learn.wordpress.org/tutorial/wordpress-rest-api-custom-routes-endpoints/

- `DONE` See restAPI/routesEndpoints.md

2. WordPress REST API – Modifying responses: https://learn.wordpress.org/tutorial/wordpress-rest-api-modifying-responses/

- `SKIP FOR NOW` See restAPI/responses.md

3. WP REST API – custom fields, authentication, and testing: https://learn.wordpress.org/tutorial/wp-rest-api-custom-fields-authentication-and-testing/ - 16 mins

- `SKIP FOR NOW` See restAPI/authTest.md

........................ DEVELOPER COURSE ...............................

## 1. Different types of themes: Overview

> `DONE` https://learn.wordpress.org/lesson/different-types-of-themes-overview/

- 23 LESSONS, 5 MODULES

> Folder blockThemeDev - do this one next

........................ DEVELOPER COURSE ...............................

2. Introduction to Block Development: Build your first custom block: https://learn.wordpress.org/course/introduction-to-block-development-build-your-first-custom-block/

- 20 LESSONS, 5 MODULES

> Folder introBlockDev

> `SKIP FOR NOW`

........................ DEVELOPER COURSE ...............................

3. Developing your first WordPress block: https://learn.wordpress.org/course/developing-your-first-wordpress-block/

- 39 LESSONS, 6 MODULES

> Folder firstBlockDev

> `SKIP FOR NOW`

........................ DEVELOPER COURSE ...............................

4. Using the WordPress Data Layer: https://learn.wordpress.org/course/using-the-wordpress-data-layer/

- 6 LESSONS - building a small React app to manage WordPress pages

> Folder dataLayer - SKIP - not ready for `Redux`

........................................................................

**Blocks**

> `WATCH ALL OF THESE`!!!

........................................................................

## 📌 Cover Block

> https://learn.wordpress.org/tutorial/uncovering-the-cover-block/

- a cover block lets you display text on top of an image or video
- can be used for CTA's, parallax images, video banner, window effect, header

Key features & settings

- the cover block is a container block which means it can contain other blocks within it
- you can add a cover overlay
- the toolbar for it allows you to use the featured image
- /cover > add image > set to full-width > you can change the position of the text and set the image to full height
- you can add a duo-tone filter
- you can toggle on "Fixed background"

> That's not creating a fixed bg image, s\b: `background-attachment: fixed;`

Video banner:

- /cover - choose video - full width - - add a heading

> you can drag the image or video to be smaller or larger

Window effect:

- /columns, 2 cols > make the parent full width > select left column and add a cover block - duplicate that twice - then duplicate the entire column - delete 3rd empty col
- click on each cover block and select Fixed background

Headers

- header with a featured image - template parts > add new > select header > insert cover block > full height > add a row block > add site logo in it and nav block > space between > select the row and insert a spacer block after it and enlarge it to sen the row block to the top (seems wrong to do that) - for the nav dese;ect allow to wrap so that everything is on one line

........................................................................

## 1. Designing with the columns block 📌 ✅

> https://learn.wordpress.org/tutorial/designing-with-the-columns-block/

> GREAT!

- the columns block is a container block used for custom layouts
- up to 6 columns - creates a grid effect
- you can choose from preset columns of 1, 2, or 3 and with varying widths
- you can add other blocks into each column
- cards are a perfect example as are testimonials - a media and text block looks like a columns block but is not
- you can add a cover block to each column
- you can set /columns to wide width or full-width
- you can duplicate blocks or reposition them via the arrows or through drag and drop
- if you select the parent block, in the right sidebar you can change the # of columns
- make sure to toggle on "Stack on mobile"
- you can change the appearance of the parent blokc or the individual columns
- can change all 4 sides of the parent block padding but only top and bottom margin
- you can turn on block spacing to change the spacing between columns
- you can transform other blocks to a columns block or a columns block to a group block

........................................................................

## 2. Creating a new header with blocks

> https://learn.wordpress.org/tutorial/creating-a-new-header-with-blocks/

> VERY GOOD

- a typical header has a logo, site title, nav menu, and other elements like social icons

2 different headers and a header pattern

First one

- editor > patterns > all template parts > add new template part > name it > header > add
- add a `/row` block > site logo > next to that add a group block so you can stack site title and tagline
- select parent block and click the `+` and add nav block
- select the site logo and group block and turn them into a row using the toolbar
- select the parent block select space between
- change the bg color to a light blue gray
- then select the header in front place > 3 vert dots > replace - but the alignment is horrible - had to puch up the padding
- add a spacer block below the header if you need more space
- finally, modify the group block s=with the site title and tagline to reduce the block spacing and tweak the tagline typography if needed

Header using a cover block

- Editor > patterns > all template parts > add new template part > name it > header > add
- add /cover and enlarge the image > change the opacity
- add a group block and insite site logo > enter and add a spacer block to push the site logo to the top - change alignment of site logo to center
- add a nav block below site logo and change the nav justification to center
- Save > front page and replace with this one
- my fucky header for front page is sticky and I had no way to change that so I moved the new header out of the group it was in
- i removed the spacer and shortened the height of the cover block

Pattern

- when you click "Replace" you can choose a header pattern in the theme
  - not for me - only the headers are there - no pattern choices

........................................................................

## 3. How to Create a Menu with the Navigation Block

> https://learn.wordpress.org/tutorial/how-to-create-a-menu-with-the-navigation-block/

> REALLY GOOD

- switch to twenty twentyfive
- go into a template - list view and header > click on the nav block >
- my Pages template has:

```
header
  group
    group
      row
        site title
        row
          navigation
```

- when she clicks on the nav block she has a popup that has a button labeled "Select menu" and another "Start empty" - I don't have that
- inside you could have a block named Page List - if you get that select the PAge List block > edit > convert and then you will see t he blocks for each page on your site
- for a nested menu I created a Custom link, named it PAges and nested 2 pagews under it and gave it a link of `#` - it opens on Hover which I don't like

> How to create different menus in a wordpress block theme

- she used `+` and searched for "front" - selected Front PAge then hit Enter which crreated a custom link block and you should be able to search for another page

Sub-navigation:

- select a link in your nav > and she gets a floating toolbar to add an item to that menu item but I don't have that
- it looks like that creates a "Block pattern" block but that doesn't appear to be a thing anymore
- oh, there is a block called Submenu

To add a category into your menu:

- go to your categoties list > select one and click View > copy the url > paste it in

Search - the search block fucking sucks

Name your navigation:

- select the Navigation block > select the gear icon > click on Advanced > scroll down to Menu name > give it a name

> How to style the search block in a wordpress block theme

- submenu may be a block and you may be able to set it to open on click as opposed to hover

. . . . . . . . . . . .

Master the new WordPress Menu System - Jamie WP on YouTube

- submenu may be a block and you may be able to set it to open on click as opposed to hover
- group things you want to be sticky

........................................................................

## 4. Taking Advantage of Query Loops

> https://learn.wordpress.org/tutorial/taking-advantage-of-query-loops/

> EXCELLENT

- the Query Loop block is used to display posts based on specified params
- you customize it however you want: # of posts, filter for category or tag
- each query loop block is made of other blocks: post featured image, categories, post title, post author, and post excerpt
- you can customize the appearance and layout of those blocks including removing or adding blocks to the post loop like post meta
- his query loop shows that it is being displayed in grid view but mine are not
  - how do you make that happen?
  - I deleted the query loop, added it again and chose from a template then I was able to set it to wide width
- to change from grid click "Replace" in t he block toolbar

> With featured image block rememeber to set a value for the height so all the featured images display the same

- for equal height columns, select the container and set the min height to 100%

Variation

- remove the query loop, add another one and instead of "Choose" select "Start blank"
- then arrrange it how you want

Taxonomies and filters

- create a page named after one (or more than one) of your categories
- select the query loop block (which you styled) and open the sidebar settings for the block
- under QUERY TYPE change from Default to Custom
- your options here are:
  - POST TYPE (pages, posts or custom post types)
  - ORDER BY: new to old, old to new, A-Z, or Z-A
  - STICKY POSTS: Include, Exclude, or Only
  - POSTS PER PAGE
  - FILTERS: Taxonomies (cats or tags), Authors, Keyword, or Formats - keywords can have more than 1 word
- he has an option to change the number of columns but I don't have that. That may be because I have grid view but I think he does as well

> How do you make a blog post styicky in a wordpress block theme

........................................................................

## 5. Add and remove a logo and site icon

> https://learn.wordpress.org/tutorial/how-to-add-and-remove-a-logo-and-site-icon-in-a-wordpress-block-theme/

> VERY GOOD

- site icon: displayed in the browser tab
- before you can add a site icon you need to add a site logo
- go to a header template part - it may have a blank spot for your logo
- when you select your site logo from the upload screen be sure to add alt text
- the best practice for the alt text for yout site logo is to yuse the name of your business or website followed by "Logo"
- you can change the size of the logo in the settings sidebar
- you can then toggle "Use as site icon"
- you can make your logo rounded in the settings sidebar

What if you want a site icon without a site logo?

- set a logo first, then the site icon then delete the logo

What if you did not want your logo to match y our site icon?

- below where you toggled "Use as site icon" is a link titled "Site icon settings"
- that takes you to Settings > General > Site Icon

........................................................................

## 6. Create Block Theme plugin (theme fonts)

> https://learn.wordpress.org/tutorial/manage-your-block-theme-fonts-with-create-block-theme/

> Very good

In the settings screen for this plugin there is this:

> How do I install and remove fonts?

First Install and activate a font from any source using the WordPress Font Library. Then, _using the Create Block Theme Panel_

1. select "Save Changes To Theme"
2. and select "Save Fonts" before saving the theme.

All of the active fonts will be activated in the theme and deactivated in the system (and may be safely deleted from the system). Any fonts that are installed in the theme that have been deactivated with the WordPress Font Library will be removed from the theme.

NOW:

1. click the half moon for Styles
2. click typography
3. click the double-reverse arrows
4. you are presented with apopup with 3 tabs: Lirary, Upload, Install fonts and the last one connects to Google fonts

. . . . . . . . . .

Read this and see:

> https://gutenberg.10up.com/reference/Themes/fonts/

Using theme.json to handle the registration of fonts automatically makes sure the font files are properly enqueued everywhere in WordPress

### How to register local font files

Most of the time we want to load custom font files that we bundle with the theme itself on the server. This is for both performance and privacy reasons. We can avoid additional requests to external servers

Each font family we want to load needs to get it's own entry in the `settings.typography.fontFamilies` array:

- `fontFamily` - Font Family declaration like in css
- `name` - Human readable Name of the font family
- `slug` - Computer readable Name of the font family
- `fontFace` - Array of the individual font faces

The fontFace itself is another array that houses each of the individual font faces of the family:

- `fontFamily` - Name of the font family
- `fontWeight` - Weight of the current font face
- `fontStyle` - Style of the current font face
- `fontDisplay` - Font Display of the current font face
- `src` - Array of relative file paths to the individual font files of the current font face

```json
{
	"settings": {
		"typography": {
			"fontFamilies": [
				{
					"fontFamily": "FontName, sans-serif",
					"name": "FontName",
					"slug": "fontname",
					"fontFace": [
						{
							"fontFamily": "FontName",
							"fontWeight": "100",
							"fontStyle": "normal",
							"fontDisplay": "block",
							"src": [
								"file:./dist/fonts/fontname/fontname-thin.otf",
								"file:./dist/fonts/fontname/fontname-thin.woff",
								"file:./dist/fonts/fontname/fontname-thin.woff2"
							]
						},
						...
					]
				}
			]
		}
	}
}
```

The resulting output on the page will be an inline style tag with the various `@font-face` declarations

the best practice is to already define the correct fonts in the themes theme.json file and even disable the font library UI via this filter:

```php
function disable_font_library_ui( $editor_settings ) {
  $editor_settings['fontLibraryEnabled'] = false;
  return $editor_settings;
}
add_filter( 'block_editor_settings_all', 'disable_font_library_ui' );
```

..........................................................................

Dev - general:

## 8. Custom CSS in the Editor

> https://learn.wordpress.org/tutorial/custom-css-in-the-editor/

1. Finding a style using the inspector in Chrome - `SKIP` except

- `element.style`: select an element and at the top you can add some styles to see what they look like

2. Showing how to add custom CSS to your theme in Customizer and theme edit

- use the inspector to get the class(es) you need
- always preview on smaller devices

> BAD

........................ DEVELOPER VIDEO ...............................

## 11. Developing with user roles and capabilities

> https://learn.wordpress.org/tutorial/developing-with-user-roles-and-capabilities/

- 15:39

1. Explain the WordPress user roles and capabilities system
2. Assign capabilities to an existing role
3. Create a new User Role and assign capabilities to it

### Comprehension questions

1. What is the name of the option which stores the default user roles and capabilities in the database?
2. What is the name of the method on the Role class that you can use to add capacities to a role?
3. Which function can be used to create a new custom role, and assign capabilities to it?
4. How should you register new roles or assign new capabilities?

### WordPress User Roles and Capabilities

- WordPress comes with several default user roles: Administrator, Editor, Author, Contributor, and Subscriber
- Each of these roles has a set of capabilities, which are the things that the user can do in a WordPress
- When a new user is created in the WordPress dashboard, they are assigned the Subscriber role by default.
- You can change this by assigning a different role. Once assigned to a role, the user will have the capabilities that are associated with that role

Check out WordPress Documentation on [Roles and Capabilities](https://wordpress.org/documentation/article/roles-and-capabilities/)

### Roles and Capabilities under the hood

The WordPress user roles and capabilities system is stored in the database during the WordPress installation process. The roles and capabilities are stored as a serialized array as site options in the `options` table, in the `user_roles` option usually prefixed with `wp_`: `wp_user_roles`

If you extract the value of the user_roles option, and unserialize the array, you will see that the array keys are the role names, and the values are arrays of capabilities

Whenever an authenticated user is attempting to do something, this action is checked against the user's role capabilities, using the `current_user_can` function. If the user has the capability to perform the action, they will be allowed to do so. If they do not have the capability, they will be denied access

### Assign capabilities to an existing role

Let's say that you want to allow your editors to be able to do something that only admins can do, maybe install and update plugins. By default, the Editor role does not have the `activate_plugins` or `update_plugins` capability

You can add this capability to the Editor role by using the `add_cap` method of the `WP_Role` class

However, doing so will add this capability to the `user_roles` stored in the database, so it's recommend to run this on something like plugin activation using the [register_activation_hook](https://developer.wordpress.org/reference/functions/register_activation_hook/) function

```php
register_activation_hook( __FILE__, 'wp_learn_add_custom_caps' );
function wp_learn_add_custom_caps() {
    // gets the author role
    $role = get_role( 'editor' );
    $role->add_cap( 'activate_plugins' );
    $role->add_cap( 'update_plugins' );
}
```

The `register_activation_hook` requires the path to the file that contains the hook callback, and the hook callback function name

Then you can add the capabilities to the Editor role by using the get_role function to get the role object, and then using the add_cap method to add the capabilities

Note that because adding capabilities to a role is a permanent change, you should only do this when the plugin is activated, and not on every page load. Also, if you want to remove a custom role, it's a good idea to do so on plugin deactivation, using the `register_deactivation_hook` function

> See the rest of the transcript

### Create a new User Role and assign capabilities to it

Just as it is possible to assign existing capabilities to roles, you can also create your own custom roles, and assign capabilities to them. This is useful if you want to create a role that has a specific set of capabilities, and you don't want to use an existing role

For example, lets say you want a user role who can only activate and update plugins, say an assistant to the administrator. You can create a new role, using the add_role function, and assign the activate_plugins and update_plugins capabilities to it

```php
register_activation_hook( __FILE__, 'wp_learn_add_custom_role' );
function wp_learn_add_custom_role() {
    add_role(
        'assistant',
        'Assistant',
        array(
            'read'         => true,
            'activate_plugins'   => true,
            'update_plugins' => true,
        ),
    );
}
```

> See the rest of the transcript for code

> GOOD - but I doubt I would need to do this, exceptions only

..........................................................................

## 13. Troubleshooting Basics: Part 1

> https://learn.wordpress.org/tutorial/wordpress-troubleshooting-basics-part-1/

> Indian with bad english...

the three steps

1. First one is learn about the problem and document it
2. The next thing is to investigate why the problem is happening
3. And the third step is to actually do the troubleshooting. Actually go ahead and fix the problems

### First one is learn about the problem and document it

- what are the symptoms of the problem? Where does this happen? Where is the problem happening? Why is it happening? And how is it happening?
- What are the symptoms of the problem? So what do you see as part of the issue? Is your site broken?
- Or is the display of one of your pages broken? Or is some feature of your site not working? And if possible, write it down
- when is the problem happening? So what actually caused the error?

### why the problem is happening

- In order to find out you would need to dig a little deeper
- the next steps involved would be to try and replicate the problem
- the best way to replicate the problem is to try to see if the same problem occurs in a different website - the best way to do this is by testing in a local server

It could be a bug with the WordPress core itself, it could be a blog bug with one of the plugins that you've used, it could be a bug with the theme that you use for your site

if you're not able to replicate the problem, it could be a problem with your site itself - in that case, it may be a configuration issue, but it may also be a bug

...tested this in a site where one or more of your plugins are not active, or an another site where the theme that you've installed is not active...

### your next step is to fix the problem

if you don't come from a development background, you may not always be able to do the fix on your own, you may have to seek help

some of the most common troubleshooting steps

- the first step: create a backup
- The next troubleshooting step: staging sites
- or work locally

> The majority of the problems that people face in WordPress are due to conflicts

in many cases The code from one plugin might conflict with the code from another plugin

> SUCKS

........................ DEVELOPER VIDEO ...............................

## 14. Troubleshooting Basics Part 2

> Troubleshooting with Logs: https://learn.wordpress.org/tutorial/wordpress-troubleshooting-basics-part-2-troubleshooting-with-logs/

- 26:43

Debug Logs

- How to enable debug logs
- How to catch errors in the debug log.

Console Logs

- An introduction to the browser console
- Finding errors using the browser console.
- Troubleshooting using the errors found in the browser console.

### WordPress debug logs

> https://developer.wordpress.org/advanced-administration/debug/debug-wordpress/

- WP_DEBUG: The following code, inserted in your wp-config.php file, will log all errors, notices, and warnings to a file called debug.log in the wp-content directory. It will also hide the errors, so they do not interrupt page generation

```php
// Enable WP_DEBUG mode
define( 'WP_DEBUG', true );
// Enable Debug logging to the /wp-content/debug.log file
define( 'WP_DEBUG_LOG', true );
// Disable display of errors and warnings
define( 'WP_DEBUG_DISPLAY', false );
@ini_set( 'display_errors', 0 );
// Use dev versions of core JS and CSS files (only needed if you are modifying these core files)
define( 'SCRIPT_DEBUG', true );
```

- NOTE: You must insert this BEFORE `/* That's all, stop editing! Happy blogging. */ in the wp-config.php file.`

WP_DEBUG

- PHP constant (a permanent global variable) that can be used to trigger the “debug” mode throughout WordPress
- `false` by default, and is usually set to true in the wp-config.php file

> It is not recommended to use WP_DEBUG or the other debug tools on live sites; they are meant for local testing and staging installs

- Enabling WP_DEBUG will also cause notices about deprecated functions and arguments within WordPress that are being used on your site. These are functions or function arguments that have not been removed from the core code yet, but are slated for deletion in the near future

### WP_DEBUG_LOG

- `WP_DEBUG_LOG` is a companion to WP_DEBUG that causes all errors to also be saved to a debug.log log file which can be useful for instance when debugging Ajax events
- When set to true, the log is saved to debug.log in the content directory (usually wp-content/debug.log) within your site's file system

**Note**: for WP_DEBUG_LOG to do anything, WP_DEBUG must be enabled

### WP_DEBUG_DISPLAY

- `WP_DEBUG_DISPLAY` is another companion to WP_DEBUG that controls whether debug messages are shown inside the HTML of pages or not. The default is ‘true' which shows errors and warnings as they are generated. Setting this to false will hide all errors. This should be used with WP_DEBUG_LOG so that errors can be reviewed later
- this is good because it will show you the file name and line number where the error is coming from

**Note**: for WP_DEBUG_DISPLAY to do anything, WP_DEBUG must be enabled

### SCRIPT_DEBUG

- `SCRIPT_DEBUG` is a related constant that will force WordPress to use the “dev” versions of core CSS and JavaScript files rather than the minified versions that are normally loaded. This is useful when you are testing modifications to any built-in .js or .css files

### SAVEQUERIES

- The `SAVEQUERIES` definition saves database queries to an array, which can then be displayed to help analyze those queries. When the constant is set to true, it causes each query to be saved along with the time it took to execute and the function that called it

```php
define( 'SAVEQUERIES', true );
```

**NOTE**: This will have a performance impact on your site, so make sure to turn this off when you aren't debugging

### Debugging Plugins

1. Debug Bar - you need the following for this plugin:

```php
define( 'WP_DEBUG', true );
define( 'SAVEQUERIES', true );
```

- When WP_DEBUG is enabled it also tracks PHP Warnings and Notices to make them easier to find.
- When SAVEQUERIES is enabled the mysql queries are tracked and displayed
- it shows a lot of information - queries, WP Query, Object Cache (?)
- seeing the queries used on any page is great
- it also shows you the JavaScript Console

2. Debug Bar Console - Adds a PHP/SQL console to the debug

- if you really want to see what's happening on the console, as you browse to your site, this is going to be a very useful add on to the debug bar plugin

3. Query Monitor - it helps you debugging database queries, PHP has hooks and actions, etc - this is for advanced users

- It enables debugging of database queries, PHP errors, hooks and actions, block editor blocks, enqueued scripts and stylesheets, HTTP API calls, and more
- It includes some advanced features such as debugging of Ajax calls, REST API calls, user capability checks, and full support for block themes and full site editing.
- It includes the ability to narrow down much of its output by plugin or theme, allowing you to quickly determine poorly performing plugins, themes, or functions
- and you can navigate to different pages to see specifics for that page
- click Database Queries > then in the left sidebar click Database Queries then Queries by Component to see all the plugin times
- you can check styles loading, http api calls,

### Using Console log to debug

- JS errors - front-end errors
- when something on the front end stops working

Steps:

1. test with a different browser
2. enable SCRIPT_DEBUG
3. check the browser console

> VERY GOOD

........................ DEVELOPER VIDEO ...............................

- 16. Using Block Attributes to Enable User Editing: https://learn.wordpress.org/tutorial/using-block-attributes-to-enable-user-editing/

Learn about block attributes and how you can use them to create blocks that your users can edit

Learning outcomes:

- Learn to define block attributes
- Pass attributes to your block code via blockProps
- Access block attributes in your code
- Make attributes editable via the Settings Sidebar

.................................................................

## 6. Block Theme Builders – Figma to Block Theme

> `DONE` https://wordpress.tv/2022/08/19/block-theme-builders-figma-to-block-theme/

Theme.json video mostly

- 58 mins
- a figma design turned into a block theme - he has typogrqaphy and colors and buttons - I forget what they call that in Figma

### Theme.json

Steps he took going from Figma to theme.json

- settings.AppearanceTools (already there)
- settings.layout (already there)
- settings.color.palette
- settings.spacing.units
- he added a Google font to assets/fonts

```json
{
  "name": "Poppins",
  "slug": "poppins",
  "fontFamily": "Poppins, sans-serif",
  "fontFace": [
    {
      "src": [
        "file:./assets/fonts/poppins-400.woff2"
      ],
      "fontWeight": "400",
      "fontStyle": "normal",
      "fontFamily": "Poppins"
    }
  ]
},
```

but you need to add the following in styles.typography - you need to tie the above custom font reference to the body:

```json
"typography": {
  "fontFamily": "var:preset|font-family|poppins",
  "fontSize": "var:preset|font-size|large",
  "fontWeight": "400",
  "letterSpacing": "-0.1px",
  "lineHeight": "1.4"
},
```

- see settings.typography.fontSizes for the fluid.max and fluid.min properties
- then styles.elements.h1.typography.fontSixe: `"var:preset|font-size|x-large"` - repeat for all headings
- besides .h1 also do link, link:hover, caption, button,

> The guy doing this video is an idiot

.................................

## 7. diving into theme.json

> `DONE` https://wordpress.tv/2022/09/02/lets-code-diving-into-theme-json/

- 59 mins
- enabling debug mode
- include the schema
- enabling/disabling appearanceTools, layout, dropCap
- color palette, theme colors,
- applying toe color to core/post-title block
- theme.json replaces the need for add_theme_Support in functions.php

> If you have caching issues while developing theme.json, set either `WP_DEBUG` or `SCRIPT_DEBUG` to `true` in `wp-config.php` - he always turns on `WP_DEBUG` and `WP_DEBUG_LOG` but has `WP_DEBUG_DISPLAY` set to `false` - always have `WP_DEBUG` on for local dev

```php
define( 'WP_DEBUG', true );
define( 'WP_DEBUG_DISPLAY', false );
define( 'WP_DEBUG_LOG', true );
```

### Top level items

1. $schema
2. version
3. customTemplates: to register a template that is not available in the Site Editor - blank and page no title are examples

- add them into an array
- three fields/keys for each array item: name, postTypes, title

4. settings: appearanceTools, color, layout, spacing, typography, useRootPaddingAwareAlignments, background, blocks, border, custom, dimensions, lightbox, position, and shadow

- `appearanceTools`: enable all of the following - border (color, radius, style, width), link color, spacing (blockGap, margin, padding), typography lineheight - always have it set to `true`
- if you set it to false you can enable individually things like border or padding
- `color`: the `palette` key has 3 fields - color (hex value), name slug - they are colors specific to the theme - "Default" colors are defined by WP core - "Theme" colors come from this setting
- there is a css preset format: `--wp--preset--color--{slug}`
- shorthand for above: `var:preset|color|{slug}` - so no `wp` or `--` using pipes instead
- `defaultDuotone`:
- `defaultGradients`:
- `defaultPalette`:
- layout: contentSize, wideSize

> **NOTE**: any changes you make in the Site Editor will override your values in theme.json

5. styles: color, spacing, typography, blocks, elements, background, border, dimensions, css, filter, outline, shadow, variations

- you can have global styles and block styles - for examples your colors or typography is global but you can set fontSizes for headings
- this section basically replaces your style.css
- for example, under styles.color there is only background and text which is like setting the color on the body tag
- for blocks and core/post-title he added a color key with "background" and set that even though it was not there already

> Do everything in theme.json, and onlt use a stylesheet fpr things that theme.json does not support

MEDIA QUERIES:

- none in theme.json
- to handle media queries, use the columns block which scales

> EXCELLENT VIDEO

........................... DESIGN ...........................

## 6. Beginner WordPress Designer

> https://learn.wordpress.org/course/beginner-wordpress-designer/

- 24 LESSONS, 6 MODULES

> `DONE` See learnWP/beginnerDesign

.................................................................

## 8. Designing for accessibility

> https://wordpress.tv/2022/12/20/designing-for-accessibility/

- 1 video, 43 mins

> `DONE` See learnWP/accessibility.md

........................ SKIP ALL BELOW HERE ..........................

> TOO LONG: SKIP BASED ON THE TITLES

- 11. Intro to Publishing with the Block Editor: https://learn.wordpress.org/tutorial/intro-to-publishing-with-the-block-editor/ - 40 MINUTES LONG

This one goes with the above video:

- 12. Intro to Block Patterns: https://learn.wordpress.org/tutorial/intro-to-block-patterns/

These videos are old and outdated: `circle back when registering patterns`

**`Block Patterns and block directory`**:

- 13. Registering Block Patterns: https://learn.wordpress.org/tutorial/registering-block-patterns/
- 14. Submitting Block Patterns to the Directory: https://learn.wordpress.org/tutorial/submitting-block-patterns-to-the-directory/
- 15. Intro to the WordPress Block Directory: https://learn.wordpress.org/tutorial/intro-to-the-block-directory/
- 16. Finding New Blocks with the Block Directory: https://learn.wordpress.org/tutorial/finding-new-blocks-with-the-block-directory/
- 17. **Customizing your post content layout**: https://learn.wordpress.org/tutorial/customizing-your-post-content-layout/
