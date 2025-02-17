# theme.json

> SEARCH FOR Variations

> 1_Combos/designBlocks.md

. . . . .

```json
{
  "version": 3,
  "settings": {
    // Global settings go here
  },
  "styles": {
    // Global styles go here
  }
}
```

. . . . .

- see "Block Theme Builders – Figma to Block Theme" & "diving into theme.json" in leftToDo.md

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
// this is under settings.typography.fontFamilies
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

> see `settings.typography.fontSizes` for the `fluid.max` and `fluid.min` properties

- then `styles.elements.h1.typography.fontSize`: `"var:preset|font-size|x-large"` - repeat for all headings
- besides .h1 also do link, link:hover, caption, button,

. . . . . .

## 7. diving into theme.json

> `DONE` https://wordpress.tv/2022/09/02/lets-code-diving-into-theme-json/

......................................

- see "Global settings and styles" in beginnerDev/5-theme-dev.md

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

1. WordPress core:

Within the installation files, if you go to the WP includes folder, you’ll see theme.json there and this file defines the default settings and styles: `wp-includes/theme.json`

2. Theme-name/theme.json file

Anything you define in that file will override the WordPress defaults. If you have a child theme that is active and you have a theme.json file included in your child theme, then anything that you do here will take precedence over the `theme.json` file in the parent theme. For instance you could set `Appearance Tools` to false.

3. User configurations

Within the Site Editor any changes that are added to the database through changes made to global styles or even templates and saved. This will override and takes priority over all other levels in the hierarchy.

> [theme.json reference guide](https://developer.wordpress.org/block-editor/reference-guides/theme-json-reference/)

............................................

- see "Creating your block theme's theme.json file" in blockThemeDev/2-getTechnical.md

## Creating your block theme's theme.json file

> https://learn.wordpress.org/lesson/creating-your-block-themes-theme-json-file/

So far, you have created: style.css, index.php, templates folder, index.html

We are now going to create an optional, but highly recommended file in order to help us unlock additional options in our theme.json file

### Creating a theme.json

- create theme.json and paste in the following:

```json
{
  "$schema": "https://schemas.wp.org/wp/6.0/theme.json",
  "version": 2
}
```

This code allows your text editor to use a technology known as “schema”. It is especially helpful to help you write code effectively

- If you open doublequotes it will indicate to you what keys should be in the file but are not

```json
{
  "$schema": "https://schemas.wp.org/trunk/theme.json",
  "version": 3,
  "settings": {},
  "styles": {},
  "templateParts": {},
  "customTemplates": {} /* missing below here */,
  "blockTypes": {},
  "description": {},
  "patterns": {},
  "slug": "",
  "title": ""
}
```

"settings" has:

```json
"settings": {
  "appearanceTools": true,
  "color": {},
  "layout": {},
  "spacing": {},
  "typography": {},
  "useRootPaddingAwareAlignments": true, /* missing below here */
  "background": {},
  "blocks": {},
  "border": {},
  "custom": {},
  "dimensions": {},
  "lightbox": {},
  "border": {},
  "position": {},
  "shadow": {},
}
```

"styles" has:

```json
"styles": {
  "color": {},
  "spacing": {},
  "typography": {},
  "blocks": {},
  "elements": {}, /* missing below here */
  "background": {},
  "border": {},
  "css": {},
  "dimensions": {},
  "filter": {},
  "outline": {},
  "shadow": {},
  "variations": {},
}
```

And I sure you could continue to drill down

............................................

- see "~~Low-code: the basics of theme.json for new developers~~" and "Your first codes in theme.json" in blockThemeDev/3-lowCode.md

## Your first codes in theme.json

> https://learn.wordpress.org/lesson/your-first-codes-in-theme-json/

In order to have the most options available to you so that you will have far more control over your custom block theme’s site editor, you’ll want to turn on a few settings in your theme.json file. We need to turn on three settings to give us the most control possible

1. _Appearance Tools_, which give you more control over your site’s overall layout.
2. _Layout_, which will allow you to set a default width so that your design doesn’t spread across an entire screen
3. A _Color Palette_, which allow you to set and re-use custom colors throughout every theme block

### Appearance Tools

Many appearance tools are automatically turned off by WordPress’ defaults. These tools will allow you to add padding around your theme and around entire blocks, which will give you a lot more control over how your theme looks

This allows you far greater control of how you can use white space, and turns on some additional tools for you to utilize as a theme designer

Use this setting to enable the following Global Styles settings:

- border: color, radius, style, width
- color: link
- spacing: blockGap, margin, padding
- typography: lineHeight
- dimensions: aspectRatio, minHeight
- position: sticky

## Layout

Many websites are built using container blocks, otherwise known as Group, Row, Stack, and Column blocks. In order to position things effectively, people use these tools to help them better control the position and blank space around individual blocks by adding invisible padding and spacing, block by block

```json
// in settings
"layout": {
  "contentSize": "645px",
  "wideSize": "1280px"
},
```

- that constrains how wide your content can get
- `contentSize` = the default setting. This will automatically make sure that content within your container blocks (columns, rows, groups, stacks) stays within a range you input.
- `wideSize` = a setting that will now appear in the editor; this can be useful for headers that you’d like to fill the entire screen vs. appear as a smaller block.

You will have times where a layout width will be used to limit the maximum widths of blocks. Set your preferred values with this code

### Create a Color Palette in the Site Editor

By default, WordPress does not include the ability to select a color palette

This can be a time-saving tool because it allows you to repeatedly select pre-set colors as you design your theme block by block

It’s also possible to select the actual color ahead of time in this section, which many developers do! However, once this feature has been turned on, you can do this right in the site editor

### naming our color palette

- “Primary”, “Contrast”, and “Base”
- why not give them color names
- WordPress, however, will not let you name colors their actual names (like indigo or blue).
- It’s a best practice to name them as they are meant to be used–such as a base color, a contrast, a primary color, etc

many theme developers are moving away from using terms like “Background” and “Foreground” because users of your theme may use them differently - instead use names like “Base” and “Contrast"

```json
{
  "$schema": "https://schemas.wp.org/trunk/theme.json",
  "version": 2,
  "settings": {
    "appearanceTools": true,
    "layout": {
      "contentSize": "920px",
      "wideSize": "1280px"
    },
    "color": {
      "palette": [
        {
          "color": "#F1F8FF",
          "slug": "background-color",
          "name": "Background Color"
        },
        {
          "color": "#222222",
          "slug": "text-color",
          "name": "Text Color"
        },
        {
          "color": "#FFEE58",
          "slug": "primary",
          "name": "Primary"
        },
        {
          "color": "#F6CFF4",
          "slug": "secondary",
          "name": "Secondary"
        },
        {
          "color": "#503AA8",
          "slug": "tertiary",
          "name": "Tertiary"
        },
        {
          "color": "#686868",
          "name": "Accent 4",
          "slug": "accent-4"
        },
        {
          "color": "#FBFAF3",
          "name": "Accent 5",
          "slug": "accent-5"
        }
      ]
    }
  }
}
```

............................................

- see "Using theme.json to control available settings" & "How presets are written within theme.json" & "Registering custom templates in theme.json" & other occurrences in intermediateDev/1-global.md

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

............................................

- see 6 occurrences in intermediateDev/3-block-themes.md

### Including fonts

how to include fonts in your theme using theme.json

- font files added to assets/fonts
- within theme.json under `settings.typography.fontFamilies`, under `fontFace` the file has been referenced in order to generate a variable that can be used within styles

```json
"settings": {
  "typography": {
    "fontFamilies": [
      {
        "fontFace": [
        {
          "fontFamily": "Inter",
          "fontStretch": "normal",
          "fontStyle": "normal",
          "fontWeight": "300 900",
          "src": [
            "file:./assets/fonts/inter/Inter-VariableFont_slnt,wght.woff2"
          ]
        }
      ],
      "fontFamily": "\"Inter\", sans-serif",
      "name": "Inter",
      "slug": "body"
      }
    ]
  }
}
```

- This is what the variable would look like and you would just have to replace the slug with the one you set under settings

```css
/* replace {$slug} */
var( --wp--preset--font-family--{$slug} )
/* an example of using the source serif pro font for the post title */
var( --wp--preset--font-family--source-serif-pro )
```

. . . . . . .

## Block stylesheets

> https://learn.wordpress.org/lesson/block-stylesheets/

> Confusing lesson

- describe a block stylesheet
- create a custom block stylesheet

### What is a block style sheet and when would you use it?

- You always have the choice to write your CSS within theme.json
- **However, block stylesheets are the solution if ever your CSS starts to get too lengthy**
- You always have the choice of placing your CSS within `style.css`
- However for a large project, you may want to consider _breaking out your stylesheets per_ block and then placing it into a folder such as assets.
- **You can improve the site performance and also make your larger project a little easier to manage**
- The Ronny block theme placed their block stylesheets in `assets/styles` but only for `core-buttons`, `core-columns`, `core-cover`, `core-post-excerpt`, and `core-separator`
- Charity Vibes block theme placed their block stylesheets in `assets/css` but in a file named blocks.css - they also have admin-styles and rtl
- you do have choices for naming your files and the folder

> How do you access those files?

> Add Contact Form 7 styles in `style.css` and also look at how other big themes did theirs

............................................

- see "1. Introduction to theme.json" in TeachWP.md

## 📌 1. Introduction to theme.json

> https://learn.wordpress.org/tutorial/introduction-to-theme-json/

> EXCELLENT

- to control the settings and styles to the blocks in the editor
- **if you wipe everything out of theme.json except schema, and type `""` you will see an auto-suggest - select "version" and it will auto-populate the latestversion number**
- WP core ships with a default theme.json
- the "settings" key is where the developer can extend the default theme.json or enable/disable specific theme settings & functionality, as well as configure new CSS variables
- these settings can then be applied to the theme globally or to specific block elements
- settings > appearanceTools - it is disabled by default - this setting controls all of the following features on blocks that support them:
  - border color, radius, style, and width
  - setting link color
  - block gap, margin, and padding
  - text line-height
- the ability to enable or disable theme specific settings in theme.json replaces the requirement for `add_theme_support` in functions.php
- e.g., custom colors for elements in the site editor - just click the color setting and change - to disable that in a classic theme is `add_theme_support('disable-custom-colors')` - to disable the custom color picker in theme.json:

```json
"settings": {
  "color": {
    "custom": false,
    "palette": [
      {
        "name": "Alt",
        "color": "#135e96",
        "slug": "alt"
      }
    ]
  },
  "blocks": {
    "core/paragraph": {
      "color": {
        "custom": true
      }
    }
  }
}
```

- however you could enable the custom color picker for a specific block(s) still under the "settings" key
- it is possible to set preset css variables for a theme
- to add a new color to the color palette - add a new color object under settings.color.palette which is an array and would appear under THEME
- doing that creates a new CSS variable for the color - the format for the variable is `--wp--preset--color--{slug}` or `--wp--preset--color--alt`
- to style all text across the entire theme/site - use the "styles" key

```json
"styles": {
  "color": {
    "text": "var(--wp--preset--color--alt)"
  }
}
```

- to apply the color to a specific block, remove the global text color and apply it to the specific block in the blocks scheme - huh?
- you could do the same for the "elements" key for buttons

```json
"styles": {
  "elements": {
    "button": {
      "color": {
        "background": "var(--wp--preset--color--alt)"
      }
    }
  }
  "blocks": {
    "core/post-content": {
      "color": {
        "text": "var(--wp--preset--color--alt)"
      }
    }
  }
}
```

............................................

- see 13 occurrences in gutenberg-clocks/WP-Docs/course-pt-1.2.md

## 2. Converting the Style Guide to the theme.json file

The first step a developer usually takes is turning the style guide from the given designs into CSS

### Populating theme.json – Settings and Styles

Creating a Global Setting

- apply the system-wide theme font
- first create a system-wide Typography setting in the settings of your theme.json, which will generate a CSS variable when the theme is rendered
- The `name` value is the name of the font as it will appear in the Site editor
- The `slug` value is used to create the CSS variable, using the following format
  - `--wp--preset--font-family--{slug}`
- This creates a CSS preset variable called `--wp--preset--font-family--system-font` that can be used in the theme’s Global Styles
- To apply this font setting to your theme, you can select this preset in the Global Styles interface in the Editor

### Applying a Setting in the Global Styles Interface

Switch back to the Site editor, open the Global Styles interface, and apply the new font in the Typography section.

1. Open the Global Styles interface.
2. Click Typography.
3. Click Text.
4. Select System Font from the Font dropdown.

> Make sure to save your Custom Styles, to ensure they are applied to the theme

### Applying a Setting in the theme.json File

If you prefer to manually add the setting to the theme.json file, you can do so by adding the following to the styles section.

- Update the `styles` section in the theme.json and apply the `–wp–preset–font-family–system-font` CSS variable to all typography.

> THAT IS THE THING THE FIRST GUY DID - FROM ONE SECTION TO ANOTHER

> HOVER OVER `settings` > `typography` > `fontFamilies` in theme.json and you will see: `--wp--preset--font-family--{slug}`

RECAP to add styles to theme.json:

- settings > typography > fontFamilies
  - hover over fontFamilies to get the class name used later
  - in fontFamilies add {fontFamily, name, slug}
- styles > typography > fontFamily
  - set fontFamily to `"var(--wp--preset--font-family--your-slug-value)"`
- Now switch back to your Site Editor, and take a look at any of the templates. You should see that the font has been updated to the system font

### Exporting Styles Applied in the Global Styles Interface

- use the `Overwrite` option of the Create Block Theme plugin, which will update your `theme.json` file with any changes applied in the Global Styles interface

### Block Course Theme Settings and Styles

The process outline above is the same for any setting or style you want to apply to your theme.

1. Add the relevant setting to the `settings` section in theme.json
2. Apply the setting via the Global Styles interface OR
3. add it to the relevant style in the `styles` section of theme.json

Styles can be applied globally, as we did for the typography, or to specific blocks.

> To speed up this process, it’s also possible to copy existing settings and styles from existing themes and update the values to match your theme.

- copy their starter `"settings"` and `"styles"`

............................................

- see 10 occurrences in gutenberg-clocks/WP-Docs/course-pt-1.3.md

NOTE:

- Only the changes are stored, not an updated version of the original theme.json with the changes included.
- The style values are stored in a slightly different format from what you’ve seen in the theme.json file so far (e.g. `var:preset|color|pale-pink` instead of `var(--wp--preset--color--pale-pink))`. Both formats are acceptable.
- The `isGlobalStylesUserThemeJSON` field is included in the stored data, and set to `true`. This allows WordPress to know which styles are from the theme.json file, and which are from the stored Global Styles data.

> WTF?

### How WordPress Decides Which Global Styles to use

When a post or page is rendered, WordPress will first load all the settings and styles from the theme.json file, and then merge any settings or styles stored in the `wp_global_styles` custom post type record

What is also important to understand is that if you make changes to a setting or style in theme.json, and there’s also a value for that setting or style in the custom post type record, then the value from the custom post type record will be used, and not the value from theme.json

### Resetting Global Styles

If you manually make changes to the theme.json file, you can reset the theme styles in the Global Styles interface. To do this, click on the three dots in the Global Styles interface, to open the options menu, and select Reset to defaults

`IMPORTANT`: This will delete the custom post type record, and the theme styles will be loaded from the theme.json file

............................................

- see 8 occurrences in gutenberg-clocks/WP-Docs/course-pt-1.4.md

### Registering Custom Templates

your final step is to register the custom template in the theme.json file. To do so, you add a new top-level item called `customTemplates` to the file, and then add an object for each custom template

THEN...

> Delete the user-created template by clicking on the three dots next to the template, and selecting the Delete option.

1. Export the template to the relevant template file
2. Register the template in theme.json
3. Delete the template added by the user

> Remember to add the new custom template to the `customTemplates` array in the theme.json file, using a comma between each custom template object. Remember to also set the correct post type for the alternative post template

............................................

- see 11 occurrences in gutenberg-clocks/WP-Docs/course-pt-2.2.md

> 160 LINES - READ THEM ALL - ABOUT FONTS

> Excellent file

............................................

- see 8 occurrences in gutenberg-clocks/WP-Docs/course-pt-2.4.md

> Skip for now - Style Variations!!!

............................................

- see 5 occurrences in gutenberg-clocks/WP-Docs/course-pt-2.6.md

> ENTIRE FILE!

- locking designs: `"templateLock":"contentOnly"`

............................................

- see 34 occurrences in gutenberg-Blocks/WP-Docs/BestOf.md

- LINE 71-150: ### theme.json
- LINE 334-360 : ### Styles
- LINE 528-543 : ### Applying Font Families via theme.json
- LINE 545-560 : ### Setting the Global Font Family

............................................

- see ## theme.json in gutenberg-Blocks/WP-Docs/blockDev.md

............................................

> see gutenberg-blocks/WP-Docs/theme.json.md

............................................

- Global Settings & Styles (theme.json): https://developer.wordpress.org/block-editor/how-to-guides/themes/global-settings-and-styles/
- Global Styles & theme.json: https://fullsiteediting.com/lessons/global-styles/
- Exercise: Creating theme.json: https://fullsiteediting.com/lessons/creating-theme-json/

## Notes

- the file used to define the global and block-based styles for the theme
- the primary file that's responsible for specifying and organizing all the theme's design aspects
- changes you make in the site editor are stored in the database, not theme.json

## Theme File Structure

- ✅ `assets`/
  - ✅ `css`/
    - ✅ editor-style.css
  - ✅ `fonts`/ - need a monospace font, have poppins, inter, playfair display
  - `images`/
    - header-background.png
  - ✅ `js`/
    - navigation.js
- `inc`/ (I don't think this is used)
  - ClassName.php
  - functions-helpers.php
- `parts`/
  - ✅ footer.html
  - ✅ header.html - NEEDS EDITS
  - ✅ post-mets.html - NEEDS EDITS
  - ✅ sidebar.html - NEEDS EDITS
- ✅ `patterns`/
  - ✅ footer.php - dozens of php files - NEEDS EDITS
- ✅ `styles`/
  - example.json - don't think I will be using this at all
- ✅ `templates`/
  - 404.html
  - archive.html
  - ✅ index.html (`required`) - NEEDS EDITS
  - page-no-title.html
  - page-with-sidebar.html
  - page.html
  - search.html
  - single-with-sidebar.html
  - single.html
  - singular.html - don't think I want this one
- .editorconfig - SKIP
- .gitattributes - SKIP
- .gitignore
- CHANGELOG.md - SKIP
- LICENSE.md - SKIP
- ✅ `functions.php`
- ✅ `README.txt` - made it .md for now
- package.json - SKIP
- ✅ `screenshot.png` - 1200x900
- ✅ `style.css` (`required`)
- ✅ `theme.json`

Child theme style.css

```css
/**
 * Theme Name: Grand Sunrise
 * Template:   fabled-sunset
 * ...other header fields
 */
```

## Templates

- need to copy patterns .php files

> fucking check all of these and the php file for `wp:pattern`

- ✅ 404.html - edit spacing, wp:pattern,
- ✅ archive.html - edit spacing, wp:pattern,
- ✅ home.html - edit wp:pattern,
- ✅ index.html - edit wp:pattern
- ✅ page-no-title
- ✅ page-wide.html
- ✅ page-with-sidebar.html - edit spacing
- ✅ page.html - edit spacing
- ✅ search.html - edit spacing, wp:pattern,
- ✅ single-with-sidebar.html - edit spacing, wp:pattern,
- ✅ single.html

## To-Do

```json
// these are true by default - why turn them off
{
  "color": {
    "defaultDuotone": false,
    "defaultGradients": false,
    "defaultPalette": false
  }
}
```

> TYPOGRAPHY, TYPOGRAPHY, TYPOGRAPHY!!!

## SETTINGS

```json
"custom": {
  "line-height": {
    "body": 1.4,
    "heading": 1.1
  }
},
```

- why no settings.background or settings.blocks?
- ✅ finish settings.color.palette
- ✅ look into settings.custom - ignore for now
- ✅ look into settings.lightbox - a specific setting that you can enable for supported blocks. It enables a lightbox feature that expands an image when a site visitor clicks on an image
- ✅ double check settings.dimensions - why?
- double check settings.shadow - copied them off WP page
- double check settings.spacing > `"defaultSpacingSizes": false` - DOUBLE-CHECK IN THEME
- edit/check settings.spacing.spacingSizes
- patterns
- settings.background, settings.blocks, ✅ settings.color.palette, ✅ settings.color.duotone, ✅ settings.color.gradient
- settings.spacing.spacingSizes > look into clamp

## STYLES

- Styles: https://developer.wordpress.org/themes/global-settings-and-styles/styles/
- Applying Styles: https://developer.wordpress.org/themes/global-settings-and-styles/styles/applying-styles/
- Using Presets: https://developer.wordpress.org/themes/global-settings-and-styles/styles/using-presets/
- Styles Reference: https://developer.wordpress.org/themes/global-settings-and-styles/styles/styles-reference/

```json
"typography": {
  "fontFamily": "var:preset|font-family|inter",
  "fontSize": "var:preset|font-size|medium",
  "fontWeight": "400",
  "lineHeight": "1.4"
}
```

```css
:root {
  -wp--preset--font-size--medium: clamp(
    14px,
    0.875rem + ((1vw - 3.2px) * 0.882),
    20px
  );
}
```

> https://raw.githubusercontent.com/WordPress/gutenberg/wp/6.6/schemas/json/theme.json

- look into styles.filter
- look into styles.outline
- look into styles.border - no, don't set this

```json
"styles": {
  "border": {},
  "filter": {},
  "outline": {},
}
```

- is my settings.spacing correct?
- styles.css, styles.dimensions, styles.shadow, styles.background
- styles.typography.fontFamily
- styles.spacingScale? generates a single custom property per preset valu

### styles.elements

> reread "What is a block style sheet and when would you use it"

- I need to maybe add color (links?) like 2025 and I need to add cite and button
- button, button:focus, button:hover, `caption`, `h1`, `h2`, `h3`, `h4`, `h5`, `h6`, `heading`, `link`, `link:hover`,

```json
"button": {
  "color": {
    "background": "var:preset|color|contrast",
    "text": "var:preset|color|base"
  },
  ":focus": {
    "outline": {
      "color": "var:preset|color|accent-4",
      "offset": "2px"
    }
  },
  ":hover": {
    "color": {
      "background": "color-mix(in srgb, var(--wp--preset--color--contrast) 85%, transparent)",
      "text": "var:preset|color|base"
    },
    "border": {
      "color": "transparent"
    }
  },
  "spacing": {
    "padding": {
      "bottom": "1rem",
      "left": "2.25rem",
      "right": "2.25rem",
      "top": "1rem"
    }
  },
  "typography": {
    "fontSize": "var:preset|font-size|medium"
  }
},
```

styles.blocks

- core/avatar, core/button, core/columns, core/buttons, core/code, core/post-author, core/post-author-name, core/post-date, core/post-excerpt, core/post-featured-image, core/post-navigation-link, core/post-terms, core/post-title, core/quote, core/pullquote, core/query-pagination, core/query-title, core/search, core/separator, core/site-tagline, core/site-title, core/term-description, core/navigation, core/list (2), core/calendar, core/categories, core/footnotes, core/gallery, core/image,

## templateParts ✅

## customTemplates

- Within this field themes can list the custom templates present in the templates folder. For example, for a custom template named my-custom-template.html, the theme.json can declare what post types can use it and what’s the title to show the user
- I have custom templates listed but they are cnot created in the templates folder:
  - check page-no-title.html
  - check page-with-sidebar.html
  - check page-wide.html
  - check single-with-sidebar.html

## Fonts

When downloading fonts online, you may not always get the newer formats. There are various converter scripts and apps available online that can convert .ttf to .woff2 and/or .woff format, such as Google Webfonts Helper: https://google-webfonts-helper.herokuapp.com/fonts
