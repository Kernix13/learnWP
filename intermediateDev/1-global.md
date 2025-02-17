# Global Settings and Styles

5 lessons

## Global theme settings

> https://learn.wordpress.org/lesson/global-theme-settings/

- Start by taking a look at the `wp-includes/theme.json` file that comes with WordPress Core. This is where all of the default settings are set up

> in wp-includes/theme.json is `"appearanceTools": false,`

### What settings are available to end users?

...there is a loading hierarchy

1. start off with WordPress Core.
2. Then we move up to Theme.
3. Next, we have Child Theme if it’s available and active.
4. And finally, we have the User Configurations

Whatever a user does within the block or site editor and saves those changes, they will take priority over everything else in the hierarchy

### Using theme.json to control available settings

... under Colors for example, we’ve got Text and here we can apply different colors to the text and this is Site Wide

If we want to work with a block, we select the block and then we go into Settings and then the Styles tab within Settings. You’ll see Color and you choose Text and from there you can change the color of the text but note that **we can’t change the color of links**. In order to do that, we need to work within theme.json

Appearance Tools is an all-encompassing property. It has all of these properties set to False by default from WordPress. If we are developing our theme and we want to, for example, enable all of these, we would just put True for Appearance Tools but for our example, we’re just going to work with the ability to change the color of links

Under Appearance Tools, we’ll add the property Color and then we’ll enter Link and instead of False, we switch it to True and then Save. Now if we go back to WordPress and reload, now this time we should have the ability to change the color of links

refer to the [theme handbook](https://developer.wordpress.org/themes/) on WordPress.org

. . . . . . .

## Block theme styles

> https://learn.wordpress.org/lesson/block-theme-styles/

- explore the style hierarchy
- modify theme styles using the Site Editor and export the changes
- understand how WordPress uses the JSON syntax to generate CSS in a browser
- configure presets via the settings property and apply them in the theme.json styles property

### The WordPress style hierarchy

- root elements, such as body text > The next level is individual elements, such as headings > finally at the top, we have blocks, such as a button block
- So anything that would be applied to the block level would take precedence over all of the other styling within your theme

### Modify theme styles

- modify theme styles using the site editor and export the changes
- The `Create Block theme` plugin is an invaluable tool for any theme developer
- One of the best features using the Create Block theme plugin is the ability to save changes directly to my theme file
- make a change within global styles, such as adding a new color to the custom palette - hit save & this change is saved to the database
- We see the Create Block theme plugin sidebar and the save changes option. This removes the changes from the database and pushes them to the theme files

### How WordPress uses the JSON syntax to generate CSS in a browser

- Inspect the H1 > WordPress takes the settings, color, contrast, and then applies it to the H1 heading
- `--wp--preset--color--contrast` is the class
- in theme.json > settings > color > palette > there is "contrast"
- then styles > elements > heading > color > text > you see
  - `var(--wp--preset--color--contrast)`

### How presets are written within theme.json

- Go into settings and set the `defaultPalette` from WordPress to `false` and then add the property `palette` and start adding colors
- note here that we’re using a generic naming convention as opposed to naming the color
- For instance here is a dark green and instead of using green for the name and slug we just use contrast. This makes it much easier to do color changes going forward and then we see it being applied at the bottom here under styles
- WordPress generates the CSS by creating the class `has-slug-feature`
- ...see how WordPress takes up preset and creates the class has-accent-3-color

```js
settings.color.palette {
  "color": "#d8613c",
  "name": "Accent / Three",
  "slug": "accent-3"
}

styles {
  "color": {
    "text": "var(--wp--preset--{$feature}--{$slug})"
  }
}

// var(--wp--preset--{$feature}--{$slug})
// var(--wp--preset--color--contrast)
```

- wordpress generates `class="has-{$slug}-{$feature}"`

> take a look at the [styles reference guide](https://developer.wordpress.org/themes/global-settings-and-styles/styles/styles-reference/)

. . . . . . .

## Templates

> https://learn.wordpress.org/lesson/custom-templates/

> EXCELLENT VIDEO

1. build a custom template from scratch and export it to your local theme folder,
2. register a custom template using the theme.json file, and
3. familiarize yourself with the workflow of updating templates using the Create Block Theme plugin

### Creating custom templates

The quickest way to build out your theme is to work within the Site Editor, and using a plugin like Create Block theme, you can push your changes directly to your theme files.

### Registering custom templates in theme.json

The custom templates are all registered within theme.json. We have several for pages and one for single posts. We see here that the name corresponds with the name of the file

- template/ shows the .html files
- in theme.json look for `customTemplates`:

```json
"customTemplates": [
  {
    "name": "page-no-title", /* "name" = page-no-title.html */
    "postTypes": ["page"],
    "title": "Page No Title"
  },
]
```

### Adding a new template

create a custom template by first clicking `Add New Template`. We’ll choose `Single Item Post` then `All Posts`. Next, choose a pattern to save time, or you can start from scratch. If you hit Save, the template is saved to the database

If we go into templates, we will see it there, Single Item Post. And if we go into Manage All Templates, we see it there as a user change which means it’s in the database and not part of our theme files just yet

### Using the Create Block Theme plugin to update theme files

In order to export the template, we need to use the Create Block Theme plugin. We start with making changes and saving those changes to the database. And each time, we can save changes using the Create Block Theme plugin (GEAR ICON) to push those changes from the database into our theme files: Click `Save Changes to Theme`

If we go into our code editor, we see the custom template, Single-Post. Now we can rename this if we want to something more descriptive

### Register a custom template

You can now register the new custom template using the theme.json file. This gives us the ability to give the template a custom name

Save those changes and then go back to the Site Editor and reload. Now go into All Templates and scroll down where you can see that

> THAT WAS AN ECELLENT LESSON

. . . . . . .

## Theme Patterns

> https://learn.wordpress.org/lesson/theme-patterns/

> https://wordpress.org/patterns/

- list and describe the sources of patterns available within WordPress
- add the Patterns property to theme.json and list the patterns to include in your theme from the Pattern Directory
- describe the process of building a pattern from scratch in order to bundle it with your theme

### Sources of patterns

When the end user uses the inserter within a page, post or template, they will have access to

1. patterns available within the currently active block theme, which includes the WordPress pattern directory.
2. They will also have access to the WordPress core patterns
3. any custom pattern you build and add to your theme

### Pattern directory

- use theme.json to list patterns from the pattern directory
- Not to be confused with the patterns that are listed within the patterns folder
- These patterns you create yourself to add to your theme and they’re automatically registered as long as they’re in that folder
  - `patterns/my-pattern.php` for example
- but if you go into theme.json > see the comma separated list of the slugs of the patterns that you find within the official WordPress pattern directory

Here is an example of a pattern comment header:

```php
<?php
/**
 * Title: Hero
 * Slug: twentytwentyfour/banner-hero
 * Categories: banner, call-to-action, featured
 * Viewport width: 1400
 * Description: A hero section with a title, a paragraph, a CTA button, and an image.
 */
?>
```

### Creating patterns

- create a pattern from scratch in order to bundle it with your theme
- create your file within the patterns folder
- The file is PHP, however, it has block markup and it also has a file header
- The most common metadata that you will find there is `title`, `slug` and `categories`.
- The HTML markup code of the blocks you need can be generated within the Site Editor.
- Go into the Site Editor and you can always go into the code editor in order to find your code to copy and paste it over into your patterns PHP file

. . . . . . .

## Style Variations

> https://learn.wordpress.org/lesson/style-variations/

- define and describe style variations
- differentiate between theme and style variation JSON files
- differentiate between a child theme and a style variation

### What are style variations?

_Style variations are essentially alternative versions of theme.json that you can ship with your theme_. They are custom named JSON files that are stored in your theme’s `styles` folder

Any setting or style that you can add to theme.json can also be added to your style variation JSON file. This lets your users pick and choose which variation they want to use on their site

You can bundle each of these alternative designs for your theme and let your users decide which is the best option for their site. Within the site editor, users can go into styles and choose a different style combination for their website

in the default Twenty Twenty-Four theme, a user could choose the Ember variation. What that means is within global styles, they have a different palette and they have these four colors available. Within the gradient tab, they have an entirely different set of gradients and the duotone orange and white

when you create a style variation, the property duotone gradients and/or palette is replaced entirely. You don’t just swap out individual colors

### Differentiate between theme and style variation JSON files

One significant difference with a style variation is we add the `title` at the top under version - note again, theme.json has the duotones here that aren’t available when the user chooses the Ember style variation

### Differentiate between a child theme and a style variation

Now first, the similarity is the desire to override the parent theme’s theme.json file but they do it in a different way. If you had a child theme and it was active, and you had the addition of a theme.json file, the settings would override the parent themes

Within a given theme, the style variations have the same ability to override the theme.json file. However, when a user selects a variation, those changes are considered to be user customizations and they’re stored in the database
