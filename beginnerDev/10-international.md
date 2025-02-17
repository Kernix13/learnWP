# An introduction to internationalization

## What is Internationalization? -> `__()`

- https://learn.wordpress.org/lesson/what-is-internationalization/
- Internationalization is the process of developing software in a way that it can easily be translated into other languages without any changes to the source code
- any text strings in WordPress need to be coded so that they can be easily translated into other languages
- If you were to access a user’s profile and update it to a different language, the text string would be translated into that language
- Because the translation function is used, once the language has been set for the user, WordPress will search for the translation for this word in the relevant language file, and either display or store the translation, depending on the context
- Internationalization is the process of writing your code so that any text strings that might be displayed to the user are translatable by wrapping them in the correct translation function
- Internationalization is often abbreviated as i18n (because there are 18 letters between the letters i and n).

> The process of translating and adapting the Internationalized text strings to a specific locale or language is called `Localization`

While localization is outside the scope of this lesson, you can read more about it in the [Localization section](https://developer.wordpress.org/apis/internationalization/localization/) of the Common APIs handbook in the WordPress developer resources

### What Internationalization is not

Internationalization is not the same as making sure your content is available in multiple languages on the front end of your website.

This is more commonly referred to as making sure your content is multilingual or translated.

Because this content is stored in the database, it’s better to have a fully translated copy of your site for each language you want to support.

This can be achieved using plugins like TranslatePress, Polylang, or WeGlot.

. . . . . .

## The commonly used internationalization functions

- https://learn.wordpress.org/lesson/the-commonly-used-internationalization-functions/
- Whenever you find yourself writing a string of text that will be displayed to the user, you should use the [WordPress i18n functions](https://developer.wordpress.org/apis/internationalization/internationalization-functions/) to make sure it can be translated

1. `__()` function. This function takes a string of text and returns the translated version of that string. If no translation is available, it returns the original string

You will also notice that this function, and most other i18n functions, takes a second parameter. This parameter is used to specify the text domain. A text domain is a unique identifier for your plugin or theme. It is used to make sure that the correct translations are used. Whenever you use a translation function, you should always include the text domain as the second parameter: `__( 'Some Text', 'my-textdomain' );`

2. `_e()`: WordPress also contains a shorthand function to echo a translatable string - It both internationalizes and then echoes the string. You can use this function to simplify your code

...you need to internationalize the text strings in the JavaScript file. To do this, there is a JavaScript equivalent to the PHP `__()` function, which is available in the wp.i18n object on the WordPress front end. you need to update your `internationalization_enqueue_scripts()` function to require the wp-i18n package as a dependency

```php
/**
 * Enqueue theme.js file in the dashboard.
 */
add_action( 'admin_enqueue_scripts', 'internationalization_enqueue_scripts' );
function internationalization_enqueue_scripts() {
    wp_enqueue_script(
        'internationalization-theme-js',
        get_stylesheet_directory_uri() . '/assets/theme.js',
        array( 'wp-i18n' ),
        '1.0.0',
        true
    );
}
```

Then, you need to call the `wp_set_script_translations` function for the script you want to translate. This function takes the handle of the script and the text domain as parameters. This will load the translations for the script

```php
wp_set_script_translations( 'internationalization-theme-js', 'internationalization' );
```

```js
const __ = wp.i18n.__;
/**
 * Add event listener to the button
 */
document
  .querySelector('#internationalization-settings-button')
  .addEventListener('click', function () {
    alert(wp.i18n.__('Settings button clicked', 'internationalization'));
  });
```

### Internationalization functions in block development

If you are developing a block for the block editor, you can also use the JavaScript translation functions in your block’s JavaScript to internationalize the text strings in your block

All you need to do to use it is to import the relevant functions from the `@wordpress/i18n` package

```js
import { __ } from '@wordpress/i18n';
```
