# Intermediate WordPress User

4. Intermediate WordPress User

> https://learn.wordpress.org/course/intermediate-wordpress-user/

- 38 lessons

## User management

> https://learn.wordpress.org/lesson/user-management-2/

- assigning roles
  - Administrator: full CRUD for everything - multi-sites have a Super-Admin - usually only 1 admin per site
  - Editor: can publish and manage posts and pages, media, comments - no themes, plugins, updates, site settings - they manage the work of other users
  - Author: only publish/manage their own posts
  - Contributor: can manage their posts but not publish
  - Subscriber: only manage their profile (Useless?)
- User Role Plugin:

> NOT THAT GOOD

## Taking advantage of query loops

- Query Loop block: to display posts based on params -
- it contains featured image, categories block, post title, post author, post excerpt - no meta?
- Post Meta block: date block, author block, categories block
- to change your theme's default query block, select that block > click Replace in the floating toolbar > browse the patterns and select one > then customize if you want
- when you add a query loop block you can choose Start Blank or Choose for a pattern
- for featured image, be sure to change the aspect ratio so they all look the same
- editing the query loop block: select the block > sidebar settings > deselect "Inherit default query from template" - not an option for me - instead I have 2 btns: Default and Custom
- Custom I assume has a filter for Taxonomies (Cats & Tags), Authors or KWs
- you can choose posts, pages or custom post types for a custom query - or to include or exclude sticky posts - under advanced you can turn off Reload full page

> **Query Block Design Options**: Query block patterns have moved from a modal interface to a dropdown menu under the block toolbar’s “Change design” option

## Using the Comments block

- Comments block - just delete it if you don't want comments
- you can display comments on your pages > click Discussion > Choose Open
- there is also a LAtest Comments block - the block is not to add comments, just to display them

> SUCKS

## Designing with the Columns block

- you can add a cover block to each of your columns
- to add another column you can:
  - 1. select one then use the vert dots to duplicate
  - 2. click the `+` between cols
  - 3. select the parent block, go to settings and change the #
- Always make sure to select "Stack on mobile"
- you can set the color and bg-color, set typography,
- block spacing appears for the parent to add margin b\tw the columns (Gap) which is better than setting it on the columns individually
- also border, radius, drop shadow
- you can select blocks like paragraphs and transform them to columns

> Good

## Using the Group block

> Using the group block is one of the cornerstones of using the block editor

- you have a settings option to add a bg image - choose full width - she clicked the 3 vert dots next to bg image and had a size choice with position boxes and Cover, Contain and Fixed - I don't have that - oh, you have to click on your image file name - you can change the focal point
- you can also select images along with text elements to group them - group anything
- always just select the first option for the grouping types
  - the first type is "Group"
  - 2nd is Row (flex-direction row)
  - 3rd is Stack (flex-direction column?)
  - 4th a Grid block

> Okay

## Designing with Row and Stack blocks

> EXCELLENT VIDEO: https://learn.wordpress.org/lesson/designing-with-row-and-stack-blocks/

- when you select the group block you can choose from group, row or stack
- `Row block` - comes in handly when you need to justify like Space Between
  - there is also vertical alignment options
- the row block is perfect for headers
- `Stack block` - columns with unequal height - he has a column with a stack inside with a stack inside that for the text and the a button not in a stack

  - set the outside stack block to min-height 100% to get the bg color to go full height
  - to get the button to the bottom choose the parent stack and set it to space between

- Columns
  - Column
    - Stack: Bg color, space between for vertical, min-height 100%
      - Heading
      - Paragraph
    - Buttons
      - Button

## Uncovering the Cover block

> EXCELLENT VIDEO: https://learn.wordpress.org/lesson/uncovering-the-cover-block/

- to display text and other content on top of an image or video
- it's another type of container block
- you can add a color overlay - WP automatically adds one based on the tones of your image
- you can set the image to fixed background which creates a parallax effect

> Fixed background not working - inspector has `background-attachment: scroll`

> To prevent your image being cropped on mobile change the aspect ratio!!!

- he chose to group 2 cover blocks in a group to get rid of the block spacing?

## Advanced WordPress block layouts

> EXCELLENT VIDEO: https://learn.wordpress.org/lesson/advanced-wordpress-block-layouts/

- Separator block - wide line

## Building a page with only patterns

- https://learn.wordpress.org/lesson/building-a-page-with-only-patterns/
- go to wordpress.org > Extern > Patterns > like the ones you like - they will be under "My favorites"
- copy each pattern and paste into a page - then start editing
- for images, click on each image and select Replace
- rewrite all the text in headings, paragraphs, buttons, lists, etc
- then change the fonts, font sizes, color, bg colors, etc
- for each section and blocks change the layout (wide-width, full, etc), padding, margins, block spacing, etc
- you can copy/paste styles for things like buttons

> Pretty good

## Creating your own custom synced and non-synced patterns

- save designs you like that you will reuse - you can sync it or not
- non-synced patterns can be edited without affecting all other instances
- for a copied or created design you like: click the 3 vert dots for the container block > select Create pattern > name it then add it to a category > then toggle the Synced button > Create
- all your patterns will be under "My patterns"
- Synced patterns have a purple icon
- if you want to save one of your theme's patterns as your own, click on the vert dots and select Duplicate - it will then be in My patterns and you can edit it
- to create a custom pattern: Appearance > Editor > Patterns > Add new pattern > Give it a name and assign it to a category > Click Create > Design it

> Pretty good

## Organizing your Media Library

- photos, graphics (gif, png, svg), audio, PDF, spreadsheets, PowerPoint, video, word docs, .txt,
- you can categorize your media library with a plugin: `Media Library Organizer`
  - Others: FileBird, Wicked Folders, WordPress Real Media Library

> Not good

## Differentiating between homepage display settings and various templates

- Blog home and Index templates:
- Pages template: every new page uses that
- you can edit every part, including header & footer, of your Home page and Blog page right in the template.
- Blog Home Template
- Navigation: Home Link block -
- Index is a fallback template for all pages
- Single Post
- 404 Template
- Search Results template
- All Archives template

> Not good

## Personalizing your 404 template

- you don't want people to leave the site - give them links

> Not good

## Customizing the search results template

> https://learn.wordpress.org/lesson/customizing-the-search-results-template/

- remember click on the three vertical dots next to the name and select "Clear Customizations". This will revert back to the original state of the template

> GOOD

## Customizing your single posts template

> https://learn.wordpress.org/lesson/customizing-your-single-posts-template/

- Single Posts Template -
- Custom Post Header: he added a `/cover` above the header then move the header in there and set it to center top - but he just copied the `/row` inside the header into the cover block - he also moved the meta into there and deleted the header?
- he did not do center top but added padding to the title block and added a 70% opacity to the cover block (white)
- you can "Clear customizations" if you don't like your changes - `WHERE?`
  - go back to Templates > click the 3 vert dots > select "Reset"

> ALWAYS CHANGE THE FEATURED IMAGES ASPECT RATIO SO ALL THE IMAGES HAVE THE SAME SIZE!

> EXCELLENT VIDEO!!!

## Creating a custom template

- Why create them?
  - for an event
  - a landing page
  - different types of blog posts
  - different pages
- a different header for the contact page
- create one: "Custom Contact" > when you get the popup "Choose a template" you can click "Skip" at the bottom right
- click Header > click the 3 vert dots and select "Detach"
- create Contact and click the PAges template then "Swap template"

Landing page:

- create a custom template > choose "Skip" so nothing is in there > Only add a `/content` block and make it full width

> GREAT

## Adding and customizing a category template

- you can choose "All categories" template or "Category" template for each specific category
  - though you will get a list of yout categories and you can choose one but not any other ones
- he chose "Skip" for this one too - he added a large header/hero image
- when you choose the "Post template" block you can choose how many columns

> GOOD

## Styling your site with Global Styles

- font pairing: check out https://www.fontpair.co/all
- color palettes: https://coolors.co/palettes/trending
- on a template click the half-moon to open Styles > click Browse styles > that shows you the color palettes
- below "Browse styles" is Typography, Colors, Background, Shadows, Layout
- Typography: links is an option but no hover option???
  - you can set your presets for sizes, and a lot more
- you can connect to Google fonts
- Click colors > Palette > and there is an option to add custom colors

Layout:

- you can set the width of "Content" and "Wide"
- Tablet Screen Resolution Stats Worldwide: 601, 744, 768, 810, 820, 834, 962
- Mobile Screen Resolution Stats Worldwide: 360, 375, 385, 390, 393, 412, 414, 428, 430

Blocks:

- Customize the appearance of specific blocks and for the whole site
- only change specific blocks that you think needs changing

## Using the Style Book

> difference between global styles and the style book

> How do you add Hover styles? How do you change link colors?

- you can make changes and see a preview

## Domain management: Understanding DNS records

- Domain: name, extension, and somtimes a prefix/sub-domain
- DNS: Domain Name System - numbers

  - Zone files: special text files, contain the individual DNS records of each website on which server to find it, how to connect to it, and more
  - there are a few dozen DNS types - but 5 primary
  - `NS records`: nameserver - tell other computers which server manages the info about your website - they direct the network traffic to where your website, mailbox, and other online assets are stored - every domain must have NS records, usually 2 of them in case one name server is down
  - Why do you have to edit your nameservers? when you have 1 company to manage the domain, and another for hosting - you would connect the registrar with the hosting via NS records -> DNS Zone Editor > delete the old NS records and copy/paste the new ones for the registrar - now your domain is connected to your hosting
  - `A records`: Address - ensures that when someone visits your site from a browser - if you are using your host's nameserver, you probably don't need to set an A record - your web host will set it for you
  - `CNAME records`: Canonical Name - an alias that lets you point one domain name to another, which is how you would set up subdomains or direct traffic to a different web address
  - the most common name for CNAME is "www" - that ensures people can access your website whether they use www or not
  - you can also use CNAME to direct users to a separate website (subdomain)
  - `MX records`: Mail Exchanger - handle the mailboxes of your domain - you need these to send and receive emails at (e.g.) info@yourdomain.com
  - `TXT records`: "sticky notes" attached to your domain - they contain all sorts of helpful info like verifying your domain for analytics services or optimizing emil security

How do you edit these records:

- vis your domain registrar or hosting provider's control panel
- they provide CRUD for your DNS records

How long does it take:

- whenever you make changes in your DNS zone Global DNS servers across the web need to update the records thay have stored
- that updating is known as "Propagation" - can take between 2-72 hours
- check on https://dnschecker.org/

> EXCELLENT!

## Website optimization

- delay = bounce so optimize for speed
- pertains to the UX of load time and runtime
- what affects performance: software, hardware, network conditions
- Software: code & content - colors have no effect on perfomance - what can though are fonts, graphic assets, carousels, popups - good practice to adopt newer, more performant file formats
- minimizing the # of assets is useful but so is how they are loaded - a well-coded theme makes all the difference
  - Themes & Plugins: bloated ones or excessive requests
  - Embedded content & third-party elements: ads: analytics, social media widgets, externally hosted assets all delay loading, slow down response times, hog bandwidth, ...
  - How performance is measured: 1) Synthetic or 2) REal USer Monitoring (RUM) - both happen in the browser - synthetic means running tests "in the lab" - while rum is "in the field", collecting data from actual site visitors
  - in either case, the tests would likely be based on a set of 3 metrics outlined by Google and adopted across the industry = `Core Web Vitals`:
    - 1. LCP: `Largest Contentful Paint` - measures when the largest element on the page becomes visible
    - 2. CLS: `Cumulative Layout Shift` - measures how much the elements on the page shift while the page is loading -
    - 3. INP: `Interaction to Next Paint` - measures how long it takes for the page to respond to user interactions - clicks, taps, keyboard inputs
    - FCP" `First Contentful Paint` - when the browser displays the first bit of content
    - TBT: `Total Blocking Time` - the time elapsed after FCP and BEFORE visitors can interact with the site

> Loading too many assets and elements and failing to do so properly

- **Web Page Test: https://www.webpagetest.org/**
- **Performance Lab plugin**
- Hosting is another factor
  - TTFB: `Time To First Byte` - measures the time it takes for the browser to receive the first byte - depends on the connection time of the visitor and the server - HOSTING MATTERS!
- Plugins: CDNs, Caching, Compression, Minification, Database optimization,
  - apply caching to reduce the # of requests

## Image optimization

- high quality images in the ideal format, size and resolution
- also adding alt text, title, caption, description, and file name

How to improve:

1. Edit the file name for keywords - png, jpeg, webp, avif - gifs have accessibility issues
2. add alt text - alt text improves SEO and helps vision impaired visitors
3. scale/crop
4. compress

- Modern Image Formats plugin - converts to webp or avif during upload
- check out https://squoosh.app/ - can save as webp

Optimal sizes:

- Header images: 1200x628
- Other: 640x480 up to 1024x768

## Essential security plugin features and settings

- Features: audits and scans - WAF (Web Application Firewall) - IP web adress detection to block -

> Look into REMOTE_ADDR - can't use with Cloudflare

- IP address detection always requires `proper server configuration`
- `wp-config.php` file - set permissions
- brute force protection is crucial
- 2FA is crucial
- backups and SSL (encrypting data between your site and visitors)

## SEO strategies

- quality content
- seo plugin
- develop a content strategy and target specific search phrases
- long tail KWs: lower competition b\c they are more specific
- semantic search: words similar to your main KWs
- content gap analysis: finding what topics your competitors are talking about that you are not
- site structure and UX: logical ordering of your pages and content
- improve page load speed and mobile optimization
  - compress images
  - use browser caching
  - responsive theme
  - clear mobile nav and avoid hover-only navigation
- link building: share on social media, guest posting,
- optimize internal links on your site

> Okay

## What is accessibility, and why is it important?

- A11Y: numerical abbreviation of the word accessibility
- WCAG: web content accessibility guidelines
  - POUR: Perceivable, Operable, Understandable, Robust
  - Perceivable: delivering the info so anyone can understand it
  - Operable: enabling people to use the interface and interact with the site
  - Understandable: ensure people can comprehend the info & use interfaces , e.g. form fields with labels
  - Robust: content remains accessible as technology advances & evolves
- Misconceptions: skip

Common categories of accessibility issues:

- low contrast text
- missing form input labels
- empty buttons
- no image alt text
- empty links
- no documant language

> Okay

## Testing your content for accessibility

- use proper heading levels, color contrast, meaningful alt text, linke text, ...
- wordpress includes 2 built in accessibility helpers
  - 1. Semantic structure: click Outline in the list view section - wrong ones highlighted in orange for headings
  - 2. color contrast: you see a message in the right sidebar for low contrast text
- accessibility plugins: WP Tota11y, Sa11y, and Editoria11y (focuses on content and structure)
- try browsing your website with a keyboard, no mouse - use the TAB key, ENTER or SPACEBAR to activate elements
- also change the device's color scheme to ensure things look and work well in dark mode or high-contrast mode

> Good

## Managing Settings: General

- URL settings is super important - don't change, something about only for SSL
- email address - can change it
- membership - "Anyone can register" - the default role is Subscriber

> Okay

## Managing Settings: Writing

- Default post format: interesting
- Post via email: to post from your email account - Mail Server, Login Name, Password, Default Mail Category - you need to create an email account with POP3 access - gmail or your WP email should work - but this feature may be depricated
- Update Services: lets other services know that you've updated your blog

> Ehhh

## Managing Settings: Reading

- Your hompage settings - Blog Home/Posts Page or Front Page
- WHEN YOU BUILD YOUR HEADER REMEMBER TO USE THE `HOME LINK` BLOCK
  - that will take users to your Home page or Blog Home page depending on the setting you chose
- RSS feed: for people to subcscibe and be alerted about new content
- Search engine visibility - only check when you are building the site but remember to uncheck it when you are done

> Okay

## Managing Settings: Discussion

- "Attempt to notify any blogs linked to from the post" - check this
- "Allow link notifications from other blogs (pingbacks and trackbacks) on new posts" - also check this
- don't check "Allow people to submit comments on new posts" if you don't want comments
- you can also make those changes on a post-by-post basis
- Other comment settings: cchecck the first two -
- Comment moderation: target words and links - held for moderation
- Disallowed comment keys - trashed
- Avatars:

> Good

## Managing Settings: Media

- WP automatically generates 3 sizes when you upload an image: thumbnail, medium, large - to improve site speed - leave t he default settings
- "Organize my uploads into month and year-based folders"

> Okay

## Managing Settings: Permalinks

- Permalinks = Permanent links - the urls that point to a specific page or post
- the default setting is "Day and name" -
- you can change the permalink for an individual post or page - in the sidebar click on the URL - edit the slug
- Permalinks for categories and tags -
  - the slug includes the word "category" followed by the category slug
  - same for tag
  - in the Optional section, consider changing "category" to "topics" and "tag" to "keywords"
- Redirecting permalinks: make sure yyou only change page structures when a post or page is new - or else you can get a 404 for the old link
- you would need a plugin to redirect your old urls

> Good

## Managing Settings: Privacy Policy

- always add a Privacy Policy page to your site - it is a document requred by law which discloses the info you collect of your visitors
- check out https://wordpress.org/about/privacy/
- WP provides a template that you can edit

> Ok

## Tools: Export and Import

- if you export, your sites contents are in a `xml` file which you can import into another WP site
- for Importing the xml file, choose WordPress at the bottom - that installs it - then click on "Run importer" > then choose the xml file and click on "Upload file and import" - for images remember to check Import Attachments
- NOTE: "unattached" media items are not included in the xml file
- NOTE: make sure you have the same theme activated for your new site
- NOTE: what is not included in this process is the site's design, themes, or plugins - to get all of that use a migration plugin

> Good

## Tools: Site Health

- the widget for Site Health can be found on the Dashboard
- there are 2 tabs: Status and Info
- Status: see critical info about your WP configuration - 2 sections for Security and Performance
- Info: a granular view of the technical aspects of your website
  - Check out `Server` for some good stuff
  - there is an export feature that lets you copy all the info about your site to the clipboard
- make a backup if you update WP or your PHP version
- "More or more recommended modules are missing" under "Performance" - aks your host to do it
- you can check out "Passed tests"

> Good

## Migrating your site Part 1: Changing to a new host and domain

Changing to a new host and domain...

- ... or moving from HTTP to HTTPS
- you need a migration plugin in your old and new website
- remember to make a backup
- some hosts have their own migration plugins
- export to "File" but also to an external drive like Google Drive or Dropbox
- Redirects: set up 301 redirects - they indicate to search engines that a page(s) has been moved

> Good

## Migrating your site Part 2: Changing your host but keeping your domain

Changing your host while keeping your domain name

- when signing up with a new host company, you'll be asked if you have a new domain or an existing domain
- when you do this you will have your website in 2 locations, your old and new hosting account - but the internet only knows about your old hosting account version -
- telling the internet that your website is in a new location is an extra step you need to do from the previous lesson
- website addresses are actually a series of numbers/letters called an Internet Protocol address (IP Address) -
- IPv4 protocol is just numbers like 192.0.2.146
- IPv6 is longer and is alpha-numeric
- they are part of the Domain Name System or DNS
- your new hostting account has a different IP address from the old host company
- you need to update the info in the Domain Name System to point to the new address
- you update your website's location by changing the Nameserver settings of your domain - they are located in the account where you registered your domain
- remember tjhta hosting and domain registration are 2 separatte functions
- your new host should send you the nameservers settings of your new account
- there are usually 2 of them - you need to use the new values in the old account
- can take 24-72 hrs to propagate - you can make a small change to a part of your site to see if the new hosting version is there

Other things to consider:

1. email accounts: you'll have to set up new email addresses for the new hosting company - some hosting companies will migrate your email
2. Content updates: after the migration file was created
3. Service renewals:
