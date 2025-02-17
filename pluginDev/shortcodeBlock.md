# Converting a Shortcode into a Block

> https://learn.wordpress.org/tutorial/converting-a-shortcode-into-a-block/

1. Set up an existing plugin for block development
2. Create the necessary source files to develop a new block
3. Register the block type in the plugin
4. Create the Edit Component
5. Create the save function
6. Add the newly created block in the editor, and view it on the front end

> Need to watch the video

Comprehension questions

1. What is the command run to create the `package.json` file?
2. What is the name of the file that contains the block metadata?
3. What command is run during development to watch the source files, and run the build step if anything changes?
4. What React hook is used in the Edit component to pass block properties to the component?

...how to convert an existing WordPress shortcode into a block...using the scaffolded code created by the Create Block tool and applying it to an existing PHP-only shortcode plugin

Suppose you have a plugin which adds a new shortcode called wp-subscribe. The shortcode can be added to a post or page in WordPress. When you view the post or page the shortcode renders its HTML output, which includes some text and a clickable link to subscribe page

> No form, just a link to a subscribe page - that sucks!

```sh
npm init
npm install @wordpress/scripts --save-dev
```

you need to make two changes to your package.json file. First, browse to the Block Editor handbook developer.wordpress.org/block-editor and navigate to the Reference guides, Package reference, WordPress scripts: https://developer.wordpress.org/block-editor/reference-guides/packages/packages-scripts/ - `@wordpress/scripts`

Copy the scripts from the setup section and overwrite the existing scripts section in your package.json file to override this test script:

```json
{
  "scripts": {
    "build": "wp-scripts build",
    "check-engines": "wp-scripts check-engines",
    "check-licenses": "wp-scripts check-licenses",
    "format": "wp-scripts format",
    "lint:css": "wp-scripts lint-style",
    "lint:js": "wp-scripts lint-js",
    "lint:md:docs": "wp-scripts lint-md-docs",
    "lint:pkg-json": "wp-scripts lint-pkg-json",
    "packages-update": "wp-scripts packages-update",
    "plugin-zip": "wp-scripts plugin-zip",
    "start": "wp-scripts start",
    "test:e2e": "wp-scripts test-e2e",
    "test:unit": "wp-scripts test-unit-js"
  }
}
```

Next, update the main field in your package.json to point to the index file in the build directory. This directory or file doesn’t exist yet, but it will be created the first time we build the block code. All we need to do is update this to point to build

```json
{
  "main": "index.js" /* Change this line to the following */,
  "main": "build/index.js"
}
```

Before you can start writing any JavaScript code, you first need to register the block type for the Block Editor. This is done in PHP using the `register_block_type` function

- https://developer.wordpress.org/reference/functions/register_block_type/

start by adding an action, binding it on the init action hook. And we’ll go wpl, `wpl_subscribe_block_init` and then we can copy that function name and register the function. It doesn’t need any parameters. And then we say `register_block_type` and we pass in the `DIR` constant, which is the directory of the current file, and we concatenate that with the path to the build directory

```php
// in root main php file
<?php

add_action('init', 'wpl_subscribe_block_init');
function wpl_subscribe_block_init() {
  register_block_type(__DIR__ . '/build');
}
```

As with the main field in the package.json file, the path to the build directory you’re passing to the register_block_type function doesn’t exist yet, but it will be created the first time we build our block

Now you can start building your block source code by creating the `src` directory in your plugin folder, and then creating all the relevant files, the index.js file, edit.js, save.js, etc

You could manually create these files but for your first block it will save you some time if you copy those files from an existing plugin created by the Create block tool and edit them to suit your current shortcode functionality

The first file you need to edit is the block.json file. This file specifies all the properties of your block

just need to change the following fields at a minimum; the Name field – this must follow the namespace/block-name format, where the namespace is the unique name of your plugin also known as the plugin slug. wp-learn-subscribe and then we could just say wp-learn-subscribe-block

The title: the block title that appears in the block list when the user wants to add a block. Update this to wp-learn-subscribe.

The description: a description for your block - then the text domain which is used for translating any strings in your block

While you’re developing your block, you will need to run the `npm run build` command every time you want the code in your source directory to be transpiled into the final block assets in the build directory

During the development process, you can use the WordPress scripts development server, which is built on top of webpack to keep watching the files in your source directory for changes and update the build directory. To do this, switch back to your terminal and run the following command:

```sh
npm start
```

Make sure this is inside the plugin directory. The development server will build all the block assets in the build directory and then watch as the source directory for any changes. If a change is made, it rebuilds all the block assets

The next two files to update are the edit.js and save.js files also known as the Edit component and the save function. It’s a good idea to edit these two at the same time, as they will determine the block functionality in the editor. The Edit component is the code that is run whenever you add or edit a block in the editor and returns the output of the block

With more complex blocks, the Edit component also handles things like block controls, block settings and user inputs

If you scroll to the bottom of the Edit component, you see the component returns the output from the scaffolded block. The output being returned here uses a special format called JSX, which is very similar to HTML. You need to update this so that it matches the code being returned in the original wp-subscribe shortcode

copy the HTML rendered by your shortcode and convert it into the JSX format

Note the use of the curly braces around `useBlockProps`. This is similar to the PHP opening and closing tags and indicates a JavaScript expression that needs to be processed. useBlockProps is a special React hook that will apply any necessary properties to the block wrapper element

The save function determines how the block output is going to be stored in the database - it just needs to return the block output - And then we copy over our updated code for save

The main difference here is using useBlockProps.save in the container div tag, which is required for the save function. If you switch back to your terminal and scroll up, you should see that the build process failed with some errors but then successfully built the assets after editing the save function. If you add this block to a post, you will see how it creates the block and renders the HTML
