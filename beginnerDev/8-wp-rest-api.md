# An Introduction to the WordPress REST API

> THIS ENTIRE SECTION IS INCREDIBLY IMPORTANT

## The WordPress REST API

When you’re developing for WordPress, there are a number of APIs that you can use to interact with your site data. One of the most important of these is the [REST API](https://developer.wordpress.org/rest-api/)

- The WordPress REST API provides an interface for applications to interact with a WordPress site
- One of the most well-known implementations of the WordPress REST API is the Block Editor, which is a JavaScript application that interacts with WordPress data through the REST API
- If you open your browser’s developer tools and look at the Network tab, you can see the requests that are made to the WordPress REST API when you interact with the Block Editor.

### What does REST API mean?

- REST stands for REpresentational State Transfer, which is a software architectural style that describes a uniform interface between physically separate components
- the WordPress REST API provides REST endpoints (URIs) which represent the posts, pages, taxonomies, and any other custom data types
- Your code can send and receive data as JSON to these endpoints to fetch, modify, and create content on your site

### Routes & Endpoints

- a route is a URI which can be mapped to different HTTP methods, the type of request that’s made whenever you interact with anything on the web
- The mapping of an individual HTTP method to a route is known as an endpoint
- a GET endpoint for fetching data, a POST endpoint for creating data, and a DELETE endpoint for deleting data, all using the same route

### Local Development Testing

- One thing to note about testing REST API routes on a local WordPress installation is that you may need to enable a Permalink setting other than “Plain”.
- This is because the REST API uses the same URL rewriting functionality as Permalinks to map the human-readable routes and endpoints to the relevant internal request
- So if your local WordPress installation is using the default Plain permalink setting, change it to something like Post name

### Example Routes & Endpoints

- open a browser, and go to the `/wp-json/` URI of a WordPress site, you will be making a GET request to that URI
- The data returned is a JSON response showing what routes are available, and what endpoints are available within each route
- `/wp-json/` is a route, and when that route receives a GET request it’s handled by the endpoint which displays the data. This data is what is known as the index for the WordPress REST API
- By contrast, the `/wp-json/wp/v2/posts` route offers a GET endpoint which returns a list of posts, but also a POST endpoint. If you are an authenticated user, and you submit the right data via a POST request to the `/wp-json/wp/v2/posts` route, that request is handled by the endpoint which creates new posts
- Typically, the same route will have different endpoints for different HTTP methods

### Global Parameters

- The WP REST API includes a number of global parameters which control how the API handles the request/response handling.
- These operate at a layer above the actual resources themselves and are available on all resources
- Global parameters are implemented on REST API routes as query string parameters: `?` followed by a series of `key=value` pairs, separated by `&`
- `/wp-json/wp/v2/posts`: update the route by adding the `_fields` global parameter, and then specify the fields you want to return in the response as a comma-delimited list: `/wp-json/wp/v2/posts?_fields=author,id,excerpt,title,link`

### Pagination and Ordering

- Pagination is handled by the `per_page`, `page` and `offset` parameters
- It’s also possible to order the results, using the `order` and `order_by` parameters:

`/wp-json/wp/v2/posts?_fields=author,id,excerpt,title,link&per_page=5&orderby=title&order=asc`

. . . . . . .

## Using the WordPress REST API

> 17:00

- https://learn.wordpress.org/lesson/using-the-wordpress-rest-api/
- three internal options for making REST API requests
- The Bookstore plugin - download main plugin code from the GitHub repository by clicking on the Bookstore plugin link
- Once you have the plugin installed and activated, open the main plugin file in your code editor
- You will notice that one of the arguments passed to the `register_post_type` function is `show_in_rest` which means that the custom post type is available in the REST API
- This means that if you browse to the `/wp-json/wp/v2/book` route, you will see the custom post type data in the response
- For example, you can change the rest_base argument to change the route that the custom post type data is available at
- Given that you would expect to be able to fetch more than one book from the book route, it would be a good idea to change the rest_base to books: `'rest_base'    => 'books',`
- Doing this will allow you to make requests to the `wp-json/wp/v2/books` route, to access books via the REST API

### Making REST API requests

- Let’s say you want to add a page in your WordPress dashboard that fetches the books and displays a list of book titles and permalinks a comma-separated list
- you might add an admin submenu page to the Books menu, using the `admin_menu` hook, and the `add_submenu_page` function
- If you browse to the dashboard and click on the Books menu, you will see a new submenu page called Book List
- Clicking on that link will take you to a page with the “Load Books” button, and a textarea

> Can I get the main keyword for my posts? Would I have to query Yoast?

- Now you could add functionality to the bookstore_render_booklist function which fetches the book list via PHP and make the button trigger a page refresh
- However, for a smoother user experience, you’d like to use JavaScript and the REST API to fetch the book data asynchronously and populate the book list, without having to wait for a full page refresh

### Enqueuing the admin JavaScript

- Because this functionality is being added to the admin dashboard, you need to set up a separate `wp_enqueue_script` function call hooked into the `admin_enqueue_scripts` hook, so that the JavaScript file is only loaded in the admin dashboard
- create a new JavaScript file in the plugin directory, called `admin_bookstore.js`
- You could test that it’s enqueued correctly by adding a single alert to the admin_bookstore.js file, and refreshing the admin page

### Option 1: Using the Backbone.js client

- WordPress included a [Backbone.js](https://backbonejs.org/) [REST API JavaScript Client](https://developer.wordpress.org/rest-api/using-the-rest-api/backbone-javascript-client/)
- This provides an interface for using the WP REST API by providing Models and Collections for all endpoints exposed through the API
- To ensure that your JavaScript code is able to use the REST API client, you need to add it as a dependency to your enqueued JavaScript
- The third argument for `wp_enqueue_script` is an array of any dependencies, and you can add `wp-api` as a dependency to your wp_enqueue_script function call
- This will ensure that your plugin’s JavaScript code is only loaded after the REST API JavaScript client is loaded, so you can use it in your plugin
- start by registering a click event handler for the new button
- in the event handler function, you can use the WP API client, by accessing it from the global wp object, to create a new collection of books
- bookstore.js is empty, see below for all the code

```js
const loadBooksByRestButton = document.getElementById('bookstore-load-books');
if (loadBooksByRestButton) {
  loadBooksByRestButton.addEventListener('click', function () {
    const allBooks = new wp.api.collections.Books();
    allBooks.fetch().done(function (books) {
      const textarea = document.getElementById('bookstore-booklist');
      books.forEach(function (book) {
        textarea.value += book.title.rendered + ',' + book.link + ',\n';
      });
    });
  });
}
```

### Option 2: Using @wordpress/fetch-api

- Since the inclusion of the Block Editor in WordPress 5.0, the @wordpress/fetch-api package has also been made available to make REST API requests
- This package is a wrapper around the browser fetch API, and provides a more modern and flexible way to make requests to the REST API.
- To make use of the fetch API you can update your plugin’s JavaScript dependencies to include wp-api-fetch

```php
wp_enqueue_script(
    'bookstyle-script',
    plugins_url() . '/bookstore/admin_bookstore.js',
    array( 'wp-api', 'wp-api-fetch' ),
    '1.0.0',
    true
);
```

```js
const fetchBooksByRestButton = document.getElementById('bookstore-fetch-books');
if (fetchBooksByRestButton) {
  fetchBooksByRestButton.addEventListener('click', function () {
    wp.apiFetch({ path: '/wp/v2/books' }).then(books => {
      const textarea = document.getElementById('bookstore-booklist');
      books.map(book => {
        textarea.value += book.title.rendered + ',' + book.link + ',\n';
      });
    });
  });
}
```

- Notice how you pass the `path` to the books endpoint in an object to the `wp.apiFetch` function. This is more flexible than using the Backbone.js client, which requires you to use a specific collection to access the books
- You can chain a `then` method to handle the response. This is similar to the use of the `done` method in the Backbone example

### Option 3: Using @wordpress/core-data

- If you’re developing blocks, there is also a `core-data` [package](https://developer.wordpress.org/block-editor/reference-guides/packages/packages-core-data/) available, to access data from the REST API
- core-data is meant to simplify access to and manipulation of core WordPress entities
- It registers its own store and provides a number of selectors which resolve data from the WordPress REST API automatically, along with dispatching action creators to manipulate data
- core-data makes use of a number of React functionalities, and so is best used in a block context:

```sh
cd path/to/local/site/wp-content/plugins
npx @wordpress/create-block bookstore-block
```

- This will scaffold the new block, with some code for you to edit
- Inside the block’s `edit.js` file, import the `useSelect` hook from the `@wordpress/data` package, as well as the store from the `@wordpress/core-data package`

```php
import { useSelect } from '@wordpress/data';
import { store as bookStore } from '@wordpress/core-data';
```

- Then you can use these to fetch the books from the REST API

```php
const books = useSelect(
  select =>
      select( bookStore ).getEntityRecords( 'postType', 'book' ),
  []
);
```

- `useSelect` is a hook that allows you to retrieve data from registered selectors
- `useSelect` accepts a callback function as its first argument, where you make use of the `bookStore` store’s `getEntityRecords` selector to retrieve the books from the REST API
- you can update the code to either return an empty component if no books are returned or loop through the books object and output the book title and link

```php
if ( ! books ) {
    return (
        <div { ...useBlockProps() }></div>
    )
}

return (
    <div { ...useBlockProps() }>
        { books.map( ( book ) => (
            <p>
                <a href={ book.link }>{book.title.rendered}</a>
            </p>
        ) ) }
    </div>
);
```

- Now, run the block build step, activate the plugin, and add the bookstore block to a post or page

Differences between options:

- The Backbone client is the oldest of the three options, but it is also the most tightly integrated with the REST API. If you need to build admin dashboard pages using the wP REST API, it’s a good choice
- apiFetch is a great all-round solution, because you can use it for admin dashboard pages, as well as blocks in the editor. It’s also a more modern way to make requests to the REST API, and is more flexible than the Backbone client
- core-data is best used in a block context, as it uses React functionality that’s not available outside the context of the block editor

. . . . . . .

## Interacting with the WordPress REST API

- https://learn.wordpress.org/lesson/interacting-with-the-wordpress-rest-api/
- While the WP REST API is commonly used to fetch data from WordPress, it can also be used to perform other actions
- The REST API also allows you to create, update, and delete various WordPress data types
- the WP REST API schema, methods to authenticate a WP REST API request, tools to test WP REST API requests, a couple of ways to add, edit or delete data via the WP REST API

### WP REST API Schema

> `/wp-json/wp/v2/posts` and `/wp-json/wp/v2/books`

- When working with the REST API, it’s useful to keep the [Endpoint Reference section](https://developer.wordpress.org/rest-api/reference/) of the WP REST API documentation handy
- The Endpoint Reference lists all endpoints that ship with WordPress core
- Clicking on an individual endpoint will show you the schema for that endpoint. The schema defines all the fields that exist for a resource when fetching or creating data of that specific type
- If you’ve created a custom post type, like the `books` custom post type from the bookstore plugin, the schema for the custom post type endpoint will be similar to the posts endpoint
- many of the endpoint fields match up with the fields that are available in the WordPress database table related to that data type. Some, however, are slightly different
- the title field for the Post endpoint will match up to the post_title field in the posts table. It is important to remember that these differences exist **and to use the correct field name** when interacting with the API

### Authentication

- By default, the WordPress REST API uses the same [cookie-based Authentication](https://developer.wordpress.org/rest-api/using-the-rest-api/authentication/) method that is used when logging into the WordPress dashboard
- For any REST API endpoints that are not public, or require an authentication user to view or modify, the authentication cookie needs to be present
- There are a number of ways to authenticate requests, including [JSON Web Tokens](https://wordpress.org/plugins/jwt-authentication-for-wp-rest-api/) and [OAuth](https://wordpress.org/plugins/rest-api-oauth1/).
- Another way that’s built into WordPress is [Application passwords](https://make.wordpress.org/core/2020/11/05/application-passwords-integration-guide/)
- Application passwords can be set on a per-user basis, and are used to authenticate requests to the WP REST API.
- This allows you to let users access the API without having to share the password they use to log in to the WordPress dashboard
- To create an application password for your user, navigate to your user in the Users list, and click on the User to edit it. Scroll down to the bottom of the screen, under the Application Passwords section
- Give the new application password a name and click Add New Application Password.
- The password will be generated for you. Make sure to copy it and store it somewhere securely, as you won’t be able to see it again

```
WP REST API password:
icir tlVc suoF X63I GNWz kRC6
```

- In this screen you are also able to revoke the password, should it ever be leaked
- Using an application password for your user is a great way to test out REST API requests, using a REST API testing tool
- If you intend to build something more complex, like a mobile app that connects to a WordPress REST API, you should rather consider using JSON Web Tokens or OAuth 1.0a

### Postman

- open Postman, and click on the Create Collection button
- give the collection a name to differentiate it from other collections. Inside the collection click the `Add a Request` button
- This will open a new request, where you can give the request a unique name. Then, enter the URL to your local books endpoint, and click the Send button: `http://twenty24.luna/wp-json/wp/v2/books`
- The request will be made, and the JSON response will be parsed and displayed in the response area
- create a new request, and enter the same URL to the books endpoint, but this time change the request method to `POST`, and hit Send.
- By changing the request method to `POST`, you’re telling the server that you want to either create or possibly update a book
- you’ll be presented with an error message because you’re not authenticated

```json
{
  "code": "rest_cannot_create",
  "message": "Sorry, you are not allowed to create posts as this user.",
  "data": {
    "status": 401
  }
}
```

- To authenticate the request, click on the `Auth` tab, and select `Basic Auth` from the dropdown
- Then, enter your `username` and the `Application Password` you created earlier, then click the `Save` button and click `Send`
- you don’t get the same error, because you’re not authenticated
- create a book by clicking on the `Body` tab in the request, and selecting the `raw` radio button. Then, select `JSON` from the dropdown, and enter the following JSON

```json
{
  "title": "My Postman Book",
  "content": "This is my Postman book",
  "status": "publish"
}
```

- Hit send and the book will be created, returning the JSON response of the new book - To be sure, go ahead and check the book in the WP dashboard
- To update a book, you use the same request configuration to add a book, but you change the endpoint URL to include the book ID

> http://twenty24.luna/wp-admin/post.php?post=285&action=edit

- To delete a book, you use the same endpoint URL as updating a book, but you change the request method to DELETE, and don’t send any data in the request body

Using a tool like Postman to test REST API endpoints is a great way to learn how to use the WP REST API. It’s also extremely useful for testing WP REST API requests, by ensuring that the data you intend to send is formatted correctly and that the request is being made to the correct endpoint

### Creating a Book

> use the WP REST API and api-fetch to create a new book

- you need to pass the title and content fields as a POST request to the books endpoint
- use the plugin that allows you to list books as a starting point
- you’ll need to update the page with a form that will allow you to enter the title and content of the book you want to create
- add it to the `bookstore_render_booklist()` admin page callback function, below the existing HTML
- With the form added, the next step would be to add the JavaScript that will handle things when the button is clicked
- Now that you have the button click event listener added, you can add the code that will handle the creation of the book
- it’s a good idea to create a separate function to create the book and call that function on the click event
- you need to create a submitBook function - Then update the click event listener to call that function
- Inside the submitBook function, you’ll need to get the title and content values from the form fields
- then create the request to the books endpoint using api-fetch, by setting the path to the books endpoint, setting the request method to POST and passing the title and content as a data object

### Updating and Deleting Books

- You can use the same api-fetch implementation for updating items as you did for adding items. You need to update the path to include the ID of the data entity being updated, as well as the updated data object, with the new values for the fields you want to update
- Deleting a post only requires the path to be set to the URL of the item, and setting the method to DELETE

```js
// you need to create a new form and button
const updateBookButton = document.getElementById( 'bookstore-update-book' );
if ( updateBookButton ) {
    updateBookButton.addEventListener( 'click', updateBook );
}

function updateBook() {
    const id = document.getElementById('bookstore-book-id').value;
    const newTitle = document.getElementById('bookstore-book-new-title').value;
    const newContent = document.getElementById('bookstore-book-new-content').value;
        wp.apiFetch( {
        path: '/wp/v2/books/' + id,
        method: 'POST',
        data: {
            title: newTitle,
            content: newContent
        },
    } ).then( ( result ) => {
        alert( 'Book Updated!' );
    } );
}

const deleteBookButton = document.getElementById( 'bookstore-delete-book' );
if ( deleteBookButton ) {
    deleteBookButton.addEventListener( 'click', deleteBook );

function deleteBook() {
  const id = document.getElementById('bookstore-book-id').value;
  wp.apiFetch({
    path: '/wp/v2/books/' + id,
    method: 'DELETE',
  }).then(result => {
    alert('Book deleted!');
  });
}
```

> But you need buttons for both

. . . . . . .

## Extending the WordPress REST API

- https://learn.wordpress.org/lesson/extending-the-wordpress-rest-api/
- The WordPress REST API provides an interface for fetching, adding, updating, and deleting data from a WordPress site in a uniform way
- While the schema for the data types that are available in the REST API is quite extensive, there may be times when you need to store additional data that is not part of the core schema
- learn about two methods of adding fields to your REST API requests, either by enabling custom fields in the REST API route, or by making custom fields available as top-level fields

### Important note about modifying responses

- it’s important to note that modifying WP REST API responses can have unexpected consequences.
- Changing or removing data from core REST API endpoint responses can break plugins or WordPress core behavior, and should be avoided wherever possible
- If you need to retrieve a subset of data from a REST API request, the recommended method is to rather use the `_fields` global parameter, to limit the fields returned in the response
- you can use the fields parameter to limit the fields returned to just id and title, if those are the only fields you need for your application

> Adding fields to a REST API response is less risky

### Working with custom fields

- custom fields, also known as metadata, are often used on custom post types, to store additional pieces of data that are specific to that post type
- Under the hood, these custom fields are stored in the postmeta table, as a set of key/value pairs attached to the post by the post id
- WordPress also supports metadata on other data types, such as comments and users
- The WP REST API allows you to create or update custom fields when creating or updating data
- This is possible by passing an object of key/value pairs to the meta property of the post type you’re working with
- in order to use a custom field, you have to register it first. This is done using the [register_meta function](https://developer.wordpress.org/reference/functions/register_meta/)

### Registering a custom field

- register a custom field called `location` on a post, use the register_meta function like this:

```php
add_action( 'init', 'wp_learn_register_meta' );
function wp_learn_register_meta(){
    register_meta(
        'post',
        'location',
        array(
            'single'       => true,
            'type'         => 'string',
            'default'      => '',
            'show_in_rest' => true,
        )
    );
}
```

- While it’s possible to add this anywhere to a plugin, it’s recommended to add it to something like the init action hook
- It’s important to ensure that the show_in_rest property is set to true, otherwise, the custom field will not be available in the REST API
- This will enable the custom field to be added to the REST API schema for a post, and will also allow you to post data to the custom field using the REST API. This is handled by passing the custom field as a key-value pair in the meta object of the request body

### Enabling Custom Fields for the specific WP REST API routes

- As of WordPress 4.9.8, it’s possible to use `register_meta` with the `object_subtype` argument that allows one to reduce the usage of the meta key to a particular post type

```php
register_meta(
  'post',
  'isbn',
  array(
    'single'         => true,
    'type'           => 'string',
    'default'        => '',
    'show_in_rest'   => true,
    'object_subtype' => 'book',
  )
);
```

> https://example.com/wp-json/wp/v2/book

```json
{
  "title": "New Register Meta Book",
  "content": "As of WordPress 4.9.8, it’s possible to use register_meta with the object_subtype argument that allows one to reduce the usage of the meta key to a particular post type.",
  "status": "publish",
  "meta": {
    "isbn": "978-1-4302-6418-2"
  }
}
```

> Something is wrong - my screen is different than his - he is showing custom fields boxes below the text editor but that looks like the classic editor - also, my paragraph is not a paragraph block but instead is a `classic` block???

### Adding Custom Fields as top-level fields to API Responses

- The other way to add custom fields to the WP REST API is to add them as top-level fields on the API responses
- In the earlier example, the isbn was registered as a meta field and is therefore available in the meta object of the REST API response. But what if you’d prefer to have it as a top-level field, alongside the title, content, and excerpt?
- This can be achieved using the [register_rest_field](https://developer.wordpress.org/reference/functions/register_rest_field/) function

### Adding a custom field as a top-level field

- you need to register your rest fields in the `rest_api_init` action hook. This is to ensure that the field is only registered on the REST API
- then use the `register_rest_field` function to register the field
- The first parameter is the object type the field should be registered on. This can be a string, for a single object, or an array, for more than one object
- The second argument is the name of the field
- The third parameter is an array of arguments that determines how the field functions. You need pass at least the following three arguments to the array.

1. get_callback – a function that returns the value of the field
2. update_callback – a function that updates the value of the field
3. schema – an array containing the schema for the field

- you can leave the `schema` argument of the rest field as `null`, but you will need to specify the `get_callback` and `update_callback` functions
- These are the functions that will be triggered when the API request is made, either to fetch the data or to create or update the data
- By default, an array of the post type’s prepared data is passed to the get_callback function as the first argument
- An implementation of this function could be as straightforward as returning the value of the custom field
- The value sent for the field from a REST API create or update request is passed to the update_callback function as the first argument, and the model object (ie the post) as the second

### Including Schema

The schema argument is an array that describes the schema for the field. While it’s not a requirement, including a schema is encouraged. If nothing else, it helps future developers understand what the field is for. It can also be used to validate the data being sent when creating automated API tests.

You can read more about how to define the schema for REST API resources and fields in the [WP REST API Handbook](https://developer.wordpress.org/rest-api/extending-the-rest-api/schema/).

### To register_rest_field or not

When deciding whether to only use `register_meta`, or to add the use of `register_rest_field`, you should consider the pros and cons of each approach.

The main advantage of using the `register_meta` only route is that you do not need to add any further code to enable storing or retrieving data from the custom fields, as long as you remember to fetch and save the data using the meta-object in your application code. You enable the field to show in the REST API, and you can use it straight away. **This is also the more performant option**, as it does not add any additional code that needs to be executed.

On the other hand, the advantage of using the `register_rest_field` route is that you can perform additional processing on the data before it is returned, or before it is saved. **For example, you could perform some validation on the data before it is saved to the database**. You could also add hooks to the `get_callback` and `update_callback` functions to either perform additional processing on the data or to allow other developers to extend your custom fields. The downside is that you’re adding a slight overhead to the API requests, as it adds more code that needs to be executed.

Ultimately, the route you choose should be decided on a case-by-case basis.
