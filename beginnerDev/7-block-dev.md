# An introduction to developing WordPress blocks

## Setting up your block development environment

- blocks are the default way in which a WordPress site stores and represents content
- Blocks are used in the Post and Page Editors when creating and editing content,
- as well as the Site Editor when creating and editing theme templates or patterns
- blocks are made up of a combination of an HTML comment with a specific format that defines the block, and if required, HTML entities to represent the block content

```html
<!-- wp:paragraph {"backgroundColor":"accent-5"} -->
<p class="has-accent-5-background-color has-background">
  This is some content in a paragraph block.
</p>
<!-- /wp:paragraph -->
```

- These `wp:paragraph` comments are how WordPress knows this is a paragraph block
- The actual content of the block is everything inside the `wp:paragraph` tags

### Getting set up

1. local WordPress installation and a code editor
2. You need a terminal, to run commands.
3. And you need an installation of Node.js and npm

- we recommend using a terminal application for Windows called PowerShell
- `Node.js` and `npm`: Block development relies on the use of a JavaScript framework called `React`

> Installing NVM on Windows

Because nvm allows you to run multiple versions of Node.js, you need to tell nvm which version you want to use. You can do this by running the nvm use command, followed by the version number.

```sh
nvm use 20
# or
nvm use --lts
```

- https://github.com/nvm-sh/nvm
- https://radixweb.com/blog/installing-npm-and-nodejs-on-windows-and-mac#windows

The WordPress Developer documentation has an entire section dedicated to the [Block Editor](https://developer.wordpress.org/block-editor/), which contains a wealth of information on blocks, block development, as well as the various packages available to block developers.

It’s also a good idea to read the [Fundamentals of Block Development](https://developer.wordpress.org/block-editor/getting-started/fundamentals/) section to get a better understanding of the process

## Scaffolding a new block

> tool called `create-block`, which will allow you to quickly scaffold your first block plugin https://learn.wordpress.org/lesson/scaffolding-a-new-block/

In software development, scaffolding is the process of creating a basic structure for a project, so that you can build on top of it.

- developing a block for WordPress requires a combination of specific files and folders to be set up in a certain way
- you would ideally want to build your block following certain best practices
- Create-block is a command line tool that helps you scaffold a new block plugin, following these best practices
- Using create-block, you can run a single terminal command to create a new block plugin, and create-block will set up the necessary files and folders for you
- if you are developing a theme for your own use, or for a client, you can include custom blocks in your theme, the difference is that you register the blocks in a different way
- Ultimately though the block development experience and tooling is designed to work best with plugins

> Copyright Date Block

- It displays the text "Copyright", followed by the copyright symbol (©), then a starting year, and the current year
- The user should also be able to adjust the starting year
- open the terminal on your local computer, and switch to the /wp-content/plugins directory
- run the create-block command, and include a plugin slug

```sh
npx @wordpress/create-block@latest copyright-date-block
```

- This will create a new plugin in the copyright-date-block directory, install any required packages, and create the necessary files - with 3 folders:
  - The `build` directory is where the final deployable build of the block code is located. This is the code that powers the block when it’s used in the editor
  - `node_modules`
  - The `src` directory is where you will spend most of your time writing block code
- Following those three directories are a number of files:
  - `.editorconfig`,
  - `.gitignore`
  - `readme.txt` file which you’ll only need to edit if you intend to publish your plugin
  - `copyright-date-block.php`: `copyright_date_block_block_init` function calls the `register_block_type()` function passing the path to the previously mentioned build directory as a parameter
  - `package-lock.json` and ` package.json`
- in package,json is The scripts object contains a list of command line scripts that can be run during development
  - `build` which compiles the files from the src directory into the build directory
  - `start` which starts a development server that watches for changes to the files in the src directory and automatically compiles them into the build directory

### The `src` directory

All of your block development takes place in the src directory

- `block.json` stores the metadata for the block, defined as a JSON object. This file allows you to define things like the block name, title, icon, the various files that make up the block, and much more
- `edit.js` is where you’ll spend most of your time as you work on a block. This file exports a React Edit() component, that is rendered in the editor and determines how the block appears and functions in the editor
- `editor.scss` contains the styles that control the appearance of the block in the block editor - Usually, you will want the block to appear the same in the editor as it does in the front end of the website, so you’ll often not need this file at all
- `index.js` is the starting point for the JavaScript execution of the block. It sets up and executes the `registerBlockType` function to register the block in the editor
- `save.js` exports a `save()` function, which determines the markup that will be saved to the `post_content` field in the `wp_posts` table when the post or page is saved, and therefore determines how the block appears and functions in the front end
- `style.scss` contains the styles that control the appearance of the block in the editor and the front end. Styles here can be overridden by styles in editor.scss if you need the block to appear different in the editor
- `view.js` is a file that is used to add any additional JavaScript to the block in the front end. This is another file that you will often not need

### The `build` directory

During development, you will execute the scripts you saw in the `package.json` file to compile the files from the `src` directory into the `build` directory.

The process of building your block code, also known as bundling your code, is the process of converting your block code into a format that is compatible with all browsers.

When you scaffolded the block, the `create-block` tool also ran the build process, generating the `build` directory for you.

You will notice that some files are bundled into the `build` directory as is, like the `block.json` file, while others are converted, like the `index.js` file. There are also additional files, like the `index.asset.php` file, that are generated during the build process.

When WordPress loads your block in the editor or on the front end, it’s executing the code from the `build` directory.

The `@wordpress/scripts` package defined as a dev dependency in the `package.json` file uses a tool called Webpack to bundle your block code

## Building your first block

- https://learn.wordpress.org/lesson/building-your-first-block/
- clean up any scaffolded code you don’t need
  Navigate to the `copyright-date-block/src` directory and remove the `view.js` file
- remove the `viewScript` property from the `block.json`
- open `copyright-date-block.php`: change the `@package` annotation from `CreateBlock` to `copyright-date`
- Remember, `register_block_type` uses the metadata from `block.json`
- modify the scaffolded block metadata for your block - change at least the values of the following properties
  - 1. update the `name`. In this case you can replace `create-block` with the same value you used for the package value in the plugin header, `copyright-date` (Huh?)
  - 2. update the `icon`. For now, change the icon value to `calendar`. This icon comes from the [Gutenberg Icon Library](https://wordpress.github.io/gutenberg/?path=/story/icons-icon--library).
  - 3. update the `description`, to make it more specific to your block

**src/index.js**

- importing the `registerBlockType`, `style.scss`, the `Edit` component, the `save` function, and imports the JSON object from the `block.json`
- it uses the `registerBlockType` function to register the block, and passes in two variables, the block name, and a block configuration object of block properties
- the edit property is set to the value of the Edit component, and the save property is set to the value of the save function.
- Because the save property and the imported save function have the same name, it uses a shorthand syntax to set the property value

Build:

- `npm run build`
- This will scan through the contents of your `src` directory, and compile the files from that directory into the build directory
- Whenever you make changes to your block code, you’ll need to run this command again to update the `build` directory
- Optionally, there is a `npm run start` command that will start a development server that watches for changes to the files in the `src` directory and automatically builds them into the `build` directory

```sh
npm run build
npm run start
```

> You can read more about the block metadata fields in the [Metadata in block.json](https://developer.wordpress.org/block-editor/reference-guides/block-api/block-metadata/) section of the Block Editor Handbook

## Block functionality

> REMEMBER: Edit component (edit.js) is for the post editor and save() (save.js) is for the front end

- https://learn.wordpress.org/lesson/block-functionality/
- adding the block’s functionality in the editor, via the `Edit` component and adding how the block stores its output, via the `save` function
- It’s often a good idea to start by building out the block’s `Edit` component, so it functions correctly in the editor
- the code block `export default function Edit()` (the Edit component) is the code that displays the block in the editor
- the code returned by the `Edit` component is wrapped in a single container element - any React component must only return a single parent container
- the use of the `useBlockProps` function: Because `useBlockProps` returns an object with properties and values, the use of the spread syntax applies the properties and their values as attributes to the parent container
- code is using the WordPress `__()` function. This is a special function that allows text to be translated for different languages, also known as Internationalization
- For the copyright symbol, you can use the `&copy;` HTML entity, which will be converted to the right symbol when it’s rendered

Adding the block’s save functionality:

- Right now, when you preview the block, it’s still showing the scaffolded text
- The `save` function in the `save.js` file is what is run every time the block is saved in the Editor.
- This is the content that is stored in the `post_content` field in the database, and rendered on the front end
- This is very similar to what was scaffolded in the Edit component, with a couple of differences
- One difference is that only a specific subset of the block’s properties are applied to the parent container, via `useBlockProps.save()`
- This is because the save function is only concerned with the properties that are relevant to the front end, and not the editor
- The other difference is that the code inside the parent tag is all on one line
- This is mostly irrelevant to the block’s actual functionality, and it just shows a different way to write the same code. Some developers prefer to split out the code onto multiple lines, as it makes it more readable in some circumstances.
- So you can update the save function to return the same content as the Edit component

## Block attributes

> GREAT VIDEO - WATCH AGAIN

- https://learn.wordpress.org/lesson/block-attributes-2/
- One of the benefits of building blocks is the ability to allow users to control the block’s appearance and behavior via block attributes
- how to add attributes to a block, and how to add controls to your block to allow users to change those attributes
- Attributes are the properties of a block that can be set by the user, e.g. the starting year would be an attribute that the user can change
- To add attributes to a block, you define them in the block’s metadata in the block.json file

```json
"attributes": {
  "startingYear": {
    "type": "string",
    "default": "2000"
  }
},
```

> sometimes the server will crash when editing the block metadata (block.json) - just restart the server: `npm run start` or `build`

- One of the benefits of the JSON format is that you can add a new property anywhere in the existing JSON object, as long as you use a property name that’s expected.
- In this case, the attributes property is expected by the block registration process, so you can add it anywhere in the JSON object
- To access the block’s attributes in the block’s Edit component, you can specify a `props` argument in the Edit component function
- Both the `Edit` component and the `save` function are set up to always accept this props object containing all the properties of the block.
- Instead of writing out `props.attributes.startingYear` every time you want to access the starting year attribute, you can use something call the destructuring assignment syntax to extract the attributes from the props object, and then again to extract the `startingYear` from the attributes

Block recovery:

If you happen to be testing your block in a post or page and refreshing your browser each time you make changes to the block attributes default value or the save function, you might sometimes run into this error:

> _This block contains unexpected or invalid content_.

- This is because when a block’s `save` function is run, it compares the output from the save function with the output already saved in the database. If they are different, it shows this error.
- If you open the Console tab of your browser’s developer tools, you’ll see this reported as a Block validation error.
- You can fix this by using the `Attempt Block Recovery` button, which re-renders the block, and re-saves its output.

### Adding a Settings panel to the block:

- To allow users to change the block’s attributes, you need to make use of [Block Controls](https://developer.wordpress.org/block-editor/getting-started/fundamentals/block-in-the-editor/#block-controls-block-toolbar-and-settings-sidebar).
- There are two ways to add controls,
  - either in the block toolbar, that appears above the block when it’s selected, or
  - in the settings sidebar (also known as the inspector), which appears in the sidebar when the block is selected
- Because the `startingYear` attribute is a text string, you can use a `TextControl` to the block sidebar to allow users to change the starting year
- To add controls to the block sidebar for your block, you’re first going to need to import a few things.
  - You’ll need the `InspectorControls` component from the `@wordpress/block-editor` package.
  - You’ll need the `PanelBody` and `TextControl` components from the `@wordpress/components` package.
- Open the edit.js file in the src directory, and look for the line that imports useBlockProps
- The InspectorControls component can also be imported from the @wordpress/block-editor package
- The PanelBody, and TextControl components can be imported in the same way from the @wordpress/components package

```jsx
import { InspectorControls, useBlockProps } from '@wordpress/block-editor';
import { PanelBody, TextControl } from '@wordpress/components';
```

- You can now use these components to add controls to the block sidebar
- Start by adding the `InspectorControls` component to the output of the `Edit` component. This component is a wrapper for the controls that appear in the block sidebar
- Then add a PanelBody component, and give it a title attribute
- either use a `div` or a React Fragment to wrap everything in a single parent container
- Because the functionality of the block only really requires the paragraph tag, using the Fragment is the best option
- If your block requires more markup, like a header tag above the paragraph, then using the div option might make more sense
- Once the build process has finished, if you add the block to a post or page, and enable the Editor’s Settings sidebar, you’ll see the Settings panel you added to the block sidebar.
- To follow WordPress plugin development practices, one small update you might want to make is to use the \_\_() function to translate the title of the PanelBody component

```jsx
<>
  <InspectorControls>
    {/* <PanelBody title="Settings">Testing</PanelBody> */}
    <PanelBody title={ __( 'Settings', 'copyright-date-block' ) }>
  </InspectorControls>
  <p {...useBlockProps()}>
    {__('Copyright', 'copyright-date-block')}© {startingYear} - {currentYear}
  </p>
</>
```

### Adding a TextControl to the block sidebar:

- With the Settings panel in place, you can now add a TextControl component to allow the user to edit your attribute.
- The TextControl component is a text input field that allows the user to enter a string. There are three properties you need to set on the TextControl component. The first two are the label and value:
  - label: the label that appears above the input field
  - value: the value of the input field
- The other property you need to set is the `onChange` property. This property is a function that is called when the value of the input field changes, which receives the new value entered by the user

```jsx
<PanelBody title={__('Settings', 'copyright-date-block')}>
  <TextControl
    label={__('Starting Year', 'copyright-date-block')}
    value={startingYear}
    onChange={newStartingYear => {
      // update startingYear with newValue
    }}
  />
</PanelBody>
```

In order to update the attribute, you can use one of the other properties on the props object that is passed to the Edit component, the setAttributes function. This function is used to update any block’s attributes with a new value.

You can add setAttributes to the list of properties being destructed from the props object, and then use it to update the startingYear attribute.

```jsx
export default function Edit({ attributes, setAttributes }) {}
```

make sure to check out the [Attributes guide](https://developer.wordpress.org/block-editor/reference-guides/block-api/block-attributes/) in the Block Editor Handbook

> REFRESHER ON DESTRUCTURING `{ }` AND SPREAD SYNTAX `...`

## Block supports and styles

- One of the benefits of blocks is the ability to control the block’s appearance on a per block level
- you can use something called block supports, as well as define the block’s styles
- Block [Supports](https://developer.wordpress.org/block-editor/reference-guides/block-api/block-supports/) is the API that allows a block to declare support for certain common features
- You can define support for these common features in the block metadata, and once enabled, the block will have those abilities enabled in the Editor
- Enabling any of the available block supports is as simple as adding them to the supports property in the `block.json` file, and it gives your users a wealth of options to customize the block’s appearance

```json
"supports": {
    "html": false,
    "align": true
},
```

> align center is there but it does not work????

Block styles:

- There are some cases however where you would prefer to define the block’s styles yourself
- style.scss and editor.scss: These files allow you to set up specific block styles, and then those styles are applied in the editor and on the front end
- If you need a specific style to be applied to the block in the front end and in the editor, you would add the styles to the style.scss file

```css
.wp-block-create-block-copyright-date-block {
  background-color: #21759b;
  color: #fff;
  padding: 2px;
}
```

- this style is not being applied to the current block. This is because the class name applied to the parent container of the block via `useBlockProps` is automatically generated based on the block’s name
- In the block.json file the name of the block is `copyright-date/copyright-date-block`, so the class name is generated as wp-block-copyright-date-copyright-date-block
- The class name you see being targeted in the style.scss file is based on the original name of the block, so you need to change it to match the class name that is being generated
- Because you want the border to appear all the time, you don’t need to define any specific editor styles. This means you can delete the editor.scss file
- You can also delete the `editorStyle` property in the block.json file
- And the importing of the editor.scss file in the edit.js file
- You’ll see that the block now has the border and border color that you defined in the style.scss file

> When you’re developing your blocks, it’s useful to think about what appearance elements you want users to be able to edit, vs what should always apply to the block. Then you can either add the relevant support or hard code any specific styles into the relevant style file

## Static vs dynamic blocks

When developing WordPress blocks, you’ll need to consider the functionality of your block, and whether it needs to change based on external factors

- it is possible to create blocks that are either static or dynamic, depending on your requirements

### Static blocks

- Copyright Date Block is a static block
- As the static block’s content is fixed, once it’s added to the editor, the save function is triggered, and the post or page is saved, the block’s content will not change
- Static blocks are useful for content that doesn’t need to change, like a quote, or a testimonial

### Dynamic blocks

- if the physical year changes, the rendered content of the block should also update
- Otherwise, you’ll need to edit anywhere that you’ve added the block, to trigger the save function and update the year
- Dynamic blocks do not render their content via the save function, and instead use PHP to render their content when a front-end request is made for a post or page that includes the block

### Making the Copyright Date Block dynamic

- To make the Copyright Date Block dynamic, you need to specify a PHP file or function that contains the block’s rendering logic
- This can be done in a few ways, but the easiest is to use the render property in the block’s metadata in the block.json file

```json
"render": "file:./render.php"
```

- This tells WordPress to use a file with the filename render.php file to render the block’s content on the front end.
- You can then create a render.php file in the src directory, and add your rendering logic to that file:

```php
<?php
    $block_props = get_block_wrapper_attributes();
    $starting_year = $attributes['startingYear'];
    $current_year = date( 'Y' );
?>
<p <?php echo $block_props?>>
    Copyright © <?php echo $starting_year?> - <?php echo $current_year; ?>
</p>
```

- You can use the `get_block_wrapper_attributes` function to get the block’s wrapper attributes. This is similar to calling `useBlockProps` in JavaScript
- Then you can get the startingYear value from the PHP $attributes array. This $attributes variable is one of three that are exposed to the file you set for your block’s render metadata property, and contains any attributes that have been set up for your block
- Then you can create the `$current_year` variable, which uses the PHP `date()` function to always get the current year. This way, when the block is rendered, it always gets the current year
- Once you’ve set up your render.php file, you can remove any code related to the block’s save process in the editor, as you don’t need to save any content to the post - you can delete the save.js file
- You can also delete the save property passed to registerBlockType, as well as the import that imports the save function
- You’ll see that the block still renders as expected in the editor. However, if you view the block in the code editor, you’ll see it the saved version does not include any output
- However, if you simulate the year change, say by changing the value of the variable in PHP, the front end rendering of the block will update accordingly

> read the [Static or Dynamic rendering of a block](https://developer.wordpress.org/block-editor/getting-started/fundamentals/static-dynamic-rendering/) section of the Fundamentals of Block Development
