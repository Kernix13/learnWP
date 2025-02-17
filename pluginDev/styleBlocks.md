# Styling your WordPress Blocks

> https://learn.wordpress.org/tutorial/styling-your-wordpress-block/

- 9 minutes
- Prerequisite: Converting a Shortcode into a Block
- className in JSX, enqueue CSS
- How to add styles to your custom WP blocks

> Need to watch the video

Learning outcomes

1. Understanding how Blocks enqueue CSS
2. Use the className property in JSX to apply class attributes
3. Add custom styling to a block
4. Add additional style to a block in the Block Editor

Comprehension questions

1. What is the name of the block.json field that represents the style sheet applied in the Block Editor?
2. Why should you use className and not a class in JSX elements?
3. What is the name of the scss file that handles the block styling?

learn how to add styles to a custom WordPress block

In the original adding block support to an existing plugin tutorial, you started with a PHP shortcode plugin (See `pluginDev/shortcodeBlock.md`)

the shortcode would usually also have some styling applied by way of the CSS file loaded from the plugin directory

At the top of the plugin, a function called `wpl_subscribe_shortcode_scripts` is registered on the `wp_enqueue_scripts` action hook. And the `wp_register_style` function is used to register the CSS stylesheet located in the plugin’s `assets/css` directory

Then at the top of the shortcode callback function, this style sheet is enqueued for rendering whenever the shortcode is used by calling the `wp_enqueue_style` function

If you look at the block.json file attributes, you will see the `editorStyle` and style attributes defined

The values for these attributes are both files that will be created in the build directory during the build step. In this case, index.css and style-index.css.

The style file is enqueued both when the block is rendered in the editor and whenever the block is rendered on the front end. The editorStyle file is enqueued when the block is rendered only in the Block Editor and can be used to add style specific to the editor experience. The style.scss file in the source directory is used create the style file. The editor.scss file in the source directory is used to create the editorStyle file

The reason for having the additional editorStyle stylesheet for your block is if you want to display different elements when the block is being added or edited in the Block Editor

For example, you might have a block that includes a select box, which allows the user to select a post which powers the block in the editor. The select box will only be displayed in the editor, but you might want to style it in some specific way. This is where the editorStyle stylesheet comes in handy

The container div’ss class attribute is generated from the name property in the block.json file and is used here because we used useBlockProps in the save function. You can make use of this class in the style.scss file so it targets the correct elements

we need to add a className value in the save function and the Edit component where it renders the JSX. If we switch back to the browser, it’s the subscribe-header class. In our save function, update this to be className. subscribe header. And then edit. Do the same thing

it’s possible to add additional styles to the block when it’s rendered in the editor by adding these styles to the editor.scss file
