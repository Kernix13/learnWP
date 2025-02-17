# Beginner WordPress User

> ALL OF THESE LESSONS ARE GREAT

## 3. Beginner WordPress User

> https://learn.wordpress.org/course/beginner-wordpress-user/

- 24 lessons
- universal themes: customizer and editor menu options like the theme `emulsion`

### Creating posts and pages with the WordPress Block Editor

- The Block Editor is used to add content to pages and posts, while the Site Editor is used to edit the overall look and feel of the site using templates.

### Intro to the Site Editor

- Style Revisions - icon between the eyeball and triple dots when in the stylebook or a template - can cycle thru changes and revert back

### Using template parts

- template parts are synched (Purple)

> Check this link for patterns: https://wordpress.org/patterns/?curation=community

### Setting up your pages, posts, site logo and navigation menu

**GREAT VIDEO**

> https://learn.wordpress.org/lesson/setting-up-your-pages-posts-site-logo-and-navigation-menu/

- in the Navigation block is a Page List block - select it and in the sidebar click edit to "detach" the page list so that you can manage the nav items individually
- when you select the navigation block you can click the 3 verrt dots for it in the right sidebar to 1) create a new menu, or 2) select another menu you created
  - click the gear icon to choose the hamburger icon
- Site Logo block

### Creating and customizing a header and footer

- Pages template > select header > select the header, click the 3 vert dots on the floating menu > and choose Replace header >

### Nesting and using blocks to create visually appealing content

- `Group`, Row, `Columns`, Cover, and `Media & Text` Block are the best way to group content together
- Is the Separator block used in case themes don't have Margin set?

**Group Block**:

- first create a heading then a columns block with 2 cols with text
- select both and group them
- before you can select Wide Width, toggle off "Inner blocks use content width"
- then choose Wide Width (Doesn't allow me to choose wide width, only full width)
  - yes it did but only after trying different things
- You can choose a background image to a group block
- you can use the group block to rename sections

**Media & Text Block**:

- choose an image for the left > add a heading and a paragraph on the right then a buttons block below that - style the elements
- select the parent block > change to Wide Width
- you can choose to align the image to the top, middle or bottom

> I'm working with twenty24 local install now

**Columns Block**:

- one of the most effective blocks to use to create complex layouts
- 2 paragraphs then an image > center the text then select the image and set the aspect ratio to square

**Cover Block**:

- allow you to display text or other content on top of an image or video
- it's great for headers and banners
- `/cover` > choose an image > add text and a button > style them > select text and button and turn into a Stack block
- the menu bar allows you to toggle the cover block to full height but you can drag the bottom to change the amount

### Using block patterns

- it is time-consuming to create layouts - that's where patterns come in
- go to the Patterns tab > click a category > select one then edit it
- or wordpress.com > Extend > Patterns > Search > Copy and paste
- if you create a design in the block editor click the 3 vert dots > select Create pattern

Template parts:

- Header, Footer, or General (Meta, Sidebar)
- in a template you can select the header or footer and use the 3 vert dots to replace them with another version

### Embedding media and third-party content on your website

- an embed is a way to display external media or content on your site without having to upload or host it directly: videos, social posts, maps, audio, crowd signal surveys, ...
- click `+` and scroll to bottom: Embeds > you can click the Embed block for links to other sites or select from the others
- actually you can type `/youtube` or whatever or even just paste the URL
- NOTE: you can transform an embed into a Columns or Group block so you can change the background color or layout
- if the Embed block does not work you can use the `Custom HTML` block
- the embed block does not work for Facebook and Instagram so

### 7 Tips to improve website security

- passwords - never use admin as a username - password managers - 2FA - users, plugins, themes, backups, security plugin, reliable host, SSL cert, spam detector,
- good security blogs: patchstack.com, wpscan.com, blog.securi.net

> HTTPS: ensures that no info is passed in plain text

### Managing spam on your site

- comment spam > comments with links > block them with built in features and a plugin
- Built-in features: Settings > Discussion:
  - 1. Limiting the # of links allowed - default is 2, try 1 but never 0
  - 2. comment moderation settings: txtarea where you enter words, ...
  - 3. disallowing comment keys - auto delete for certain words
  - 4. disable trackbacks - a large part of spam is trackbacks - trackbacks and pingbacks notify you that another blog has linked to your content and vice versa - turn this off "_Allow link notifications from other blogs (pingbacks and trackbacks) on new posts_"
  - 5. moderate all comments
  - 6. or turn off all comments by unchecking "Allow people to submit comments on new posts"
- How to mark a comment as spam: Comments > hover overr a comment > click Spam or check that comment > bulk actions > Mark as spam > Apply
- Anti-spam plugin: Antispam Bee, Clean Talk, Akismet

### How to backup your site

- hosting backups are the easiest - filesystem and DBs backups > select a date then click Restore
- updraft plus: same thing > just click Restore
- store a copy of your backups in a location separate from your web server like Dropbox or Google Drive
- you can manually update to a database using phpMyAdmin or File Manager but these methods are more technical
  - try this: https://developer.wordpress.org/advanced-administration/security/backup/

### How to improve SEO rankings

- First make sure to deselect Settings > Reading > "Discourage search engines from indexing this site" - only select that while your site is being built
- fresh content!
- quality content - EAT, expertise, authority, trustworthiness
- kw research, try https://www.wordstream.com/keywords and enter a url for a competitor site
- linking: site structure - crawlers use links to understand your site structure and look for more similar content - link to your own posts
- use quality external links
- metadata: description using a plugin always use a quality excerpt as WP uses them to write meta descriptions
- site speed: very important - host speed, caching, fast/slow theme, optimized images, ...
- good image file names and alt text
- sitemap - good for indexing
- Local SEO: local seo kw research, contact info on your contact page, post localized content, get local backlinks,

### How to use headings for accessibility and SEO

- headings help readers naviagte your post and are essential for acccessibility
