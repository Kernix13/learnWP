# An introduction to developing WordPress themes

## Introduction to themes for developers

The difference between a theme and a plugin is that themes control the presentation of content, and plugins control the behaviors and features of your site

- When you’re ready to start designing your theme, you’ll have to put some thought towards colors, fonts, layouts and features
- You can get inspiration by visiting the [WordPress.org themes directory](https://wordpress.org/themes/) - you can see a list of layouts that theme developers normally include in their themes
- also go to Appearance > Themes > Add new theme > click Feature Filter and look at the Features column
- For a block theme, what blocks, patterns and media will you give your end users access to

### The fundamental structure of a block, classic and hybrid theme

- Block themes use blocks for all parts of the site, including navigation menus, headers, content and footers. This theme’s files are mainly HTML and JSON file format
- Classic themes don’t use the block editor to manage the site, layout beyond posts and pages. With classic themes we mostly have PHP files
- A good example of a hybrid theme is the Twenty Twenty-One theme - A hybrid theme is a classic theme that adopts some features of site editing - within the Twenty Twenty-One theme we will see in the functions.php file that they have added theme support for block styles

> [Developer Resources](https://developer.wordpress.org/)

## Theme structure

1. Within the `assets` folder, you’ll find fonts, images, CSS and JS files.
2. Within the `parts` folder, you’ll find HTML files for things like the header and the footer.
3. Within `patterns`, you’ll find PHP files for components you can build to save users time when they’re building their pages and posts.
4. Within `styles`, you’ll find JSON files, which offer the user variations on their sites global styles.
5. And finally, within `templates`, you’ll find HTML files for generating pages and posts

### Required and optional files needed for a block theme

Required:

- The two necessary files are `style.css` and `templates/index.html`
- `index.html` needs to be in the templates folder - It is the default fallback template and it’s necessary for WordPress to consider this a block theme

Optional:

- The `functions.php` file is automatically loaded by WordPress after the theme is initialized and this is a good place to run your custom PHP.
- Next we have the `readme.txt` file and it’s not used directly by WordPress but is a required file when you submit your theme to the official WordPress theme directory
- the `screenshot.png` file and it is recommended to use a dimension of 1200 by 900
- The last file we’ll look at is `theme.json` and it is your site’s configuration file for mainly settings and styles that integrate with the user interface

### Standard folders used with a block theme

There are four standard folders. These are the standard ones that WordPress has designated for specific features

1. the `templates` folder: HTML files and they represent the overall document structure of the front end and they are essentially templates made up of block markup
2. the `styles` folder: JSON files and each one of these represents a different style variation - the different color options
3. the `patterns` folder: reusable components and they’re made up of one or more blocks that users can insert within the site editor. Note that WordPress will automatically register files included in this folder
4. the `parts` folder: smaller sections that can be included within top level templates. This includes things like headers, footers, sidebars

```md
functions.php
readme.txt
screenshot.png
style.css
theme.json
assets/ <!-- css, fonts, images, js -->
parts/ <!-- .html files -->
patterns/ <!-- .php files -->
styles/ <!-- .json files for global styles variations -->
templates/index.html <!-- .html files -->

<!-- 2024, no JS:  -->

assets/css
assets/fonts
assets/images
```

> `.html` files in the `templates/` folder - go hog wild

- Home, Index, Page,
- 404, Single Post, Search, Archive
- Front Page, Author, Category, Date, Tag, Taxonomy, Single item: Post, Custom Template, Page No Title, ...

## Main stylesheet

### Creating the style.css file header to configure data about the theme

- The file’s header comment section is used to let WordPress and users know about the theme - here is twentytwentyfour's style.css

```css
/*
Theme Name: Twenty Twenty-Four
Theme URI: https://wordpress.org/themes/twentytwentyfour/
Author: the WordPress team
Author URI: https://wordpress.org
Description: Twenty Twenty-Four is designed to be flexible, versatile and applicable to any website. Its collection of templates and patterns tailor to different needs, such as presenting a business, blogging and writing or showcasing work. A multitude of possibilities open up with just a few adjustments to color and typography. Twenty Twenty-Four comes with style variations and full page designs to help speed up the site building process, is fully compatible with the site editor, and takes advantage of new design tools introduced in WordPress 6.4.
Requires at least: 6.4
Tested up to: 6.7
Requires PHP: 7.0
Version: 1.3
License: GNU General Public License v2 or later
License URI: http://www.gnu.org/licenses/gpl-2.0.html
Text Domain: twentytwentyfour
Tags: one-column, custom-colors, custom-menu, custom-logo, editor-style, featured-images, full-site-editing, block-patterns, rtl-language-support, sticky-post, threaded-comments, translation-ready, wide-blocks, block-styles, style-variations, accessibility-ready, blog, portfolio, news
*/
```

### Header fields available within a theme’s style.css file

- Theme Name: this needs to be unique - if you’re just getting started with theme development, you can stop after adding the theme name. That is all you really need
- Theme URI: the URL of a public web page. This is where people will go to get more information about your theme
- Author and Author URI
- Description: this is especially important if you’re wanting users to see this and get a good idea of if this theme is for them
- Requires at least, Tested up to, Requires PHP
- Version: good to include
- License, License URI
- Text Domain: a string used for translations, so make sure to include this if you plan to translate your theme, and make sure that you’re using all lowercase letters
- Tags: comma separated list of features that your theme supports

### The necessary header field to designate the parent theme’s folder within a child theme

Creating child themes is actually a more advanced topic for theme developers. It’s important to understand that your child theme not only inherits your parent theme’s functions, filters, templates, and so on, but it will both extend and override its parent theme. Now that connection between the child and parent theme is created by adding the header field template to the style.css file of the child theme.

## Templates

Templates are files that represent the overall document structure of the front end. For a modern block theme, they are made up of block markup and render both static and dynamic data.

Block markup is identified by a specific HTML comments notation. It tells the page being rendered to render the output for that block. Additional information about the block, like attributes or inline styles, is passed to the block markup in a JSON format. WordPress parses this block markup and translates it into its final HTML markup within a web browser.

NOTE the JSON:

```html
<!-- wp:template-part {"slug":"header","area":"header","tagName":"header","theme":"mytwenty24"} /-->

<!-- wp:group {"tagName":"main"} -->
<main class="wp-block-group">
  <!-- wp:group {"layout":{"type":"constrained"}} -->
  <div class="wp-block-group">
    <!-- wp:spacer {"height":"var:preset|spacing|50"} -->
  </div>
</main>
```

> The new ![template hierachy](https://i0.wp.com/developer.wordpress.org/files/2023/10/template-hierarchy-scaled.jpeg?ssl=1) for block themes

### Common templates found within a theme

- the template used follows a set of rules outlined by the template hierarchy
- Index: this is the fallback template file and it is a required file in all themes.
- Single: used when a visitor requests a single post as we saw in our example.
- Page: used when visitors request individual pages.
- Archive: used when visitors request posts by archive type, for example, category or author.
- Search: used for search results when a visitor does a search on a website
- 404: used when WordPress cannot find a post page or other content that matches the visitors request.
- others: page-notitle.html, page-wide.html, single.html, single-with-sidebar.html, page-with-sidebar.html

### Difference between templates and template parts

- Template parts are meant to provide areas of web pages that are repeated
- header.html, footer.html, post-meta.html, sidebar.html
- Templates can include either one or more template parts, however you can opt to not have any at all

## Global settings and styles

### Why does a WordPress theme need a theme.json file?

- if we take a look at the classic theme Twenty Twenty-One, we would find the settings for colors and widgets within the Customizer. It is with the Customizer that end users work with the theme
- block themes and theme developers can now use theme.json to provide those features to end users. This provides a more consistent way of presenting features
- Within the Site Editor, you can see the possibilities for the settings and styles that you can include in your theme

> Way more possibilites given the stylebook and Styles link to change EVERY design element of your site and then further customize the blocks

### JSON format and the structure of theme.json

JSON is for config files and is a common format for sending and requesting data through a REST API and it’s lightweight and easy to read

- One thing to note is the key is always a string
- `Schema`: used for defining the supported JSON. And this is why we get the on the fly hints and error reporting
- `Version`
- `Settings`: used to define your block controls, color palettes, font sizes, and so on
- `Styles`: used to apply items such as colors, font sizes, custom CSS applied to the website and blocks.
- `Template parts`: metadata for template parts defined in your themes parts folder.
- `Custom templates`: metadata for custom templates defined in your themes templates folder.
- `Patterns`: a comma separated list of slugs to be registered from the pattern directory available to us on WordPress.org.

### Hierarchy used for loading the setting and style configurations

- The theme.json file included in your theme is only one level in a hierarchy of setting and style configurations for a website. This means that it can be overridden under certain circumstances

1. WordPress:

Within the installation files, if you go to the WP includes folder, you’ll see theme.json there and this file defines the default settings and styles: `wp-includes/theme.json`

2. Theme theme.json file

Anything you define in that file will override the WordPress defaults. If you have a child theme that is active and you have a theme.json file included in your child theme, then anything that you do here will take precedence over the `theme.json` file in the parent theme. For instance you could set `Appearance Tools` to false.

3. User configurations

Within the Site Editor any changes that are added to the database through changes made to global styles or even templates and saved. This will override and takes priority over all other levels in the hierarchy.

> [theme.json reference guide](https://developer.wordpress.org/block-editor/reference-guides/theme-json-reference/)

## Create Block Theme plugin

The Create Block Theme plugin has been developed by the MakeWordPress.org community. It is meant for development only and is not intended for use on a production website - it's tool meant for creating new themes

Appearance > Create Block Theme - Some options you will find are all related to the currently activated theme

- Export "your theme" as a zipped file
- Create a Clone of "your theme"
- Create a Child of "your theme"

And then you have:

- Create a new Blank Theme: in case you're wanting to start off with a boilerplate or an empty theme

> And finally, the last option is Create a Style Variation. This is something that is in relation to global styles and we will be covering this in much greater detail later on within the Intermediate Theme Developer Learning Pathway - _NOT AN OPTION ANYMORE_

- Note that this plugin also helps you with managing your theme fonts - not like they say

### Exporting Changes to Theme Files

> WRONG I THINK

- the Create Block Theme plugin sidebar and the Save Changes option. This removes the changes from the database and pushes them to the theme files
- take a quick look in the theme files to see those saved changes

CLICK THE WRENCH ICON IN A TEMPLATE AND YOU'LL SEE:

1. Save changes in theme
2. Create theme variation
3. Edit theme metadata
4. view theme.json
5. view custom styles
6. export zip
7. create blank theme
8. create theme
9. reset theme

Remember, to see changes made to the theme go to the template html files

> Instead read the [plugin page](https://wordpress.org/plugins/create-block-theme/)
