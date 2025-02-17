# Publishing Themes

## The WordPress.org Theme Directory

> https://learn.wordpress.org/lesson/the-wordpress-org-theme-directory/

- One of the most popular ways to to publish your theme is to submit your theme to the WordPress.org theme directory

### What is the WordPress.org theme directory?

The WordPress.org [theme directory](https://wordpress.org/themes/) is a repository of free, GPL-licensed themes that have been reviewed and approved by the WordPress theme review team.

One of the benefits of publishing your theme in the WordPress.org theme directory is that it gives you access to a large audience of WordPress users.

Folks can either download the theme from the online theme directory or install it directly from the Themes page in their WordPress dashboard.

### Why publish your theme in the WordPress.org theme directory?

Besides the fact that WordPress users can search for and install your theme right from their WordPress dashboard, there are additional features you have access to when you publish your theme in the WordPress.org theme directory, including:

#### Theme updates:

You are able to push updates to your theme, and users who have your theme installed will be notified in their WordPress dashboard when an update is available.

#### Support forums:

The theme directory has built-in support forums where you can provide support to users who have questions or issues with your theme.

#### Theme preview:

The theme directory supports a live preview of your theme so users can see what it looks like before installing it.

#### Theme statistics:

You are able to see how many users are actively using your theme, as well as how many people have downloaded your theme.

#### Theme ratings and reviews:

Users can rate and review your theme, which you can use to help add features and improvements and grow your user base.

### How to submit your theme to the WordPress.org theme directory

There are a series of steps you need to follow to submit your theme to the WordPress.org theme directory. Here’s a high-level overview of the process:

**Step 1**: Check for required theme files – make sure your theme contains the minimum required files for submission.

**Step 2**: Test your theme – use tools like the Theme Unit Test data, the theme-sniffer extension for PHP_CodeSniffer, and the Theme Check plugin to test your theme for errors, and fix them.

**Step 3**: Follow the Theme Review Guidelines – read through and understand the [theme review guidelines](https://make.wordpress.org/themes/handbook/review/required/), and make sure your theme meets all these requirements.

**Step 4**: Prepare documentation – Create documentation detailing the theme’s features, customization options, and any unique aspects of the theme to be included in either your theme’s readme.txt file or via the theme download page.

**Step 5**: Submission and review process – Submit your theme to the WordPress.org theme directory, and wait for the theme review team to review your theme. This process can take a few weeks, depending on the volume of themes being submitted.

### Summary

The WordPress.org theme directory is one of the best places to publish your theme. It gives you access to a large audience of WordPress users, and provides you with useful features to support and improve your theme.

. . . . . . .

## Required theme files

> https://learn.wordpress.org/lesson/required-theme-files/

When you submit your theme to the WordPress.org theme directory, there are a set of required theme files that you need to include in your theme.

### Block themes

- style.css
- index.html
- theme.json
- readme.txt
- A screenshot file

### theme.json

The theme.json file is used to define the global styles and settings for your theme.

Create Block theme creates a theme.json file for you, which includes some default global styles and settings.

If you don’t have a theme.json file, you can use this template to create one in the root of your theme.

```json
{
  "$schema": "https://schemas.wp.org/wp/6.5/theme.json",
  "version": 2,
  "settings": {},
  "styles": {}
}
```

### readme.txt

Originally required for plugins, the readme.txt file is used by both plugins and themes to provide more information about them.

For themes, the information from the readme.txt is displayed on the theme’s page in the WordPress.org theme directory.

This file should include information about the theme, such as the theme name, description, version number, author, and other details.

The [WordPress readme file](https://wordpress.org/plugins/readme.txt) standard contains the details of the type of information that you can use in your readme.txt file.

There is also a [readme validator](https://wordpress.org/plugins/developers/readme-validator/) that you can use to check if your readme.txt file is formatted correctly.

### Screenshot

The screenshot file is used to display a preview of your theme in the WordPress.org theme directory, as well as in the theme directory page in the WordPress admin area.

This file should be a PNG or JPG image, and should be no bigger than **_1200 x 900_** pixels in size.

If you use Create Block Theme to create your theme, a default screenshot file is automatically generated for you, but it’s best to replace this with a custom screenshot that showcases your theme.

### Classic themes

If you are submitting a classic theme, the required files are slightly different.

- style.css: his shows css styles in the file?!?
- index.php
- comments.php
- readme.txt
- A screenshot file

Check out the [Theme structure](https://developer.wordpress.org/themes/core-concepts/theme-structure/#required-files) chapter in the WordPress theme developer handbook

. . . . . . .

## Preparing your theme for submission

> https://learn.wordpress.org/lesson/preparing-your-theme-for-submission/

...how to prepare your theme for submission, including how to test your theme, check and follow the theme review guidelines, and prepare documentation for your theme

### Testing your theme

Before submitting your theme to the WordPress.org theme directory, you should test it thoroughly to ensure that it works as expected.

This includes testing things like whether it has any errors or warnings, how it handles different types of content, and how it performs in terms of accessibility and performance.

It can also be beneficial to test your theme against the next version of WordPress to ensure that it remains compatible.

To do this, you can install the [WordPress Beta Tester](https://wordpress.org/plugins/wordpress-beta-tester/) plugin, which allows you to switch your site to the latest beta or release candidate version of WordPress.

### Theme review guidelines

The WordPress [theme review guidelines](https://make.wordpress.org/themes/handbook/review/required/) are a set of requirements that you need to follow when submitting your theme to the WordPress.org theme directory.

These guidelines cover a wide range of topics, including:

1. Licensing & copyright
2. Privacy
3. Accessibility
4. Code requirements
5. Functionality and Features
6. Plugins
7. Naming, spelling, and trademarks
8. Language and internationalization
9. File requirements
10. Classic theme requirements
11. Block theme requirements
12. Theme settings pages and onboarding
13. Upsells, credits, links, and spam
14. Theme author and theme upload restrictions

Your next step is to review every single item in the theme review guidelines, and make sure your theme meets all these requirements.

If you’ve thoroughly tested your theme using the tools mentioned in the Testing your theme lesson, you should have already addressed many of the issues that the theme review guidelines cover.

It’s still a good idea, however, to work through them all and check each one off before you submit.

During the submission process, a theme that contains 3 or more distinct issues according to these guidelines, may be closed as not-approved.

It is possible to resubmit your theme after fixing the issues, but it’s going to delay the process.

### Preparing documentation

The final step in preparing your theme for submission is to create documentation that details the theme’s features, customization options, and any unique aspects of the theme.

Themes are required to provide end-user documentation of any design limitations or extraordinary installation/setup instructions.

Depending on how detailed your documentation needs to be, will determine where you add this information.

While you could add this to your theme’s readme.txt file, it’s often easier to provide this information on a dedicated theme homepage.

Many theme developers create a page on their website that provides detailed information about the theme, including installation instructions, customization options, and any other relevant information.

They will then link to this page using the theme’s `Theme URI` field in the `style.css` file.

This link will display on the theme’s page in the WordPress.org theme directory and in the WordPress admin, and users can click on it to access the theme documentation.

. . . . . . .

## Submitting your theme to WordPress.org

> https://learn.wordpress.org/lesson/submitting-your-theme-to-wordpress-org/

When you’ve made sure your theme includes all the required files, passes the theme review guidelines, and you’ve thoroughly tested your theme, you’re ready to submit your theme to the WordPress.org theme directory

### Archive your theme

The process of uploading your theme for review requires you to upload a zip file of the entire local theme directory.

There are a number of ways to achieve this, from using the terminal to using your operating system’s file manager.

The zip file should contain the theme files inside the theme directory.

Make sure not to include any files that are not part of the theme, such as version control files, package dependency files, or any other files that are not required for the theme to function.

### A note on the theme name

It’s important to note that the theme name as it’s registered on the WordPress.org theme directory, sometimes also called the theme slug, is determined by the name of the folder of your theme when you create it on your local computer.

When you create the zip file, the theme folder with all the theme files are archived inside the zip file.

When a new theme is submitted, the theme name is automatically generated from that folder name. This name is then used everywhere in the theme directory, from the theme URL to the location of the theme’s code repository on WordPress.org.

_It's a good idea to choose a theme name that is unique_ and that reflects the title of your theme.

### Upload your theme

Once you have the zip archive ready, you can upload it to the WordPress.org theme directory.

To do this, browse to [https://wordpress.org/themes/upload/](https://wordpress.org/themes/upload/).

You will be required to log in with your WordPress.org account. Once you’re logged in, you can upload your theme by clicking on the Choose File button, and selecting the zip archive of your theme.

You will also be required to confirm that you have permission to upload the theme, that it complies with the theme review guidelines, and that it is GPL-compatible.

Once you’ve checked all those boxes, click the Upload button to upload the theme for review.

### Theme review process

Once the theme is uploaded, a number of actions take place automatically.

The theme files are extracted, and the new theme is created in the WordPress.org theme directory. This means that the theme has a theme URL, based on the theme name, as well as an SVN repository for the theme code, all hosted in the WordPress.org infrastructure. The process will also run the theme through a series of automated checks, the same checks as in the Theme Check plugin.

The theme is then added to the review queue, where it will be reviewed by a member of the WordPress theme review team. This queue is managed in software called [Trac](https://trac.edgewall.org/), which is a bug-tracking system used by the WordPress community.

A new trac ticket is opened, and the theme details are added to the ticket. The theme reviewer will then download the theme and review it against the theme review guidelines.

If a theme ticket has no update from the theme reviewer within the first 48 hours after assignment, you can request that the theme is returned to the new queue, and a new reviewer is assigned.

Any communication between the theme reviewer and the theme author will take place in comments in the trac ticket, and the theme author will be notified of any issues that need to be addressed.

Trac automatically sends an email to the theme author when the ticket is updated, so it’s important to keep an eye on your email for any updates. This will be the email you used when you registered your WordPress.org account.

If a theme ticket has no update from the theme author for 7 days it may be closed due to inactivity.

Once a theme passes all required checks, the reviewer marks the theme as approved. The theme is then added to a final review queue in trac, where a key reviewer will do the final review.

If the theme passes the final review, it is marked as live, and the theme will show up in the WordPress.org theme directory.

. . . . . . .

## Updating your theme

> https://learn.wordpress.org/lesson/updating-your-theme/

Once your theme is live on the WordPress.org theme directory, you may need to update it from time to time. This could be to fix bugs, add new features, or generally improve it.

There are two ways to update your theme on WordPress.org:

1. uploading a new zip file or
2. using Subversion (SVN).

### Uploading a new zip file

The most straightforward way to update your theme is to upload a new zip file to the WordPress.org theme directory.

Once you’ve made any changes to your theme files, you’ll need to update the version number in the style.css file.

```css
/*
 * Theme Name: Twenty Twenty-Four
 * Version: 1.2
 */
```

This is important, as it tells WordPress that a new version of the theme is available.

You then create a new zip file of your theme directory, using whatever method you used when you first submitted it.

Finally, browse to https://wordpress.org/themes/upload/, and follow the same process to upload the zip file.

### Using Subversion (SVN)

An alternative to the zip upload method is to use Subversion (also known as SVN) to update your theme.

[Subversion](https://subversion.apache.org/) is a version control system similar to Git that allows you to manage changes to your code.

When the WordPress plugin repository was first created, Subversion was used to allow developers to manage updates to plugins and themes.

This was mostly because Git and GitHub did not exist, and Subversion was the default version control software open-source developers used.

It, therefore, made sense to use the same system for the WordPress theme directory when it launched a few years later.

To use Subversion to update your theme, you install Subversion on your local machine and then use it to commit your changes to the WordPress.org theme directory.

One of the benefits of using Subversion is that it allows you to keep track of changes to your theme over time, and easily roll back to a previous version if needed.

You can find the Subversion Repository URL on your theme’s page in the directory, under Browse the code.

For example, the URL for the Twenty Twenty-Four theme is:

    https://themes.svn.wordpress.org/twentytwentyfour/

### macOS and Linux

> SKIP

### Windows

For Windows users, you can download and install [TortoiseSVN](https://tortoisesvn.net/), which provides a graphical interface for managing your Subversion repositories.

TortoiseSVN integrates with Windows Explorer, so you can right-click inside a folder and select the **TortoiseSVN -> Checkout** option to download the theme files to your local machine.

It’s a good idea to create a folder specifically for your theme files and check out the repository into that folder.

It will ask you to provide the URL of the Subversion Repository, which you can find on your theme’s page in the directory.

Once it’s checked out, you can create the new version of the theme by either creating a new folder and copying the files across, or by copying and pasting the existing folder, and then renaming it.

Now, you can make changes to the theme files in the new directory.

Make sure to update the version number in the `style.css` file to match the new version and update the changelog in the `readme.txt`.

Once you’re ready to commit the new version of the theme, you can right-click inside the main folder and select the **TortoiseSVN -> Commit** option.

This will open a dialog box where you can enter a commit message, select all the files to commit, and then click OK to commit the changes.

As with macOS and Linux, you will be asked for your username and password during the commit process. This is the same username and password you use to log in to the WordPress.org theme directory.

### After a successful commit

After a successful commit, you will receive an email from WordPress.org to confirm that the new version of your theme has been uploaded.

It may take some time to reflect on the WordPress.org directory, but the updated version is usually available within a few hours.
