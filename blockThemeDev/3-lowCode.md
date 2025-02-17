# Low-Code Challenge: Turn on important design features

## Low-code: the basics of theme.json for new developers

> https://learn.wordpress.org/lesson/low-code-the-basics-of-theme-json-for-new-developers/

- why do some block themes have more color options than others
- What decides which fonts are even available to choose from–and which fonts appear as the default when a user first activates a theme

The answer to this lies in one of the optional, but key features of block themes: your theme.json file

### How can code in a theme.json file help or hinder you

while the Site Editor by itself is powerful, you’ll want to turn on a few more options in theme.json to help you best design your first block theme

What can your theme.json do:

- Create a suggested color palette or limit the color options that are available
- Turn on (or turn off!) additional tools to give theme designers (and users) even more flexibility in customizing a block theme
- Set available fonts for users and select which font appears upon a brand-new installation
- Adjust the appearance, sizes, weights, and colors of headings (presently unavailable in the Site Editor as of WordPress 6.1)
- Make patterns available to users

Check out [Global Settings & Styles (theme.json)](https://developer.wordpress.org/block-editor/how-to-guides/themes/global-settings-and-styles/)

Using WordPress alone without a theme.json file, the Site Editor allows you to choose many of the defaults that a user will see when they first install and activate your theme on their website - Not all tools are enabled by WordPress’ default, and not all options are able to be created in the Site Editor

.........................................................................

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

.........................................................................

## Check your work: Is your theme working

> https://learn.wordpress.org/lesson/check-your-work-is-your-theme-working/

go through this checklist to make sure you have all the necessary settings turned on for your theme

- Open your Global Styles (half-moon)
- Are your Appearance Tools turned on - look for "Layout"
- Do you see the "dimensions" setting in the Layout section - Content & Wide
- Is your color palette turned on - click on Colors > Palette - Do you see your theme palette names under THEME

.........................................................................

## Low-code: Preparing to set fonts for your block theme

> https://learn.wordpress.org/lesson/low-code-preparing-to-set-fonts-for-your-block-theme/

- Fonts are one of the key elements for a new block theme. They are often the first elements chosen by theme designers
- from a coding standpoint, setting fonts is one of the more challenging things you can do

### Where do your theme’s fonts live

- System Fonts – The fonts that common devices use - These fonts live in the many different browsers and settings on different devices
- Local Fonts – These fonts live within a theme file’s “assets” folder

### How can I manage fonts without coding heavily in theme.json

> Create Block Theme - doesn't do fonts anymore

It turns out that using theme.json to set fonts from the code settings can be really tough! It’s been described by some developers as one of the hardest things you can do within your theme.json file

- need to add one last bit to our theme.json code for the plugin to work correctly in t he ‘Settings’ section

```json
// settings.typography.fontFamilies
// Make sure to include this code so that you can successfully manage your theme’s fonts
{
  "settings": {
    "typography": {
      "fontFamilies": [
        {
          "fontFamily": "-apple-system,BlinkMacSystemFont,Segoe UI,Roboto,Oxygen-Sans,Ubuntu,Cantarell,Helvetica Neue,sans-serif",
          "slug": "system-fonts",
          "name": "System fonts"
        }
      ]
    }
  }
}
```

The resulting CSS custom properties have the following format:

    --wp--preset--font-family--slug: fontFamily value

    body {
      --wp--preset--font-family--system-fonts: -apple-system,BlinkMacSystemFont,Segoe UI,Roboto,Oxygen-Sans,Ubuntu,Cantarell,Helvetica Neue,sans-serif;
    }

.........................................................................

## A website’s look and feel: Design element best practices and brainstorm

> https://learn.wordpress.org/lesson/a-websites-look-and-feel-design-element-best-practices-and-brainstorm/

> One of the hardest things to do is to fill up a blank piece of paper, so this module aims to help you start thinking like a designer

### Where does theme inspiration come from

> skip

- Paintings, photos, or images, Nature, Architecture, album covers, ...
- minimalist, art,
- Who is the audience for your theme? What resonates with this audience?
- What mood or feeling do you want your theme to convey?
- Is there a particular image, idea, concept, or experience that inspires this theme? How does this relate to your audience?
- What five main colors you will want to use on your website? How do these colors connect with the mood/feeling you want to inspire, or your audience?
- What will be your base/primary/background?
- What will be your contrast?
- What will be your primary, secondary, and tertiary colors?
