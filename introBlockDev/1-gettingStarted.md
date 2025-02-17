# Introduction to Block Development: Build your first custom block

## What is a block

> https://learn.wordpress.org/lesson/what-is-a-block/

Gutenberg blocks are built with React. You implement a custom block from within a WordPress plugin

Some types of blocks, such as the paragraph block or the image block, are “primitives” that contain a single item of content. Other types of blocks allow “primitive” blocks to be contained within them. An example of this type of block is the Group block which allows you to group blocks together so that they can be treated as a single unit

It is this type of block that you will be creating in this course, i.e. a block which contains other blocks and styles them as “newspaper columns”.

The content of a post or page is stored in the wp_posts table in the database just as it always has been with the older TinyMCE based editor. However, the block editor inserts HTML comments into the content to delineate individual blocks and to provide meta information that is parsed when the block is rendered in the browser

........................................................

## Set up your development environment

> https://learn.wordpress.org/lesson/set-up-your-development-environment/

- just the basics

........................................................

## Scaffold your first block

> https://learn.wordpress.org/lesson/scaffold-your-first-block/

- A tool exists called “Create Block” which is the officially supported tool for scaffolding a project to implement a custom block

The generated project is essentially a plugin that registers a block. The scaffolding tool generates all the files needed for the project. The files variously contain PHP, JavaScript, CSS, and JSON – basically everything you need to get your project off the ground with minimal effort

```sh
npx @wordpress/create-block multi-columns
```

........................................................

## Understand the structure of the project

> https://learn.wordpress.org/lesson/understand-the-structure-of-the-project/

you now have all the code for a fully working block

First there are three directories

- build
- node_modules
- src

Files

- .editorconfig
- .gitignore
- package-lock.json
- package.json
- readme.txt
- multi-columns.php: the main plugin file that initiates execution of the plugin

```php
<?php
/**
 * Plugin Name:       Multi Columns
 * Description:       Example block written with ESNext standard and JSX support – build step required.
 * Requires at least: 5.8
 * Requires PHP:      7.0
 * Version:           0.1.0
 * Author:            The WordPress Contributors
 * License:           GPL-2.0-or-later
 * License URI:       https://www.gnu.org/licenses/gpl-2.0.html
 * Text Domain:       multi-columns
 *
 * @package           create-block
 */
```

After the standard plugin header this file contains just a few lines of executable code consisting of a single function which is hooked onto the `init` action. This function calls the `register_block_type()` function passing the path to the previously mentioned `build` directory as a parameter. This is the location of block.json which contains the metadata that defines the block which the `register_block_type()` function needs

### src directory

- `block.json` stores the metadata for the block structured as a JSON object. You’ll be working extensively with this file, but take a moment to learn more about it in [this handbook page](https://developer.wordpress.org/block-editor/reference-guides/block-api/block-metadata/). In this file you’ll define attributes that the functions defined in edit.js and save.js can consume as parameters.
- `edit.js` is where you’ll spend most of your time as you work on a project. This file exports a component, `Edit()`, that is rendered in the editor and so determines how the block appears and functions within the editor. It is where you work on the markup of the block, and the associated controls that appear in the Inspector Panel in the editor. The user then has the ability to interact with the block and customize the appearance and content of the block. The function defined here will usually take an `attributes` parameter which is an object containing the attributes defined in `block.json`.
- `editor.scss` is a file containing CSS that styles the appearance of the block in the block editor. Usually you will want the block to appear the same in the editor as it does in the front end of the website, so you’ll probably make no, or very few, changes to this file. You will notice that this example merely adds a border when the block is selected in the editor.
- `index.js` is the starting point for the JavaScript execution of the block. It imports the functions exported by `edit.js` and `save.js` and then executes `registerBlockType` passing as parameters the name of the block and an object containing the two imported functions.
- `save.js` exports a function, `save()`, that determines the markup that will be saved to the `post_content` field in the `wp_posts` table when the post or page is saved, and hence determines how the block appears and functions in the front end. Like with edit.js the function defined here will usually take an `attributes` parameter which is an object containing the attributes defined in block.json.
- `style.scss` is another file containing CSS. In this case the CSS determines the styling of the block in the front end but also in the editor. Styles here can be over-ridden by styles in editor.scss if you need the block to appear different in the editor. However it would be unusual to do this.

edit.js exports a React component whereas save.js exports a function. So Edit() is a React component, and the convention is for React components to be named with a name starting with an upper-case letter. On the other hand save() is a function, the convention for these being to have a name starting with a lower-case letter

........................................................

## Build and run your project

> https://learn.wordpress.org/lesson/build-and-run-your-project/

-

........................................................

##

>

-
