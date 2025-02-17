# Block Themes Features

## Custom functionality

> https://learn.wordpress.org/lesson/custom-functionality/

- describe the purpose of a WordPress theme's functions.php file
- decide when to use a plugin instead of the functions.php file when developing a theme
- list some common uses of the functions.php file for extending the functionality of WordPress

### The functions.php file

- add the functions.php file in order to extend WordPress without changing the files by using the WordPress hook system
- you should always run your code on a hook so that it performs its functionality at the appropriate point in the load process
- For example, you could add various theme support features after your theme is initialized by using the after setup theme action hook and the add theme support function
- the `register_block_pattern_category` Fx registers the page's pattern category - you need to do that as well
- WordPress Core already provides us with many pattern categories. It just so happens that this particular pattern category is not provided, so the theme is doing it for us. This will run the Twenty Twenty-Four pattern categories function when the init hook is executed

```php
// see twentytwentyfour functions.php
register_block_pattern_category(
  'twentytwentyfour_page',
  array(
    'label'       => _x( 'Pages', 'Block pattern category', 'twentytwentyfour' ),
    'description' => __( 'A collection of full page layouts.', 'twentytwentyfour' ),
  )
);
```

### Using a plugin

How do you know when to use a plugin instead of the functions.php file?

Since you can add plugin-like features to your theme, it's important to use this power wisely. If you plan to distribute your theme, you'll want to consider placing your code within a plugin rather than relying on the functions.php file

### Common uses

common uses of the functions.php file for extending functionality of WordPress:

- For classic themes, you could use the functions.php file to add block theme styles: `add_theme_support( 'wp-block-styles' );`
- You can also load scripts and styles with the functions.php file
- you can choose to include other PHP files: `require get_template_directory() . '/filepath';

`add_theme_support` I added to customizer theme:

```php
add_theme_support('custom-line-height');
add_theme_support( 'custom-spacing' );
add_theme_support( 'appearance-tools' );
add_theme_support( 'border' );
add_theme_support( 'link-color' );
add_theme_support( 'featured-content' );
add_theme_support( 'responsive-embeds' );
add_theme_support( 'editor-styles' );
add_editor_style( 'style-editor.css' );
// didn't add this one though
add_theme_support( 'post-formats', array( 'aside', 'gallery' ) )
```

Consider these:

- 'disable-custom-colors'
- 'disable-custom-font-sizes'
- 'disable-custom-gradients'
- 'disable-layout-styles'
- 'editor-color-palette'
- 'editor-gradient-presets'
- 'editor-font-sizes'
- 'editor-spacing-sizes'
- 'link-color'
- 'starter-content'

. . . . . . .

## Including assets (in your block theme)

> https://learn.wordpress.org/lesson/including-assets/

- describe how to enqueue styles and scripts
- include CSS in your theme either using stylesheets or inline styles
- include JavaScript in your theme by either using an external file or inline JavaScript
- include images in your theme
- include fonts in your theme

### Enqueue styles and scripts

in order to enqueue or include your CSS or JavaScript files within your themes, you would use the WP `wp_enqueue_scripts` action hook

### Including CSS | Including JavaScript

including CSS in your theme, either using stylesheets or inline styles | including JavaScript in your theme by either using an external file or inline JavaScript:

- `wp_enqueue_style` with get_stylesheet_uri for .css
- `wp_enqueue_script` with get_template_directory_uri for .js
- what about `wp_register_style`

> Using wp_enqueue_style( $handle, $src, $deps, $ver, $media ); and/or wp_enqueue_script( $handle, $src, $deps, $ver, $in_footer ); will load the style/script on every page. This can be very useful if you are developing a theme, but if you are developing a plugin your code will probably not be used everywhere - especially in the WordPress Admin.

> So using wp_register_style and wp_register_script with the same parameters will not only reduce the user's server load, but will also prevent possible plugin conflicts

> `get_template_directory_uri`, that function concatenated with the style.css file will essentially make the CSS styling available in the front end. In case you ever need to add inline CSS, WordPress has the `wp_add_inline_style` - also `wp_add_inline_script`

### Including images

...**going on the assumption here that you're not building a block theme**

- Place your image file within the `assets/img` folder and use the function `get_parent_theme_file_URI`, which will get the URL of your theme

```php
<img src="<?php echo esc_url( get_parent_theme_file_uri( 'assets/img/example.webp' ) ); ?>" alt="" />
```

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
- You can improve the site performance and also make your larger project a little easier to manage
- The Ronny block theme placed their block stylesheets in `assets/styles` but only for core-buttons, core-columns, core-cover, core-post-excerpt, and core-separator
- Charity Vibes block theme placed their block stylesheets in `assets/css` but in a file named blocks.css = they also have admin-styles and rtl
- you do have choices for naming your files and the folder

> Add Contact Form 7 styles in `style.css` and also look at how other big themes did theirs

### Create a custom block stylesheet

...creating custom block stylesheets. There are some naming conventions to take note of

- The class name for a block stylesheet is `.wp-block-{namespace}-{slug}`
- and for core blocks you would use the class `.wp-block-{slug}`
- and the block stylesheet would be `core-{slug}.css`
- To register block stylesheets, you use the `wp_enqueue_block_style` function
- You'll be passing the block name as the first parameter and an array of arguments as the second parameter.
- You can use functions.php to register your block stylesheet

Here is an example of how you would do this for the WordPress core image block and this is the minimum required in order for your style to appear inline within the head area of your page (in `<style>`?):

```php
add_action( 'init', 'themeslug_enqueue_block_styles' );
function themeslug_enqueue_block_styles() {
	wp_enqueue_block_style( 'core/image', array(
		'handle' => 'themeslug-block-image',
		'src'    => get_theme_file_uri( "assets/blocks/core-image.css" ),
		'path'   => get_theme_file_path( "assets/blocks/core-image.css" )
	) );
}
```

. . . . . . .

## Block style variations

>

- describe block style variations and explain how to include them in your theme
- register your new block style using either PHP or JavaScript
- customize core WordPress block styles using the theme.json file

### What is a block style variation and how would you include it in your theme?

Here's an example using the Twenty Twenty-Four theme: ???

> ????????????????????????????????????????

If we select the H2 here, we see that the `With asterisk` style has been applied, including an additional CSS class `.is-style-asterisk`

- select h2 > advanced > additional css classes > `is-style-asterisk`

### Register a block style variation

take a look at how to register a block style using PHP

- functions.php for the Twenty Twenty-Four theme > register_block_style > core/heading - where the block style for the core block heading is being modified here with some styles

> really confusing

```php
register_block_style(
  'core/heading',
  array(
    'name'         => 'asterisk',
    'label'        => __( 'With asterisk', 'twentytwentyfour' ),
    'inline_style' => "
    .is-style-asterisk:before {
      content: '';
      width: 1.5rem;
      height: 3rem;
      background: var(--wp--preset--color--contrast-2, currentColor);
      clip-path: path('M11.93.684v8.039l5.633-5.633 1.216 1.23-5.66 5.66h8.04v1.737H13.2l5.701 5.701-1.23 1.23-5.742-5.742V21h-1.737v-8.094l-5.77 5.77-1.23-1.217 5.743-5.742H.842V9.98h8.162l-5.701-5.7 1.23-1.231 5.66 5.66V.684h1.737Z');
      display: block;
    }

    /* Hide the asterisk if the heading has no content, to avoid using empty headings to display the asterisk only, which is an A11Y issue */
    .is-style-asterisk:empty:before {
      content: none;
    }

    .is-style-asterisk:-moz-only-whitespace:before {
      content: none;
    }

    .is-style-asterisk.has-text-align-center:before {
      margin: 0 auto;
    }

    .is-style-asterisk.has-text-align-right:before {
      margin-left: auto;
    }

    .rtl .is-style-asterisk.has-text-align-left:before {
      margin-right: auto;
    }",
  )
);
```

- take a look at how to customize core WordPress block styles using theme.json
- take a look at the theme.json > core/image > it has a border radius - a `variations` property is added in order to provide the option to round the corners of images
- go into a page and look at an image for the `Rounded` option in the styles tab

```json
"core/image": {
  "variations": {
    "rounded": {
      "border": {
        "radius": "var(--wp--preset--spacing--20)"
      }
    }
  }
},
```

> CONFUSING LESSON

. . . . . . .

## Block variations

> https://learn.wordpress.org/lesson/block-variations/

> https://developer.wordpress.org/block-editor/reference-guides/block-api/block-variations/

- describe block variations
- differentiate between block variations and block styles,
- add the JavaScript file to your theme, and
- register a block variation
- Row and Stack are "Variations" of the Group block - what is different about the 3 are the attributes they have
- All the various specific Embed blocks are variations of the Embed block
- a block varition is a block with preset attributes - look in the code editor at group, stack, row

### What is a block variation?

A block variation is an alternative block you can add to your theme using the [block variations API](https://developer.wordpress.org/block-editor/reference-guides/block-api/block-variations/). You would use the attributes already assigned to the block you are creating a variation from.

You wouldn't require a build process as you can choose to enqueue your custom JavaScript file from functions.php, along with passing through a few dependencies.

You can choose to place your block variation within a plugin or within your theme files.

### Block variations vs Block styles

What is the difference between block variations and block styles?

The main difference between a block variation and a block style is that a block style applies a CSS class to the block so it can be styled in an alternative way.

> STOPPED HERE - NEED TO WTCH AND LISTEN TO THE VIDEO - using the h2 example again with `is-style-asterisk`

- if you click on the block inserter `+` you'll see an example of block variations under Embeds - each one is a block variation - they ship with WP core
- to view the entire code go to https://github.com/WordPress/gutenberg/blob/trunk/packages/block-library/src/embed/variations.js
- If you'd like to learn more about the difference between block variations and block styles, there's a great [online workshop](https://youtu.be/ICI0GW9vibk?feature=shared) that you can refer to

### Adding JavaScript

You can name your JavaScript file block hyphen variations and place it within the JS subfolder under assets (?) - `assets/js/block-variations.js`

### Register block variations

You could use the functions.php file, open up your PHP, use the enqueue block editor assets action hook and use the WP enqueue script function.

You see here that the block variations.js file is being called along with an array of some dependencies

```php
add_action( 'enqueue_block_editor_assets', 'themeslug_enqueue_block_variations' );

function themeslug_enqueue_block_variations() {
	wp_enqueue_script(
		'themeslug-block-variations',
		get_theme_file_uri( 'assets/js/block-variations.js' ),
		array(
			'wp-blocks',
			'wp-dom-ready',
			'wp-i18n'
		),
		wp_get_theme()->get( 'Version' ),
		true
	);
}
```

You can learn more about variations by referring to the [block editor handbook](https://developer.wordpress.org/block-editor/), or you can take a look at the theme handbook. And finally, there's a great [blog post](https://developer.wordpress.org/news/2024/03/14/how-to-register-block-variations-with-php/) available on WordPress.org on their WordPress developer blog

> CONFUSING LESSON
