# Templates

## Template overview

> https://learn.wordpress.org/lesson/template-overview/

- describe the purpose and structure of a template
- list the sequence templates are loaded by WordPress, and
- with theme starter files in place, create a template from scratch

### What is the purpose and structure of a template?

Templates are created to give pages some structure. They dictate the layout and they can pull in different sections, like a header, main, and footer.

Now bear in mind with a block theme, you cannot put straight up HTML.

within the Site Editor, when we go into the code editor, the code for the pattern is actually pulled in here

```html
<!-- wp:template-part {"slug":"header","area":"header","tagName":"header"} /-->

<!-- wp:pattern {"slug":"twentytwentyfour/hidden-404"} /-->

<!-- wp:template-part {"slug":"footer","area":"footer","tagName":"footer"} /-->
```

No html in .html templates like `<p>Hello</p>` - in the template refresh and you will see `Block contains unexpected or invalid content.`

### What is the sequence templates are loaded by WordPress?

There's a template loading order and at the bottom is

1. the themes templates.
2. Next, if there's an active child theme, those templates take precedence.
3. Now finally at the top, we'll find that user customizations saved within the database have the highest priority.

- create a template from scratch

### Create a template from scratch

Let's build out our own 404 template, but let's first take a look at how the 404 template was created within the Twenty Twenty-Four theme

Use the 404 template to create a new one

If you look at 404.html you will see `wp:pattern {"slug":"twentytwentyfour/hidden-404"}`, so check out `/patterns/hidden-404.php`

In that file you see `wp:pattern {"slug":"twentytwentyfour/hidden-search"}` so go into `patterns/hidden-search.php`

> a pattern within a pattern

- so she has her own theme and copied over 404.html, hidden-404.php, and hidden-search.php
- but in both php files is a textdomain in `esc_html_x` so make sure to change it to your textdomain

. . . . . . .

## Template Hierarchy

> https://learn.wordpress.org/lesson/template-hierarchy/

- explain how WordPress uses the query string
- briefly explain the template hierarchy diagram
- describe the template hierarchy for a given page being queried

### How does WordPress use the query string?

When someone visits a page on a WordPress site, the query string helps determine which template should be used according to some rules. To better understand the query string itself, let's take a look at a simple example within the WordPress dashboard

The plain permalink structure uses the query string with the question mark, parameter, and then the value being the page or post ID in the database. If we were to change the permalink structure from post name to plain and then save that change, look at a page that we actually have available

blah blah blah

### WordPress database

now take a look at the database to see how WordPress handles the query string - WordPress has a table called WP posts and a field called post type

post with ID of 2...scroll down to the bottom, we'll see the post type is page

### Overview of the template hierarchy diagram

> just describing the template hierarchy graphic: https://developer.wordpress.org/themes/templates/template-hierarchy/

### Query example

- go to the main domain of a website, otherwise known as the front page, then WordPress will look for the front-page.html template
- If that's not available, it will move on to the home.html template
- And then finally, if that's not available, it will fall back on the ultimate fallback template which is your index.html template

. . . . . . .

## Template parts

> https://learn.wordpress.org/lesson/template-parts-4/

- describe template parts and how they work
- define template part areas
- add template parts to your theme

### What are template parts and how do they work?

Template parts such as headers and footers are small reusable content sections that can be added to the templates of your choice within your theme. Template parts are saved within your themes parts folder and we load template parts using the template part block

- in 404 template > take a look at the template part block here for the header:
  - We have the `slug` property that is the name of the template part file, in this case header and
  - then next is `area` and that designates where the template part will appear in the page layout and
  - then we have `tagName` and that creates the wrapper container element and in this case it would be the header tag

### What are template part areas?

Template part areas are a way to organize similar template parts. The use of areas is one significant difference which distinguishes them from patterns since they don't have the area property

### Add template parts to your theme

One of the ways to add template parts is to go into Manage all template parts and then click add new template part. Give your template part a name and choose its area then click create

create a new template part:

- name it header and assign the area header and click create
- insert some content then save changes
- create your new template part file and copy your code over into that file
  - copy and then go into the `parts` folder, create the new header file and paste your code

### Register a template part

This is done in theme.json

- search for `templateParts` > it should look like this:

```json
"templateParts": [
  {
    "area": "header",
    "name": "header",
    "title": "Header"
  }
],
```

- repeat this exact process for the footer

> to make your workflow a little easier, you can just install the create block theme plugin and then choose the save changes option
