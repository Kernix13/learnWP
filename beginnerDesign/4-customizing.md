# Customizing themes and templates

> EXCELLENT COURSE - was the column reverse in this section?

## Intro to the Site Editor

> https://learn.wordpress.org/lesson/intro-to-the-site-editor-copy/

### Navigation

- Appearance > Editors > Navigation: you can quickly see and tweak all your menus
- You can make simple edits directly - click on the three vertical dots next to the menu item’s name, you can rename, duplicate, and delete the item as required - or Edit
- If opened in the editing mode, you can make certain changes without distractions
- You can add new pages or other menu items when you click on the plus icon. You will notice that the Navigation block is locked in this area.
- If you want to style your navigation menu, you must open a template or the template part it is part of

> CAN I CREATE DIFFERENT NAV MENUS HERE?

### Styles

When you select Styles, you will be able to browse through a variety of different style combinations that come with your theme. When you click Edit Styles, you can browse your styles from here and then change your site’s typography, colors, and layout

1. Typography: text, links, headings, captions, and buttons - you also now have access to a font library

- click Manage Fonts: you can install, remove, and activate local and Google fonts across your site with any block theme

2. Colors: you can also change the colors for different global elements on your site
3. Layout: you have control of elements such as padding, margin and block spacing

### Style Book

The Style Book allows a user to preview every block that can be inserted into your site. It gives you a preview of how global styles will affect any blocks displayed without the user inserting those blocks into a template

- you can customize the appearance of specific blocks
- notice there is a little eye at the top of the right panel
- a block’s styling can be adjusted within the Style Book
- note that changing an individual block in your Style Book takes precedence over the global styles you’ve set (FROM PREVIOUS SECTION)

### Style Revisions

- go ahead and click on Style Revisions next to the Style Book icon
- Style revisions will open up when you’re editing a template in the Style Book
- The styles revisions feature adds a visual way to browse changes to your styles over time, and you can easily revert to a previous stage
- You merely have to select the version and then click on Apply

> When you click on the three vertical dots next to styles, you can reset styles and add additional CSS

### Pages

...go to Pages to create and publish pages

- To add a new page, click the plus icon next to pages and create a draft
- When you open a page, it is important to remember to add content to the Content block. To put it another way, the Content block is the house or the container for all your content
- The second thing to remember is that you can’t customize your header and footer when editing a page

> You will not be able to add content to a template. Content, of course, gets added to posts and pages. The Content block is merely a placeholder in this context

### Templates

Templates provide the structure for how your content is displayed. When you select templates, you will notice a range of templates that come with your theme, built-in templates.

A template provides structure. A template usually includes a header template part and a footer template part. A template is only used to modify the layout or design of the page

The `Post Content` block pulls the content from the page or post assigned to the template

- Page template: displays a single page
- Index template: a fallback template
- Single Post template: displays the layout of single posts
- Custum templates:
- `+`: add a variety of new templates, even a custom template that can be applied to any post or page

...click on the three vertical dots and select Replace Header (or Footer) - you can replace your current header with one of your existing header template parts or header patterns that come with your theme

Another option you have is to select your header and then click on Edit. This will allow you to modify your header or footer within template editing mode without any other distractions

### Assigning a template

To assign a new template to a page or post, open the relevant content - open the sidebar settings on the right. Next to Template, click on the name of the template, select Swap Template, and then you can choose a custom template to assign to your page or post

### Managing templates

> Bulk Edit???

### Patterns

- When you select My Patterns, you can create and manage your own custom synced and non-synced patterns
- custom patterns and patterns that come with the theme in their relevant categories
- Template Parts, we can also create and manage our header, footer, and general template parts. Template parts are essentially patterns. They are synced reusable components that can be used across your site

### Custom patterns

- My Patterns > click the Inserter next to patterns and then select Create Pattern
- give it a name > add it to a category > sync or unsynched
- A synced pattern will sync across your entire site, meaning if you change your pattern in one place, it will update anywhere it is used
- Non-synced patterns are just regular patterns that can be edited independently
- synced patterns have a purple icon and non-synced patterns don’t
- you will notice that the patterns that come with your theme are locked, and you cannot edit them.
- But when you click on the three vertical dots below a pattern, you can copy it to your My Patterns area

### Template Parts

- You can create and manage our header, footer, and general template parts
- You can create custom headers and footers or customize template part patterns that come with your theme
- To create your own template part, click on the plus icon at the top next to patterns and select Create a template part
- When you add a new template part, you can choose between general header and footer template parts.
- General template parts are not tied to any particular area, so remember to give them a descriptive name
- you will be able to modify and edit your template part in template editing mode
- you can easily replace one of your headers or footers with a pattern or an existing template part from the library

### Command Palette

...the Command palette that will save you loads of time and help you move around your Site Editor more effectively

The command palette allows you to complete tasks and navigate within the Site Editor swiftly

You can type 'new' to create a page, post, etc or or 'pattern' to go to patterns

- You can do CTRL + K or in the site view sidebar by clicking the search icon or merely click on the title bar

> EXCELLENT VIDEO

..................................................................

## Differentiating between homepage display settings and various templates

> https://learn.wordpress.org/lesson/differentiating-between-homepage-display-settings-and-various-templates-copy/

WordPress uses templates to create the layout and structure for a page or post

### Pages template

The pages template is the default template, and every new page you create will be assigned to this template. You will also possibly see other custom page templates depending on your theme, such as a page with no title, a page with a sidebar, etc

The `Content` block or the `Post Content` block:

- The Post Content block pulls in the content from pages assigned to this template
- You don’t add content to the page template
- You only provide structure

### Blog Home template

...we have to discuss the homepage display settings

- Settings and click on Reading > select a static home page and a static blog page
- If you have selected a static home page, all your pages including your home page will be assigned to the page template
- If you have selected a static blog page or posts page, your blog or posts page will be assigned to the blog home template

> Please note you will edit the content, the header, and the footer of your blog page or posts page right within the blog home template. So yes, you will build your entire blog page or posts page within the template

But what if you have selected your latest posts as your homepage display? Well, your blog home template will become your homepage. In this case the blog home template is also indicated by the home icon on the left

> _Very important tip_: to add the Homepage link, add the `Home Link` block. This means your home navigation menu will go to the home page display you set

### Index template

The index template is used as a fallback template for all pages when a more specific template is not defined. It is not advised to use the index template for your homepage or blog page

It would be best to add a new template. So when we click on the plus icon next to templates we can add the blog home template if available. Or assign a custom template for our latest posts’ homepage or static blog page

### Single Posts template

This template influences the layout of individual posts. You don’t add content to the single posts template, but you can modify its layout. For example, you can move around theme blocks such as post author, post date, post category, post tag, etc

### 404 template

No page is assigned to this template - If you want your 404 page to have a unique look and feel, you can edit the 404 template directly

### Search Results template

This template will be displayed when a visitor performs a search on your website. You can modify this template and change how search results are displayed

### All archives template

The all archives template displays groupings of posts by categories, tags, or archives such as author, month, or year.

...notice that it says archive type and then name at the top...the archive type can be a category, a tag, an author, etc

The layout of this page is determined by the all archives template, which can be modified

### Adding templates

...what if you wanted to create a template for a specific category or tag, or author?

you can do that by adding a template. If you click on the Inserter or the plus icon next to templates, you can add a template for author archives. You also have the option to add a category template for all your categories or individual categories

You can also create a template for date archives or tag archives. Then you will notice you also have an option to add a new page template or a single item post template

You can also add a custom template. A custom template can be manually applied to any post or page. Another template that you can add is a front page template - the front page template will display your site’s homepage, whether it is set to display the latest posts or a static homepage. The front page template takes precedence over all templates

> EXCELLENT VIDEO

..................................................................

## Using page templates

> https://learn.wordpress.org/lesson/using-page-templates-copy/

A template provides the structure for how a page is displayed. That usually includes a header template part, a content area, and a footer template part

Templates are not for posting content; templates for a post or page display your content with the Post Content block...design templates that can be applied to single or multiple pages and posts

### Exploring templates

The Editor can be used to customize the styles of your entire site, edit pages, modify templates, as well as manage all the different patterns on your site

1. Page template: creates the structure for displaying individual pages
2. Single Post template: displays a single blog post
3. Index template: displays posts
4. 404 template displays when no content is found

To add a new template, click on the Inserter or plus icon next to templates. A modal appears where you can choose between different template options. You can create a template for a specific page, a template for all your post categories, or an individual category

You can even create your own custom template that can be applied to any post or page

other built-in templates:

- Blank template:
- Page No-Title

### Editing templates

After selecting the relevant template, you can click on the Edit icon in the sidebar next to Pages or on the template screen on the right. Once your template opens up, you can start editing your header and footer template parts

When you edit a template, you must remember to separate the dynamic and static parts.

- The dynamic part is the content part that will change for every page or post that uses the template
- the content from your page or post will be displayed where the Post Content block has been added to your template
- The static parts are the reusable parts of the template that will stay the same, like the header and the footer

The Site Editor, therefore, makes a clear distinction between editing a page’s content and its template, making it easier for you to switch between the two modes and view them in the appropriate context

> notice that the `Post Content` block is only a placeholder

...three vertical dots, and then replace the footer...If you would like to return to the page, click on Back on your toolbar

### Assigning templates

...assigning a different template to a page or post

To assign the new custom template

- click on the template name and add a new template from there
- You can edit the template assigned to the page, or if you click on the drop-down, you can select or assign a new template to this page

### Header and footer template parts

You can edit a header or footer template part right within a template

Another option is to make your way to patterns in your site view sidebar

To add a new template part, click on the plus icon next to “Patterns” and select “Create Template Part”. You have an option between General, Header, and Footer Template Parts

- General template parts are not tied to any particular area
- When you click on the three horizontal dots below a template part, you will be able to rename, duplicate or delete it

> EXCELLENT VIDEO

..................................................................

## Using template parts

> https://learn.wordpress.org/lesson/using-template-parts-copy/

### What are template parts?

Template parts are groups of blocks you can use to create repeated parts of your template, like the header, footer, and sidebar

You create and modify our header and footer template parts within a template. Some block themes provide more or fewer options, but almost all come pre-packaged with the header and footer

WordPress has made it even simpler by providing header and footer patterns that are ready to be used and modified - when you click on the three vertical dots of the header template part and select Replace header, you will first notice the existing template parts - below that, you will find header template part patterns

### Editing a template part

- Open List View > add or change what you want > Save

> Reminder: Template parts are synced and will be updated everywhere they have been used - the color purple indicates when a pattern is synced

What if you wanted a different header on your home page but you would like the rest of your website to have a standard header - you would want to create a new header template part or replace the header with a pattern and add it to your blog home or front page template

### Creating a template part from scratch

- To create a new template part, click the plus icon next to patterns and select `Create template part` - name it - Create
- grab a pattern from the Patterns Directory if you want

..................................................................

## Customizing theme settings: Colors, fonts, typography and layout

> https://learn.wordpress.org/lesson/customizing-theme-settings-colors-fonts-typography-and-layout/

When using a block theme, you can customize colors, fonts, typography, and layouts for your entire site using Styles

### Global Styles

1. Typography: you can manage fonts, install Google fonts, or upload a font from your computer

- below Elements, we can customize the text, links, headings, captions and buttons
- Text: update the font, size, appearance, line height, and letter spacing

2. Colors: you can select one of the color palettes that come with your theme, create a custom color palette

- you can change the color for your text, your background, and other elements such as links, captions, buttons and headings

3. Shadows: you can edit default styles or create custom shadows

4. Layout: allows you to change the content width for the main content area on your site, as well as padding and block spacing

### Style Book

...the Style Book is a preview of the design decisions you make in the styles section. The Style panel is where you define your design and the Style Book is where you can see those designs applied across various site elements - it is a visual preview of how your style changes affect various elements and blocks across your site - You can also customize individual blocks, which allows you for more detailed control over your site’s design

- click on the eye icon to open our Style Book
