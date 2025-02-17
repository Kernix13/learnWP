# Using the create-block Tool

> https://learn.wordpress.org/tutorial/using-the-create-block-tool/

a command line tool called Create Block, and how you can use this tool to scaffold a new block plugin

Create-block is an official command-line tool developed by WordPress contributors to scaffold or create a new block plugin.

It generates everything you need to start a new block plugin and integrates a modern build setup with no configuration

## Requirements

- a local WordPress install,
- a terminal to run commands,
- Node.js and npm

It’s important to make sure you use the right version of Node.js. Fortunately, you can do this using the open-source node version manager, also known as [nvm](https://github.com/nvm-sh/nvm/blob/master/README.md)

The great thing about using nvm, is if your version requirements change, it’s very easy to update your Node.js version using nvm

## Installation

> ???

## Using Create Block

```sh
npx @wordpress/create-block wp-learn-todo
```

This will create a new plugin, install any required packages and create the necessary files. Once the new plugin is scaffolded, you should have a new plugin folder in your WordPress install, named after the slug you passed to create-block (`wp-learn-todo`)

The most important directories and files:

- `build` – this is the location where the final block asset files will be built for distribution
- `src` – the source directory, where you will do most of your coding. All your block code lives here.
- `package.json` – the file that determines what packages your code needs
- `Readme.txt` – the file that is used by the WordPress.org plugin repository
- `wp-learn-todo.php` – the main plugin file that tells WordPress this is a plugin

Activate this plugin via the WordPress dashboard and if you open the block editor, you can add the WP Learn Todo block

> See beginnerDev/7-block-dev.md for another example
