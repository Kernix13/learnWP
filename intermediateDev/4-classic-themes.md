# Classic Themes

## Introduction to Classic themes

> https://learn.wordpress.org/lesson/introduction-to-classic-themes/

- differentiate between classic and block themes,
- list and describe the typical files included in a classic theme, and
- organize your theme files

### Classic vs Block Themes

- in December 2018 when WordPress 5.0 released Gutenberg
- August 2023, and that's when WordPress 6.3 really took off and interested users started seeing the power of full site editing
  - we can manage and create new templates.
  - We can create patterns and also manage template parts

If we were comparing a traditional classic theme with a block theme, the main differences would lie within three main categories, and those are file structure, the end user customization via settings, and styling

One of the significant differences between a classic and a block theme is how end users are able to make site-wide changes to their website. The UI has changed dramatically

Hybrid: So a classic theme doesn't have to be a block theme in order to take advantage of some of the flexibility provided by the use of a theme.json file

A classic theme therefore has the ability to provide configuration and styling options to the Block Editor and block content, and that's done via `theme supports`, and you would include those within your `functions.php` file, or you could consider adding `theme.json`

### Organizing theme files

```
|-- assets /
|   |-- css
|   |-- images
|   |__ js
|-- inc
|-- template parts /
|   |-- footer
|   |-- header
|   |-- navigation
|   |-- page
|   |__ post
|-- 404.php
<!-- the rest of classic theme templates -->
```

There's actually a considerable amount of flexibility in terms of how you structure your files with a classic theme - we've got the templates written in PHP, and then we have CSS and JavaScript files

learn more about [classic themes](https://developer.wordpress.org/themes/), you can refer to the developer's theme handbook

. . . . . . .

## The Loop

> https://learn.wordpress.org/lesson/the-loop/

- describe how the Loop is used within a theme,
- list some examples of what the Loop can display, and
- explore displaying data from Custom Post Types and Custom Fields

### How is the loop used within a theme?

```php
<?php
if ( have_posts() ) :
  while ( have_posts() ) : the_post();
    // Display post content
  endwhile;
endif;
?>
```

- The loop extracts the data for each post from the WordPress database and inserts the appropriate information in place of each template tag
- Any HTML or PHP code in the loop will be processed for each post
- loops through each post retrieved for the current page one at a time and performs the actions specified in your theme

### What can the Loop display?

- metadata, the post title, the featured image, and the excerpt
- Other examples of using the loop include listing comments on a single post and also pulling data from custom post types and custom fields

### Custom Post Types and Custom Fields

- custom post type **portfolio** - use the loop in order to display the portfolio posts and include a custom field
- Each post has a post title, a project brief, and a featured image
- taxonomy for skills and tools, and at the bottom, we see the project brief custom field
- note `get_post_meta()`
- A plugin was created in order to create the custom field, and it's actually specifically known as a meta box. This meta box is the project brief - `new_cmb2_box()` and `add_field()`

```php
<?php
if ( have_posts() ) :
	while ( have_posts() ) : the_post();?>
		<div class="cm-post-list mb-5">
			<a href="<?php the_permalink(); ?>"><h2><?php the_title(); ?></h2></a>
			<?php
			if ( ! has_excerpt() ) {
				echo '';
			} else {
				the_excerpt();
			}?>
			<?php $project_info = get_post_meta( get_the_ID(), 'catmom_textarea', true );
			if ( $project_info ): ?>
			<p class="project-meta"><?php echo $project_info; ?></p>
			<?php endif;?>

			<?php the_post_thumbnail();?>
		</div><?php
	endwhile;
else :
	// When no posts are found, output this text.
	_e( 'Sorry, no posts matched your criteria.' );
endif;
wp_reset_postdata(); ?>
```

> Try this: metadata above title > t hen title > then featured image > them excerpt

. . . . . . .

## Theme options

> https://learn.wordpress.org/lesson/theme-options/

- describe the Customize API otherwise known as the Customizer,
- list examples of how the Customizer is used in a theme, and
- register theme options using the Customizer.

### What is the Customizer?

> [Theme Options – The Customize API](https://developer.wordpress.org/themes/customize-api/)

> [WP_Customize_Manager class](https://developer.wordpress.org/reference/classes/wp_customize_manager/)

- install a classic theme
- we don't see the Editor choice anymore because we don't have access to the Site Editor with a classic theme

### Using the Customizer

- open up the functions.php file > `add_theme_support()` > Editor Color Palette. And this is how users can just select from the palette

### Register theme options

- It all starts with the [WP_Customize_Manager class](https://developer.wordpress.org/reference/classes/wp_customize_manager/) that will help you with creating those controls in the Customizer
- Note the comment here under More Information on how the `$wp_customize ` object is used as an instance of this class, and it's the primary use of this class that you'll see within Themes

```php
function themeslug_customize_register( $wp_customize ) {
  // Do stuff with $wp_customize, the WP_Customize_Manager object.
}
add_action( 'customize_register', 'themeslug_customize_register' );
```

- the Twenty Twenty-One theme that calls the WP_Customize_Manager in order to create that object, `$wp_customize`

it's strongly recommended that developers study the core customizer code. This is all of the core files that contain the word "customize," and you'll find this in your WordPress install folder, `wp-includes/customize`

. . . . . . .

## theme.json in Classic themes

> https://learn.wordpress.org/lesson/theme-json-in-classic-themes/

- list the benefits of having theme.json added to a classic theme, and
- describe the process of adding theme.json to a classic theme.

### What are the benefits of having theme.json added to a classic theme?

- activate the Twenty Twenty-One theme > look at Sample page and select a block > there's text and typography settings and styles available.
- With theme.json, we can gain control over those settings and styles
- For example, you could choose to disable color support for the heading

```json
{
  "version": 3,
  "settings": {
    "blocks": {
      "core/heading": {
        "color": {
          "text": false,
          "background": false,
          "link": false
        }
      }
    }
  }
}
```

### Adding theme.json

- add theme.json to the Twenty Twenty-One theme: all you need is the schema and the version and of course add theme.json to the root

```json
{
  "$schema": "https://schemas.wp.org/trunk/theme.json",
  "version": 3
}
```

- To learn more about adding theme.json to a theme, do check out the _Global settings and styles_ lesson available within the Beginner WordPress developer learning pathway
- something about layout shifts and to add settings for contentSize:

```json
"settings": {
  "layout": {
      "contentSize": "650px"
  }
}
```

If you want to see all of the settings within theme.json of WordPress core, you can find it within the 'wp-includes/theme.json' folder

. . . . . . .

## Converting a Classic theme to a Block theme

> https://learn.wordpress.org/lesson/converting-a-classic-theme-to-a-block-theme/

- describe the various requirements of converting a classic theme,
- differentiate between a hybrid theme and a block theme, and
- list the steps to take in order to convert a classic theme into a block theme.

### Converting a classic theme

- If you opt to not add `theme.json` you'll need to take a look at the various options for adding theme support using the functions.php file
- within the WordPress dashboard, end users will know that they're either working with a classic theme or a hybrid theme when they're in appearance and they don't have access to the Site Editor

### Hybrid vs Block theme

...the difference between a hybrid theme and a block theme

- Twenty Twenty theme: typography, changing the color for the text and the background, the end user can choose blocks, patterns, and media
- Under Patterns, they have access to patterns that are shipped with the theme
- Also within Widgets, end users can use blocks in order to build out their widgets

A hybrid theme is still a classic theme, however, the theme author has chosen to add theme support for things like block template parts

```php
add_theme_upport('block-template-parts');
```

### Steps to converting a classic theme

- Your first step is to take a look at settings and styles
- You can bridge the gap between a classic theme and a block theme by simply adding `theme.json` to your theme
- Or you can choose to add_theme_upport for blocks within functions.php
- You can choose to remove patterns from wordpress.org patterns directory and just include the patterns that you want the end user to have for your theme

> The goal here is to start reducing the amount of CSS in your style sheets and use theme.json instead

Check out [15 ways to curate the WordPress editing experience](https://developer.wordpress.org/news/2024/07/04/15-ways-to-curate-the-wordpress-editing-experience/) - it starts off by providing you with how to do so using theme.json. But there are many ways you can do so by using JavaScript or PHP

- Your next step is to start building out your pages by using the Block Editor
- You don't have access to the site editor yet, so you can't develop your HTML templates using the Site Editor, but you can build out pages using the editor
- Your final step is to add the Site Editor to your theme and start building out all of your templates using the Site Editor, which essentially means that you'll no longer have PHP templates and you'll replace those with HTML ones
- You do not need to convert your classic theme to a block theme. You can just stop at the hybrid theme stage
- If you're interested in converting your classic theme to a hybrid theme, you may want to start off by [adding support within functions.php for block template parts](https://learn.wordpress.org/tutorial/using-block-template-parts-in-classic-themes/)
