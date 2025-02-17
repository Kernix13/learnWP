# WordPress Action Hooks

> https://learn.wordpress.org/tutorial/wordpress-action-hooks/

- 11 mins

Learning outcomes

1. Understand the difference between action hooks and filter hooks.
2. Register an action hook callback function.
3. Update an action hook callback priority.
4. Work with hook callback accepted arguments.

Comprehension questions

1. What is the difference between an action hook and a filter hook?
2. What function is used to register an action callback function on an existing action hook?
3. Which parameter affects when the action hook callback is run?
4. Which parameter affects the number of variables passed to the hook callback?

Hooks allow your theme or plugin code to interact with or modify the execution of a WordPress request at specific predefined spots. Hooks are what Make WordPress so extendable and allow you to build anything on the foundation of WordPress, from a blog to an online e-commerce platform

actions allow you to perform some action at a specific point

One common activity you will need to accomplish if you develop WordPress themes is deciding which post formats to support and then enabling support for them in your theme

documentation indicates that you need to use the `add_theme_support` function and recommends that this be registered via the `after_setup_theme` action hook

in the WordPress code where this hook is first defined, which is currently on line 576 of the wp-settings.php file. Here, the `do_action` function defines the action hook with the hook name `after_setup_theme`

this hook is fired during each page load after the theme is initialized and is used to perform basic setup, registration, and initialization actions for a theme

In order to make use of an action, you register a function in your code to a pre-existing action hook, which is known as a callback function. To register your callback function on an action, you use the WordPress `add_action` function. You will need to pass the hook name and the name of your callback function as arguments to the `add_action` function

First, we use add_action, and we pass in the action hook name. Then we define our callback function. Next, create the callback function and add support for your chosen post formats

you use actions to perform something either enabling some already existing feature or adding something to the code execution

Now let’s talk about hook priority. If you take a look at the documentation for add_action, you will see two additional function parameters after the hook name and callback function. The third parameter is the hook priority, which is an integer which defaults to 10. This means if you register an action in your code without specifying a priority, it will be registered with a priority of 10

Hook priority allows you to determine the order in which your hook callback is run relative to any other hook callbacks that may be registered on the given hook, either by WordPress Core, or other themes and plugins. Hooks run in numerical order of priority starting at one. It’s usually safe to leave the priority to default of 10, unless you want specifically to change the order in which your callback function is run

If you specify a priority of 11 you can make sure your callback function is run after any core callback functions have been completed

The fourth parameter in the add_action function is the number of accepted arguments the callback function can accept

When defining an action hook using do_action, any number of possible arguments can be added. However, the number passed to the accepted arguments parameter determines how many of them are passed to the hook callback function. If you take a look at the documentation for add_action, you will see that the default value for the number of accepted arguments is one, which means you don’t have to specify a value for this parameter. The first argument will be available passed to the callback function. In the save_post action, there are three possible variables to be accepted. If you register the callback without setting the number of arguments, only the first will be available to the callback function. In this case, the post ID

Being able to determine which arguments you need for your callback function, and then setting the number in the hook registration is a valuable skill
