# An introduction to WordPress multisite

> SKIP THIS ENTIRE SECTION

## Setting up a WordPress multisite network

- https://learn.wordpress.org/lesson/setting-up-a-wordpress-multisite-network/

A WordPress multisite network is a way to host multiple WordPress sites on a single WordPress installation

### What is a WordPress multisite network?

A WordPress multisite network is a collection of WordPress sites that share a single WordPress installation. With a multisite network, it’s possible to allow users to create their own sites, or configure the network so that only administrators can create sites. These sites are known as “subsites” or “individual sites” on the network

All sites on a multisite network use the same WordPress installation files and share the same plugins and themes. Plugins and themes are installed on the network and then activated on individual sites

Each individual site has separate directories for media uploads within the shared installation and separate tables in the database for site content

### Why use a WordPress multisite network?

A multisite network is a good solution where you have a number of sites that are similar in nature, but that need to be kept separate from each other. Examples of this include higher education websites, non-profit organizations, and open-source projects.

### Multisite network support

The web host or local development environment you use will determine how you create a multisite network either locally, or on a live server. The two common options are either to offer a setting that you enable during the new installation process, to set up the new installation as a multisite network, or to follow the manual steps to setting up a multisite network after WordPress is installed.

Web hosts and local development environments that use the Apache web server generally allow you to convert an existing WordPress install into a multisite network using the manual method. Those who use Nginx generally require you to create a multisite network during the new site creation process. This is because by default nginx doesn’t support the .htaccess file that is used to enable multisite manually.

Whether you use a web host or local development environment that enables multisite automatically or manually, it’s a good idea to understand the additional steps needed to create a multisite network from a WordPress install, which is what this lesson will focus on.

### How to create a multisite network

Before you create your multisite network, make sure to read the [Before You Create A Network](https://wordpress.org/documentation/article/before-you-create-a-network/) page in the developer documentation, as it covers some important considerations you need to be aware of before you create a multisite network.

Next, you should make a backup of the current site files and database. At the same time, you should make sure that Permalinks work on the site, and that any plugins installed are deactivated.

Finally, if you want to have your WordPress install running in its own directory, make sure to do that before you create the multisite network

### Enable Multisite

To enable multisite, you need to edit the wp-config.php file in the root directory of your WordPress install and define the PHP constant WP_ALLOW_MULTISITE as true

```php
define( 'WP_ALLOW_MULTISITE', true );
```

Then, refresh your WordPress dashboard. By setting this constant, you’ll now see a new menu item in the dashboard under the Tools menu called “Network Setup”.

### Installing the Network

The Network Setup page will walk you through the steps to create your multisite network.

First, you’ll need to choose whether you will use subdomains of your top-level domain as addresses for the sites on the network, or subdirectories. Subdirectories are easier, as you don’t require any additional DNS configuration, but subdomains give the sites a more professional-looking URL. To use subdomains, you will need a wildcard DNS record for your top-level domain.

You can leave the rest of the settings as is, or change them to your liking.

Once you’re ready, click the “Install” button.

WordPress will now run the network installation, creating any database tables required, and adding any specific data needed to those tables.

### Enable the Network

Once the installation is complete, you’ll need to enable the network, This is done by making two changes:

1. Edit the `wp-config.php` file again, and add the constants described at step one of the Enabling the Network page in the dashboard

```php
define('MULTISITE', true);
define('SUBDOMAIN_INSTALL', true);
define('DOMAIN_CURRENT_SITE', 'My Website');
define('PATH_CURRENT_SITE', '/');
define('SITE_ID_CURRENT_SITE', 1);
define('BLOG_ID_CURRENT_SITE', 1);
```

2. Edit the `.htaccess` file in the root directory of your WordPress install, and add the rules described at step two of the Enabling the Network page

```apacheconf
# BEGIN WordPress Multisite
# Using subfolder network type: https://wordpress.org/documentation/article/htaccess/#multisite

RewriteEngine On
RewriteRule .* - [E=HTTP_AUTHORIZATION:%{HTTP:Authorization}]
RewriteBase /
RewriteRule ^index\.php$ - [L]

# add a trailing slash to /wp-admin
RewriteRule ^([_0-9a-zA-Z-]+/)?wp-admin$ $1wp-admin/ [R=301,L]

RewriteCond %{REQUEST_FILENAME} -f [OR]
RewriteCond %{REQUEST_FILENAME} -d
RewriteRule ^ - [L]
RewriteRule ^([_0-9a-zA-Z-]+/)?(wp-(content|admin|includes).*) $2 [L]
RewriteRule ^([_0-9a-zA-Z-]+/)?(.*\.php)$ $2 [L]
RewriteRule . index.php [L]

# END WordPress Multisite
```

Once you’ve made these changes, refresh your WordPress dashboard, and you will be asked to log in again.

You will be redirected back to the “Network Setup” page, but you will notice you are now logged in as the network admin, and you have a different set of menu options for your newly created Multisite network

. . . . . .

## Managing a WordPress multisite network

- https://learn.wordpress.org/lesson/managing-a-wordpress-multisite-network/

### The Network Admin dashboard

Once you have enabled your multisite network, your Admin user will change to a Super Admin and will have access to the Network Admin dashboard. Here, you can manage sites, users, themes, plugins, and settings for the network.

### The Network Settings page

The Network Settings page is where you manage your multisite network.

The Operational Settings allow you to set the Network Title and Admin Email

The Registration Settings allow you to set the registration options for the network. For example, if you want to allow users to register new sites on the network, you can enable the “Both sites and user accounts can be registered” option. You can also set banned names for new sites, limit registrations by certain email domains, and ban registrations by certain email domains

New Site Settings controls what emails are sent and what content is created when creating a new site on the network.

Upload Settings controls file uploads, including file size limits, and allowed file types.

Language Settings allows you to control the default language for new sites on the network.

Finally, the Menu Settings allows you to control which menus are available to site admins.

### Create a site

One of the first things that you might want to do is create a sub-site. To do this, go to the Sites page, and click the “Add New” button. You’ll be asked to enter the site address (either a subdomain or a subdirectory), the site title, site language, and the site admin email address. If you use an email address of an already existing user, that user will be added as the site admin. Otherwise, a new user will be created and made admin of the new site

Once the site is created, you can edit the site by clicking on the Edit button in the Sites list.

The Info tab manages the site address, shows when the site was registered and last updated and manages the site attributes

The Users tab allows you to add existing users to the site, or add new users to the site.

The Themes tab allows you to activate a theme for the site. The themes available here are the themes that are not activated for the entire network. This means you can have specific themes only available for specific sites on the network.

The Settings tab contains all the rest of the site settings that you can manage.

### Assign a top-level domain to a site

It is also possible to set a top-level or apex domain for a site on the network. This is useful if you or the site admin wants to use a different domain for a site on the network.

In order for this to be possible, you need to have registered the domain with your domain registrar and have it pointed to the same location as the multisite install.

In this case, you can see the new top level domain is pointing to the same location as the multisite install, as it redirects to the multisite URL.

Then, in the Network Admin, edit the site in question, and change the Site Address field to the new top-level domain.

Now, when you browse to that domain, you will be redirected to the associated site on the network.

### Allow users to register their own sites

Depending on how you plan to use your multisite network, you might want users to be able to register their own subsites. To do this, go to the Network Settings page, and enable the “Both sites and user accounts can be registered” option.

Now, if a user browses to the default WordPress registration URL, they will see an option to also register a site one the network.

    https://multipress.test/wp-login.php?action=register

After entering their username and email address, they will be asked if they want to create a site, or just register a user account on the network.

If they choose to create a site, they will need to set the site name and title.

Once they click signup, the site will be created and the user will be sent an email to activate the new site, after which they will be able to log in to the subsite.

. . . . . .

## Advanced multisite management

- https://learn.wordpress.org/lesson/advanced-multisite-management/

### Site Status

There are some site status options that are available to a Network Admin, that are useful to know about.

Deactivating a site will update the site status to deleted, and shows a message to anyone visiting the site. Additionally, there is a `deactivate_blog` action hook when a site is deactivated, and a `activate_blog` action hook when a site is activated, that can be used to run additional functionality when a site is activated or deactivated.

Archiving a site will update the site status to archived and show an archived message to anyone visiting the site URL.

Marking a site as Spam will update the site status to spam and show the same message as archiving, but no additional hooks are fired.

### Deleting a site from the network

Deleting a site from the network will remove all content associated with the site, including posts, pages, comments, and any other custom content types. It also removes any tables in the database that were used to house the site’s content. Unlike when you trash a post or page, once you delete a site, you cannot undo this action.

### Export a site to a single site install

Under certain circumstances, you might want to extract one of the sub-sites to its own single-site WordPress install. This is possible but requires some manual steps. There are a few ways to do this, this is just one possibility.

First, log into the subsite, and browse to the `Tools` > `Export` page.

You can use the WordPress export tool to export the content to the WordPress `eXtended RSS` or `WXR format`.

Then create the new single site and the associated user.

Make sure to install any plugins and the themes used on the sub-site.

Then browse to `Tools` -> `Import` to use the WordPress importer to import the data into the new site. You may need to install the importer by clicking `Install Now` under the WordPress option, and then clicking `Run Importer` once it’s installed.

Don’t forget to assign the data to the relevant user on the new site.

Once the data is imported, manually copy the uploads directory for the sub-site over to the new single-site install.

You will find the subsite uploads directory in `wp-content/uploads/sites/` directory of the multisite install, in a folder with the same name as the sub site id.

Last but not least run a search and replace tool like `Better Search Replace` to update any URLs in the database.

You will need to replace the sub-site URL (either the subdomain or sub-directory version) with the new single-site URL. If you were pointing a top level domain to the subsite, this step might not be necessary.

Lastly, test everything out to make sure it’s working as expected.

An alternative to the WordPress data export option is to manually copy the database tables for the sub-site to the new site. However, this might lead to further issues if the content isn’t associated with the correct user.

### Considerations

If you have any plugins that create custom database tables, you might need to manually copy these tables over to the new installation.

In that case, it might be easier to rely on paid third-party backup solutions that have multisite extensions and will handle this for you.

### Convert a Multisite back to a single site install

It’s also possible to convert a multisite back to a single site install. This is useful if you no longer need the multisite functionality, but want to retain the original site.

If you have other sub-sites, it might be a good idea to export them to single-site installs first, as this will delete the sub-site content tables. Additionally, delete any users that were created for the sub-sites.

To revert back to a single site, you first need to remove all multisite-related constants in wp-config.php.

Once you do this, your dashboard will revert back to a single-site dashboard.

Then, if you previously updated the .htaccess file, you will need to revert that back to the original .htaccess file.

You can do this by resetting permalinks to whatever you want them to be.

Lastly, delete any tables specifically created during the multisite installation, namely:

`wp_blogmeta`, `wp_blogs`, `wp_registration_log`, `wp_signups`, `wp_site`, `wp_site_meta`

If everything went well, you should now have a working single-site installation of your main site.

> [WordPress Multisite / Network](https://developer.wordpress.org/advanced-administration/multisite/)

. . . . . .

## Developing for a multisite network

- https://learn.wordpress.org/lesson/developing-for-a-multisite-network/

### Note on naming conventions

There are a couple of different naming conventions used in the WordPress codebase when it comes to multisite.

WordPress multisite was originally known as WordPress MU (or WordPress multi-user), and many multisite-related functions and hooks use the wpmu\_ prefix.

Additionally, some functions are named based on the old terminology which described multiple “blogs” on a “site”. This has since been updated to describe multiple “sites” on a “network” instead, but some old terminology still lives on in some function names.

### Useful functions

The first is the `is_multsite` function. This function will return true if multisite is enabled, and is probably the most widely used function related to multisite. If you do a search through the WordPress codebase for uses of the is_multsite function, you’ll see that it’s used in a number of places, to either perform specific tasks in the context of a multisite network or to restrict functionality only to multisite networks

There are also some common functions that are useful when developing administration interfaces for a multisite network:

- `is_super_admin` can be used to check if the currently logged-in user is a Network Administrator on the network.
- `is_network_admin` is the multisite equivalent of the is_admin function and determines whether the current request is for the network administrative interface.
- `network_admin_url` is the multisite equivalent of the admin_url function and allows you to create URLs relative to the admin area of the network. This is useful for redirecting to different areas of the network admin dashboard.

When working with site content, there are some functions that are widely used.

`is_main_site` determines whether the current site is the main site of the current network or not.

Next, there is the `get_sites` function, which will return a list of sites matching the requested arguments.

Then there is `switch_to_blog`, which allows you to switch to a different site in the network, `restore_current_blog` which restores the current site after you’ve switched to a different site and `get_current_blog_id`, which returns the ID of the current site.

Using these functions, you can perform actions across the network.

- `get_sites`
- `update_blog_option`
- `is_network_only_plugin`

### Useful hooks

The first is the `network_admin_menu` hook, which allows you to add menu items to the network admin dashboard. This is useful if you want to add a custom menu item to the network admin dashboard.

The second is the `network_admin_notices` hook, which allows you to add notices to the network admin dashboard. This can be used to display a notice to network admins, in the same way that admin_notices is used for single-site notices

`signup_blogform` is a filter that allows you to modify the signup form for new sites. You can use this to add additional fields to the signup form.

`wp_initialize_site` is an action that is fired when a new site is created. This is useful if you want to perform actions when a new site is created, for example if you wanted to assign a custom top level domain to a sub-site.

### Developing for individual sites in a network

When you are rendering any content in the scope of a single site on the network, WordPress core is clever enough to know that you are working inside the scope of that site.

This means that any functions that you use to retrieve information, such as `get_bloginfo`, `get_option`, `get_posts`, or `get_post_meta`, and any functions you might use to add or update information, like `update_option`, `wp_insert_post` or `update_post_meta`, will get, add or update the correct tables for the site that you are currently working with.

Additionally, if you use functions like `register_post_type` or `register_taxonomy`, these will be registered for the current site only.

. . . . . .

## Building plugins abd themes that support multisite

- https://learn.wordpress.org/lesson/building-plugins-and-themes-that-support-multisite/

### Developing themes and child themes

Generally, themes and child themes work exactly the same on a multisite network as they do on a single site. Once a theme or child theme is network activated, it can be activated on any single site on the network

- switch_to_blog, restore_current_blog, is_main_site

### Developing plugins

most plugin functionality will work the same in a single site as well as a multisite. Functions like `register_post_type` or `get_posts` will function in the same way, just in the scope of the specific site in question

However, there are two things to consider when developing plugins for multisite.

Plugins often have a settings page, which is usually accessible from the admin dashboard. This is fine for single-site plugins, but on a multisite network, you need to consider where the settings page should be located. Should it be on the network admin dashboard, or on the individual site dashboard?

If you need to have a settings page on the network admin dashboard, you can use the `network_admin_menu` hook to add a menu item to the network admin dashboard. If you need to have a settings page on the individual site dashboard, you can use the `admin_menu` hook to add a menu item to the individual site dashboard

Plugins might have to add custom tables to store custom data. If you use something like the `$wpdb->prefix` variable to prefix your table names, you’ll end up with a table name that is prefixed with the site ID. So if you need to have a custom table for this functionality on a per-site basis, you need to plan for it.

> Skip the majority of the rest of the text

- register_activation_hook

...to view a list of all multisite-related functionality by browsing to the [multisite package](https://developer.wordpress.org/reference/package/multisite/) section of the WordPress code reference
