# The programming languages of WordPress

## HTML

- HTML elements can also have attributes. Attributes are used to provide additional information about an element
- Certain elements allow you to include media, such as images, audio, and video
- When writing HTML, it’s important to write accessible HTML. Accessible HTML is HTML that is written in a way that makes it easy for people with disabilities to use
- you should always use semantic HTML elements, and use them in the correct way

> https://web.dev/learn/accessibility

## CSS

- used to define the colors, fonts, and layout of a web page
- Adding CSS to elements using the style attribute is known as inline styles, but it is not the best way to style an HTML document.
- Instead, you can use a `<style>` element to add CSS to the document
- It’s also possible to add CSS to a document using an external stylesheet.
- The dashboard has its own core set of CSS to control its look and feel
- Themes will ship with a custom set of CSS to style the theme elements
- Plugins that add content to the front end of a site will also use CSS to style that content
- WordPress also allows you the flexibility to add your own custom CSS, or to use external CSS frameworks, such as Bootstrap or Tailwind.

## JavaScript

- used to add interactivity to web pages
- JavaScript is a client-side scripting language, which means that it is interpreted by the browser
- `script` tag - added after the the html - the JavaScript needs to be able to access the HTML elements in order to work
- Because the browser reads the HTML document from top to bottom, adding the JavaScript at the bottom of the document ensures that the HTML elements have been loaded into the browser before the JavaScript is run
- it is possible to add JavaScript to a document using an external file. This is the preferred way to add JavaScript to a document
- One of the biggest uses of JavaScript is in the new block editor, which is powered by a JavaScript framework called React
- There are also a number of external JavaScript libraries that are used in WordPress
- WordPress allows you the flexibility to add custom JavaScript or external JavaScript libraries to your plugins and themes

## PHP

- PHP is used to create dynamic web pages
- PHP powers over 75% of the modern web
- PHP is often used to create administrative interfaces for websites but it is also used to populate the front end of a website with content
- PHP is a server-side scripting language, which means that it is interpreted by the server, and the results are rendered in the browser
- take note of the use of the query string on the anchor tag (`href="/index.php?color=blue"`), to pass data from one page to another. This is a common way to pass data from one page to another in PHP

Resources:

- [PHP Getting Started guide](https://www.php.net/manual/en/getting-started.php)
- [Official PHP Documenation](https://www.php.net/docs.php)
- [Learn PHP for Beginners on freeCodeCamp](https://www.freecodecamp.org/news/the-php-handbook/)

## MySQL

- MySQL is an open-source relational database management system
- SQL stands for Structured Query Language, and it is a programming language that is used to interact with data in a MySQL database
- One of the tools you can use to interact with a MySQL database is phpMyAdmin
- phpMyAdmin is a browser-based tool that allows you to interact with your MySQL databases using a graphical user interface but also run SQL queries on them

Creating tables

```SQL
CREATE TABLE colors (
  id INT(6) UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  type VARCHAR(30) NOT NULL,
  value VARCHAR(30) NOT NULL
)

-- Adding rows to a table: use the INSERT statement
INSERT INTO colors (type, value) VALUES ('header', 'red');

-- Reading rows from a table: use the SELECT statement
SELECT * FROM colors WHERE type = 'header';

-- If you just wanted the value of the value column
SELECT value FROM colors WHERE type = 'header';

-- Updating rows in a table: use the UPDATE statement
UPDATE colors SET value = 'blue' WHERE type = 'header';

-- Deleting rows from a table: use the DELETE statement
DELETE FROM colors WHERE type = 'header'
```

Database Keys

- ...the use of the value column to update or delete the row. While this works, it is not the most efficient way to update or delete a row
- This is because the value column is not unique, and there could be multiple rows with the same value.
- if you wanted to update or delete a row, you would need to know the value of the value column, which may not be possible
- it's usually a good idea that your database tables have an id column, and that the id is unique, and auto-incrementing.
- Its also a good idea that the ID has an index on it. Indexes allow MySQL to do much quicker selects, updates, and deletes, than if a field does not have an index

Running queries from PHP

- Unlike PHP and JavaScript, SQL is a query language that is executed on the database.
- because JavaScript is run in the browser, you generally don't make requests to the database from JavaScript, and would instead do it using PHP, which is executed on the server
- To run a SQL query, you would create a connection from PHP to the database (`mysql_connect`), prepare and then run a query, and the results of the query would be returned to PHP, as some type of variable
- if you use the default WordPress data types, you won't even need to worry about executing SQL queries

> WordPress includes a Database API that allows you to manage the connection to the database, and run any queries you need to

Resources:

- [MySQL Tutorial](https://dev.mysql.com/doc/refman/8.4/en/tutorial.html)
- [MySQL 8.4 Reference Manual](https://dev.mysql.com/doc/refman/8.4/en/)
- [Learn MySQL - Beginner's Course on freeCodeCamp](https://www.freecodecamp.org/news/learn-mysql-beginners-course/)
