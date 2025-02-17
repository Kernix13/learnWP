# Advanced WordPress User

5. Advanced WordPress User

> https://learn.wordpress.org/course/advanced-wordpress-user/

- 20 lessons

## Creating custom post types and taxonomies

- custom post type: they are stored in the DB as pages and posts - along with taxonomies (categories, tags)
- you can create custom post types + taxonomies
- a custom post type is useful when creating content that has a different format than a standard page or post
- Portfolio post types are common - products in Woocommerce are registered as custom post types and the product categories are custom taxonomies
- other examples: books, book reviews, team members, clubs, courses, lessons, recipes, ...

The best way to establish a custom post type on your site:

- either code it or use a plugin
- the developer handbook recommends to put the custom post types in a plugin rather than in a theme
- the 2 most popular plugins for this: Custom Post Type UI, Advanced Custom Fields
- install/activate Custom Post Type UI > Add/Edit Post Types > name a slug > enter single and plural labels > select "Auto populate labels" > then scroll thru the labels to see if you want to change any of them
- scroll to the settings below the labels > make sure you change "Has Archive" setting to `True` - same for "Can Export"
- Taxonomies setting > don't select them if you are setting up your own > Save
- now you can set up custom Taxonomies - select Add/Edit Taxonomies > same fields as for the custom post type > remember to select the post type to which they apply
- you probably want tto set Hierarchical to `True` and "Show in quick/bulk edit panel" to `True`
- when done you need to edit your custom post type: Add/Edit Post Type > choose the post type and check your new taxonomies > Save
- then add your variations for your custom taxonomies, e.g. for Height, "Less than 3000'", "Above 12000'", etc
- then create your first custom post type entry > then provide a way for your users to view them - create a page to display the CPT archives - make sure to change its slug to match the slug of your post type > add it to your menu
- he is adding a sub menu for Height and Climbing Rating as placeholders - add 2 hashtags `##` in the URL field to ensure they are not clickable
- select each one > 3 vert dots > Add submenu link > less for the values

Templates:

- these pages are using the All Archives template - Add New Template > choose either "All YourCPTName" or "Single Item YourCPTName" - you could also choose your Taxonomies in that list

> GREAT

. . . . . . . . . . . . .

### Creating Custom Fields

> https://learn.wordpress.org/tutorial/creating-custom-fields/

adding custom fields to your custom post types

- There are a variety of ways to do it, you can write the code yourself, which isn't that hard

> He is using Advanced Custom Fields - `SKIP` becuase I watched some dev videos on how to do it with code but come back to this video later

. . . . . . . . . . . . .

### Custom post types and capabilities

> https://learn.wordpress.org/tutorial/custom-post-types-and-capabilities/

- 15:35
- `capability_type` | `map_meta_cap` | `register_post_type` | `capabilities`
- LOOK AT wp-includes/class-wp-post-type.php > map_meta_cap
- the 3 meta capabilities are edit_post, read_post, delete_post
- there are two types of primitive capabilities
- current_user_can

> See `6-plugin-dev.md` & `8-wp-rest-api.md` - both in `learnWP/beginnerDev`

> GOOD - watch later or skip - super complex and confusing

. . . . . . . . . . . . .

## WordPress taxonomies

- taxonomies are a way of grouping posts together - the method of classifying content and data in WP
- there are 2 types of taxonomies: default and custom
  - default: cats, tags, post formats
  - custom: created by coding or a plugin
- categories are hierarchical which means they can have children
- WP requires at least one category per post
- you want to rename "Uncategorized" to something relevant
- Tags: non-hierarchical
- custom taxonomies:
- adding a description to a taxonomy: `Term Description block`

> Good

## Adding custom user roles using a WordPress plugin

- defaults are Admin, Editor, Author, Contributor, Subscriber
- custom roles: allow you to define specific responsibilites & permissions, segment users and tailor their experiences, manage content moderation effectively, and define custom work flows
- example: non-profit and you want Coordinators & Volunteers
- Members plugin > Roles > Add New > select capabilities

> Okay

## Use WordPress to create a one-page site

- you don't need any pages - just add a Front Page template
- `#anchorname` in the menu then `anchorname` for each section under Advanced > HTML Anchor
- you can see the anchor is List View to the right of each section
- Sicky Header: wrap your `Header` in a `Group block` > select the group and in the right sidebar, below Position select Sticky - that changed my alignement to center so I had to make the Group full-width - it needs padding now
- Smooth scrolling: he used CSS: Click on the Styles icon (half-moon) > then on the 3 vert dots > then on Additional CSS:

```css
@media (prefers-reduced-motion: no-preference) {
  html {
    scroll-behavior: smooth;
  }
}
```

> Good

## Making the most of the Font Library

- WP 6.5 - install and remove custom fonts just like the media library
- Click on the global styles icon (half-moon) > Typography > click the double arrows "Manage Fonts" >
- You see Installed Fonts if you added any or just Theme for the theme fonts
- Click on the Upload tab and upload your font files - sometimes your host may restrict uploading fonts
- To install fonts from Google Fonts click on the tab "Install Fonts" > click Allow access to Google fonts > the next screen has 3 vert dots to revoke access
- The fonts you install will be downloaded from Google and stored on your site - that means they are locally hosted
- Locally hosted fonts load faster
- You can select specific weights and styles

Pairing font families:

- font families are groups of related font faces that share common design characteristics - it's best to only have 2 font families, 1 for headings, 1 for body, and apply different styles for elements like quotes (italic, light weight)
- example: Merriweather and Ubuntu Sans
- Legibility: distinct letters, big enough font size, good contrast - avoid cursive font faces

> Great

## How to build a responsive WordPress website

1. choose a mobile friendly theme

- when you preview a theme, you can use the "Medium" and "Narrow" display options to see what the theme looks like on smaller screens
- also test them out at https://playground.wordpress.net/?theme=slug

2. Simplify your navigation menu

- select header > navigation block > settings icon > you will see that the hamburger menu is selected by default for mobile

3. Mobile-friendly forms

- use responsive form designs that adapt to different screen sizes
- improve accessibility by always adding form labels and TAB navigation

4. the intrinsic design of WordPress blocks

- intrinsic design means coding web layouts and components that dynamically adapt to the available space based on the content and user preference, instead of solely focusing on screen sizes
- blocks allow for flexible and responsive layouts
- blocks adapt to all devices due to their intrinsic nature - typography and spacing grow and shrink based on the screen size
- there are excellent 3rd-party block plugins that offer granular responsive controls - Kadence, Stackable

5. Test your site

- resize the window, CTRL + or -, or use the inspector

> Good

## Use the Create Block Theme plugin for exports, and theme variations

> https://learn.wordpress.org/lesson/use-the-create-block-theme-plugin-for-exports-and-theme-variations/

> REWATCH THIS OVER AND OVER

- to save and export design variations
- by default, changes to a theme styles are saved as database entries which menas they are _NOT_ integrated into the theme files
- However, if you are working on a design website and want to transfer that design to another website you would need to save it as part of the theme
- **the Create Block Theme plugin lets you transform your customizations into permanent variations of the original theme and export that modified theme**
- that is then a custom theme - this avoids overwriting your customizations when updating the theme

Customizing the active theme on your site:

- adjusting global styles, modifying templates and template parts, creating custom block styles, design block patterns, manage site layout options,
- so make some customizations > try global styles > colors > palette > custom > select a color > click Done > then apply that color to an element via the style book > Save > then make a change to say Page 404 by addding an image > Save > then click on the Wrench icon (Create Block theme) > select Save changes to theme > Save Changes
- when you do that you will see that your custom color is no longer under "Custom" but is below "Theme" because it was added to the theme.json file - all your changes are now part of the theme files

> The Create Block Theme plugin allows you to transform your customizations into permanent variations of the original theme

- the next step is to rename your theme
- choose Create a new Blank Theme > name it, add a description and the name of the author
- you can continue to make customizations and when you are ready to export the mdified theme > click the Wrench > Export Zip > Import it to another site

> EXCELLENT!

## Using caching to improve website performance - W3 Total Cache plugin

- caching is a technique to improve the performance of websites - it involves frequently accessed data in a cache which can be quickly retreived rather than having to retreive from the website each time
- web pages load faster and lessens the server's burden - better UX
- caching occurs at multiple levels
  - front-end: browser cache - caches static files like images and CSS reducing server requests
  - Object caching in WP: speeds up data retreival by storing frequently accessed info in fast access storage systems like memcache and redis
  - Server level: improves php execution (CDN, opcode)
  - advanced solutions like "Varnish"???

The 4 most common types of caching: https://managewp.com/blog/types-of-web-cache

1. Page/Site cache: a snapshot of your web page, a static copy of tthe page
2. Browser cache: files stored on 1st visit making other visists faster
3. Server cache: involves storing commonly accessed website data. When a user requests that data, the server can quickly retrieve it from the cache instead of generating it again
4. CDN cache: Content Delivery Networks -

- WP Total Cache, WP Fastest Cache, LiteSpeed Cache

W3 Total Cache settings:

- Test page Cache
- Test Database Cache - note about skipped "Disc" as the server database engine may be faster than using disc caching - they recommend using Redis or Memcached
- Test Object Cache - choose the option with the fastest time
- Test Browser Cache
- Image Optimization - check Enable WebP Converter
- Lazy Load - enable this too
- More Caching Options > click General Settings link >
- General Settings:
  - enable page cache (some hosts provide page caching)
  - minify - enable > leave it on Auto but check your site for "issues"
  - Opcode Cache: pro version only
  - Database Cache: recommended not to enable and is to be used if Object cache is not available
  - Object Cache: enable it - but these 2 are not recommended when on Shared Hosting
  - Browser Cache: enable it
  - CDN: enable it but sign on for Cloudflare
  - Google PageSpeed section: skip

Note: sometimes the cache won't know that you made changes - clear your cache so the newer version loads

> Great

## Using a CDN to enhance performance

- CDN: Global network of servers that caches your website's static content such as images, CSS, and JS files - Edge Servers
- improves speed, reduces server load, increases uptime, enhances security especially against DDoS attacks
- DDoS: Distributed Denial of Service, a type of cyber attack that overwhelms your server with too much traffic causing it to crash - a CDN spreads this across multiple servers
- it's best to integrate a caching plugin with the CDN
  - WP-Optimize automatically integrates with Cloudflare
  - Others: W3 Total Cache, LiteSpeed Cache for WordPress

> Good

## Why would a WordPress user need to run a local site?

- WordPress Studio: https://developer.wordpress.com/studio/ - download and install
- WordPress Playground: https://wordpress.org/playground/ - browser-based tool - enable browser storage otherwise you lose everything
- DevKinsta: https://kinsta.com/devkinsta/ - download and install but you also need Docker
- LocalWP, XAMPP

> Ok

## How to start using WordPress Playground

- install plugins: you can't use Plugins > Add New but you can Upload them
- same with themes
- but better to do `/theme=statepark&plugin=gutenberg&plugin=create-block-theme` but make sure you are using the exact theme and plugin slugs
- then Appearance > Editor > make changes
- to export click the 3 vert dots > Create Block Theme > Export
- then open new playground > Appearance > Themes and install the zip you exported
- but there is a download icon at the top right to download your entire site - next to it is an upload icon
- compatibility tsting - can switch versions of PHP or of WordPress

> That enables you to find out the minimum version required to run your theme

> Okay

## The building blocks of WordPress templates

> I HAVE TO REMEMBER HOW TO SAVE CHANGES

- Tools > Theme File Editor > Templates > page.html - it's not recommended to modify the files this way
- go into a post then 3 vert dots > Code Editor > he says there are 3 languages: HTML, CSS and JSON

## How Styles are generated

- WP offers 2 ways to modify fonts, colors and layouts via the site editor:
  - 1. use global styles
  - 2. use the style book

theme.json

- the file used to define the global and block-based styles for the theme
- the primary file that's responsible for specifying and organizing all the theme's design aspects
- changes you make in the site editor are stored in the database, not theme.json

> Ok

## Understand where your files live

- FTP:
- use cPanel instead - File Manager - public_html -
- wp-content folder > compress > save the zip file download
- to upload you also need to compress the files and upload a zip file > extract to unzip it

wp-config.php

- essential when trouble shooting or setting up a multi-site (also need to edit .htaccess)
- Editing wp-config.php: https://developer.wordpress.org/advanced-administration/wordpress/wp-config/

## Introduction to phpMyAdmin

- phpMyAdmin is a browser based tool
- LocalWP uses AdminerEvo
- you can also use cPanel, or plugins like SQL Buddy, Advanced Database Cleaner, or WP phpMyAdmin but remember to delete the plugin when you are done
- cPanel > Databases > phpMyAdmin - once inside click on the database name to see all the tables - if you have more than one DB becuase you have multiple sites, go to the admin dashboard > Tools > Site Health > Info > Database > Database name
- the 2 most important tables:
  - `wp_options`: stores info about your site's settings
  - `wp_posts`: all the posts and pages, attachments, custom post tables

wp_options

- notice the columns `option_name` and `option_value`
- from Settings > General

wp_posts

- `guid` - the post url

## What is WordPress Multisite?

- to manage multiple WP sites from a single installation - to manage multiple sites without multiple logins
- multiple sites that all run on the same WordPress installation
- each site/sub-site share the same theme and plugins - they each have separate media directory and database tables
- you can updates themes and plugins for all of them at once
- these are usful when running the same site in multiple languages, a media company managing regional news sites under one network, a university providing each department with its own website
- they can be setup in 2 ways: sub-directories and sub-domains
  - sub-directories: `yourdomain.com/support`
  - sub-domains: `support.yourdomain.com` - tend to look different
- Super-admin vs site-admin -
  - Super-admin or network admin manages the entire network of sites
  - Site admin manages individual sites within the network - can add users but can't manage themes or plugins but may be able to activate or deactivate themes and plugins

## Managing a WordPress Multisite network

The network admin dashboard

- Sites: new sidebar link to manage the sites
- also Users, Themes, Plugins, Settings
- Settings is where you manage your multi-site network
  - Operational Settings: netwrk title and admin email
  - Registration Settings:
  - New Site Settings: emails sent
  - Upload Settings: control file uploads lize size limits
  - Language Settings
  - Menu Settings - which menus are available for site admins

The first thing you want to do is create a sub-site

- when you do click "Edit" - options are Info, Users, Themes (different themes?), and Settings
- it's possible to set a top level/apex domain for a site on the network - useful if you or the site admin wants to use a different domain for a site on the network
- for that to be possible, you need it to point to the same ip address as the multi-site install (A Record?)

The network settings page

- Settings > Network Settings >

> Check out Network Admin: https://developer.wordpress.org/advanced-administration/multisite/admin/ and
> Network Admin Settings Screen: https://developer.wordpress.org/advanced-administration/multisite/admin/settings/

## Unlocking advanced SEO techniques: Part 1

- Yoast (or RankMath)

1. robots.txt file > tells search engines which pages of your site they should crawl and which to ignore - you can edit the file from the admin dashboard
   1. Yoast > Tools > File Editor >
2. Canonical urls: `rel="canonical"` - lets you tell search engines that certain pagges are the same - you hurt your rankings if you don't use this
   1. go to a post or page > go to Advanced in the Yoast settings > enter the full canonical url???
3. Sitemaps: Yoast > Settings > Site Features > click on View XML sitemap - how do you edit it? Then submit it to Google Search Console
4. Meta tags:

> Sucks

## Unlocking advanced SEO techniques: Part 2

Structured Data

- helps search engines understand the context of your content
- makes your content eligible for rich snippets
- you can use a plugin to automatically create it
- Yoast > Settings > Post > Schema > leave first select list as default but change second to Blog Post
- you can add schema markup for individual pages and posts
- ypoast rich snippets is for the premium plugin
- schema.org -

```html
<script type="application/ld+json">
  {
    "@content": "https://schema.org"
    "@type": "Product",
    "name": "Smartphone",
    "price": "299.99",
    "currency": "USD"
  }
</script>
```

Open Graph Protocol

- allows you to control how your content appears when shared on social media platforms
- RankMath provides this in the free version

> Conduct regular SEO audits using Google Search Console, Screaming Frog, or ahrefs - and follow SEO Blogs

Schema markup

- ???

SEO Blogs:

1. Positional: https://www.positional.com/blog
2. Backlinko: https://backlinko.com/
3. https://www.growth-memo.com/
4. https://ahrefs.com/blog/
5. https://www.semrush.com/blog/
6. https://www.searchenginejournal.com/

## Troubleshooting your site: Plugin and theme conflicts

- White Screen of Death (WSOD): memory limits, php errors, db issues, plugin and theme conflicts
- plugin and theme conflicts: code incapatibility, JS errors, deprecated Fxs that use outdated WP features,

Troubleshooting steps

- approach methodically
- before making changes, make a backup
- develop locally or use staging - for staging use a plugin or your hosting company may provide them
- use error logs - ways to enable error logging:
  - install a debugging plugin: Debug Bar, Query Monitor, ...
  - edit wp-config.php: under the debug link comment add `define('WP_DEBUG', true);` | `define('WP_DEBUG_DISPLAY', false);` | `define('WP_DEBUG_LOG', true);` - when finished, remove them or switch the booleans
  - check for theme issues - chab=ge to a default WP theme - if you can't get in the dashboard, use file manager to rename your active theme
  - check for plugin issues - automatic rollback feature
  - Health Check & Troubleshooting plugin

```php
define( 'WP_DEBUG', true );
define( 'WP_DEBUG_DISPLAY', false );
define( 'WP_DEBUG_LOG', true );
// when resolved replace all above with:
define( 'WP_DEBUG', false );
```
