# Completing your Custom Theme

## Completing your custom theme: Taking a screenshot

> https://learn.wordpress.org/lesson/completing-your-custom-theme-taking-a-screenshot/

- Now is the time to showcase what your theme will look like on a sample website. Theme designers carefully select images and generate content on this sample theme website in order to take its screenshot
- You can use a plugin such as FakerPress or Lorem Ipsum text to generate sample content that can be easily deleted once you are done
- In FakerPress, use LoremPicsum to pull random images that you can use for your sample website
- Select images of your own to use for your demo website to help demonstrate the theme’s purpose and reach your audience
- IMPORTANT NOTE: Images you add to your media library to create your demo website do not transfer to your theme - it’s a best practice to only use images for your theme’s example image
- we recommend not including images in your actual theme design

> 1200px wide and 900px tall .png - Name this photo `screenshot.png`

.....................................................

## Completing your custom theme: Adding informations in style.css

> https://learn.wordpress.org/lesson/completing-your-custom-theme-adding-information-in-style-css/

### Adding Content in style.css

you have the option to add any or some of the following information to this - Items indicated with (`*`) are required for a theme in the WordPress Theme Repository

- Theme Name (`*`): Name of the theme.
- Theme URI: The URL of a public web page where users can find more information about the theme.
- Author (`*`): The name of the individual or organization who developed the theme. Using the Theme Author’s wordpress.org username is recommended.
- Author URI: The URL of the authoring individual or organization.
- Description (`*`): A short description of the theme.
- Version (`*`): The version of the theme, written in X.X or X.X.X format.
- Requires at least (`*`): The oldest main WordPress version the theme will work with, written in X.X format. Themes are only required to support the three last versions.
- Tested up to (`*`): The last main WordPress version the theme has been tested up to, i.e. 5.4. Write only the number, in X.X format.
- Requires PHP (`*`): The oldest PHP version supported, in X.X format, only the number
- License (`*`): The license of the theme.
- License URI (`*`): The URL of the theme license.
- Text Domain (`*`): The string used for textdomain for translation.
- Tags: Words or phrases that allow users to find the theme using the tag filter. A full list of tags is in the Theme Review Handbook.
- Domain Path: Used so that WordPress knows where to find the translation when the theme is disabled. Defaults to `/languages`.

For a child theme

```css
/*
Theme Name: My Child Theme
Template: twentytwenty
*/
```

Notes:

1. Theme URI: This gets created after a page is approved to appear in the WordPress.org theme repository - This URI can be a simple link, such as to a Github page where your theme files and description can live, or a simple website describing the features of your theme - This theme URI should not point to a personal website
2. Author: Using the Theme Author’s WordPress.org username is recommended - For theme distribution, you cannot put multiple theme authors; only one author is allowed - You can add your username, company, and/or your own name
3. Author URI: An Author URI is not required to distribute your theme, but a link to your personal website, blog, or company website is allowed here - This could be a link to their Github user profile, or it could be a general website such as yourname.com - Nothing about the theme needs to exist on your Author URI website, just information about you as the author - You should not have both URIs (Theme URI and Author URI) pointing to the same link; your theme URI should be different than your author URI
4. Description: This field should be a description of your theme; you should not mention any pro version features here. It should describe the free theme only. This description should mention features that are relevant to someone searching for a theme like yours, but it shouldn’t be a comma separated list
5. Version: Your theme versions should be incremental, because that is how WordPress recognizes the new version - How often you update your theme is up to you as the developer
6. Tags: Only mention a tag for a feature that is actually included in your theme - If you add accessibility-ready tag to your theme, your theme will also go through a accessibility review to make sure that your theme is actually accessible

- View a list of allowable tags here https://make.wordpress.org/themes/handbook/review/required/theme-tags/

> GOOD

.....................................................

## Theme enhancements - offering reusable blocks, unique templates, unique patterns, style variations

> https://learn.wordpress.org/lesson/theme-enhancements-offering-reusable-blocks-unique-templates-unique-patterns-style-variations/

- Reusable Blocks, Block Patterns, Templates & Template Parts
- Style Variations: a different color scheme, font choice, and other stylistic variations that a user can access to quickly change the look and feel of a theme
- Utilize the Create Block Theme plugin to create style variations
- This will essentially create multiple theme.json files in a new 'styles' folder, which allows you to pick different variations of colors, fonts, and options in the site editor

### Unique Templates

- index template, page template, 404, ...
- These custom templates allow users to select different theme templates to apply to individual posts or pages, giving users more options for the layout of a theme
- A user could choose to apply a unique template in their post or page editor

### Unique Patterns

When you designed your block theme, you may have relied on a variety of patterns that appeared in the site editor to give you a leg up.

Did you know you can also create and surface unique patterns that will only appear in your custom theme

.....................................................

## You're almost finished - what's next

> https://learn.wordpress.org/lesson/youre-almost-finished-whats-next/

### Export or Save Your Theme

Don’t forget to save your theme! You can either export it to make a shiny new copy of your theme, ready to be installed

you can use Create Block Theme to save your changes directly to the theme itself, which will not make a copy

Once you’ve saved all your changes, you have a few final things to do in order to touch up your block theme

### (Optional) Rename Any Custom Templates

When you saved your theme, you may have noticed that some of your templates were renamed inside your site editor to something less desirable. You can rename these templates!

### Finally! Delete Your Style Guide

If you plan on sharing your theme with anyone, it’s a best practice to delete your style guide. That’s why you don’t often see a style guide template in any additional block themes

> ???
