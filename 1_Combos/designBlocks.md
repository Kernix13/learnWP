# The most important blocks

> EXCELLENT VIDEO: https://learn.wordpress.org/lesson/advanced-wordpress-block-layouts/

> I forgot to check gutenberg-blocks/WP-Docs for these blocks except for Cover

- `Group`, Row, `Columns`, Cover, and `Media & Text` Block are the best way to group content together
- Also Navigation, Query Loop
- it is time-consuming to create layouts - that's where patterns come in
- See [Blocks list](https://wordpress.org/documentation/article/blocks-list/)

## Group block

> Using the group block is one of the cornerstones of using the block editor

- you have a settings option to add a bg image - choose full width - she clicked the 3 vert dots next to bg image and had a size choice with position boxes and Cover, Contain and Fixed - I don't have that - oh, you have to click on your image file name - you can change the focal point
- you can also select images along with text elements to group them - group anything
- always just select the first option for the grouping types
  - the first type is "Group"
  - 2nd is Row (flex-direction row)
  - 3rd is Stack (flex-direction column?)
  - 4th a Grid block

...................................................................

## Row and Stack blocks

- when you select the group block you can choose from group, row or stack
- `Row block` - comes in handly when you need to justify like Space Between
  - there is also vertical alignment options
- the row block is perfect for headers
- `Stack block` - columns with unequal height - he has a column with a stack inside with a stack inside that for the text and the a button not in a stack

  - set the outside stack block to min-height 100% to get the bg color to go full height
  - to get the button to the bottom choose the parent stack and set it to space between

- Columns
  - Column
    - Stack: Bg color, space between, min-height 100%, padding
      - Stack:
        - Heading
        - Paragraph
      - Buttons
        - Button

. . . . . . . .

Creating a new header with blocks:

- editor > patterns > all template parts > add new template part > name it > header > add
- add a `/row` block > site logo > next to that add a group block so you can stack site title and tagline
- select parent block and click the `+` and add nav block
- select the site logo and group block and turn them into a row using the toolbar
- select the parent block select space between
- change the bg color to a light blue gray
- then select the header in front place > 3 vert dots > replace - but the alignment is horrible - had to puch up the padding
- add a spacer block below the header if you need more space
- finally, modify the group block s=with the site title and tagline to reduce the block spacing and tweak the tagline typography if needed

...................................................................

## Columns block

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

. . . . . . .

- one of the most effective blocks to use to create complex layouts
- 2 paragraphs then an image > center the text then select the image and set the aspect ratio to square

. . . . . . .

- first create a heading then a columns block with 2 cols with text
- select both and group them
- before you can select Wide Width, toggle off "Inner blocks use content width"
- then choose Wide Width (Doesn't allow me to choose wide width, only full width)
  - yes it did but only after trying different things
- You can choose a background image to a group block
- you can use the group block to rename sections

. . . . . . .

> https://learn.wordpress.org/tutorial/designing-with-the-columns-block/

> GREAT!

- the columns block is a container block used for custom layouts
- up to 6 columns - creates a grid effect
- you can choose from preset columns of 1, 2, or 3 and with varying widths
- you can add other blocks into each column
- cards are a perfect example as are testimonials - a media and text block looks like a columns block but is not
- you can add a cover block to each column
- you can set /columns to wide width or full-width
- you can duplicate blocks or reposition them via the arrows or through drag and drop
- if you select the parent block, in the right sidebar you can change the # of columns
- make sure to toggle on "Stack on mobile"
- you can change the appearance of the parent blokc or the individual columns
- can change all 4 sides of the parent block padding but only top and bottom margin
- you can turn on block spacing to change the spacing between columns
- you can transform other blocks to a columns block or a columns block to a group block

...................................................................

## Cover block

> EXCELLENT VIDEO: https://learn.wordpress.org/lesson/uncovering-the-cover-block/

- to display text and other content on top of an image or video
- it's another type of container block
- you can add a color overlay - WP automatically adds one based on the tones of your image
- you can set the image to fixed background which creates a parallax effect

> Fixed background not working - inspector has `background-attachment: scroll`

> To prevent your image being cropped on mobile change the aspect ratio!!!

- he chose to group 2 cover blocks in a group to get rid of the block spacing?

. . . . . . . .

- allow you to display text or other content on top of an image or video
- it's great for headers and banners
- `/cover` > choose an image > add text and a button > style them > select text and button and turn into a Stack block
- the menu bar allows you to toggle the cover block to full height but you can drag the bottom to change the amount

. . . . . . . .

> the hero pattern

...at its most basic level, it is typically a full-width box with a background that contains some text. Often, this is a heading, paragraph, and some buttons

To start:

1. click on Pages > Add New.
2. insert a Cover block into the empty canvas and choose a background color

For the hero pattern, create the following content within your inserted Cover block.

1. Add a `Group` block to the Cover block.
2. Inside the Group block, add a `Heading` block with the text "Welcome to My Site".
3. After the Heading block add a `Paragraph` block with any content (you can reuse the example below).
4. After the Paragraph block, add a `Buttons` block, using one button, with some call-to-action text.
5. For each of the Heading, Paragraph, and Buttons blocks, set the alignment to Center.

. . . . . . . .

Header using a cover block:

- Editor > patterns > all template parts > add new template part > name it > header > add
- add /cover and enlarge the image > change the opacity
- add a group block and insite site logo > enter and add a spacer block to push the site logo to the top - change alignment of site logo to center
- add a nav block below site logo and change the nav justification to center
- Save > front page and replace with this one
- my fucky header for front page is sticky and I had no way to change that so I moved the new header out of the group it was in
- i removed the spacer and shortened the height of the cover block

. . . . . . . .

> https://learn.wordpress.org/tutorial/uncovering-the-cover-block/

- a cover block lets you display text on top of an image or video
- can be used for CTA's, parallax images, video banner, window effect, header

Key features & settings

- the cover block is a container block which means it can contain other blocks within it
- you can add a cover overlay
- the toolbar for it allows you to use the featured image
- /cover > add image > set to full-width > you can change the position of the text and set the image to full height
- you can add a duo-tone filter
- you can toggle on "Fixed background"

> That's not creating a fixed bg image, s\b: `background-attachment: fixed;`

Video banner:

- /cover - choose video - full width - - add a heading

> you can drag the image or video to be smaller or larger

Window effect:

- /columns, 2 cols > make the parent full width > select left column and add a cover block - duplicate that twice - then duplicate the entire column - delete 3rd empty col
- click on each cover block and select Fixed background

Headers

- header with a featured image - template parts > add new > select header > insert cover block > full height > add a row block > add site logo in it and nav block > space between > select the row and insert a spacer block after it and enlarge it to sen the row block to the top (seems wrong to do that) - for the nav dese;ect allow to wrap so that everything is on one line

...................................................................

## Query Loop block

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

. . . . . . . .

> https://learn.wordpress.org/tutorial/taking-advantage-of-query-loops/

> EXCELLENT

- the Query Loop block is used to display posts based on specified params
- you customize it however you want: # of posts, filter for category or tag
- each query loop block is made of other blocks: post featured image, categories, post title, post author, and post excerpt
- you can customize the appearance and layout of those blocks including removing or adding blocks to the post loop like post meta
- his query loop shows that it is being displayed in grid view but mine are not
  - how do you make that happen?
  - I deleted the query loop, added it again and chose from a template then I was able to set it to wide width
- to change from grid click "Replace" in t he block toolbar

> With featured image block rememeber to set a value for the height so all the featured images display the same

- for equal height columns, select the container and set the min height to 100%

Variation

- remove the query loop, add another one and instead of "Choose" select "Start blank"
- then arrrange it how you want

Taxonomies and filters

- create a page named after one (or more than one) of your categories
- select the query loop block (which you styled) and open the sidebar settings for the block
- under QUERY TYPE change from Default to Custom
- your options here are:
  - POST TYPE (pages, posts or custom post types)
  - ORDER BY: new to old, old to new, A-Z, or Z-A
  - STICKY POSTS: Include, Exclude, or Only
  - POSTS PER PAGE
  - FILTERS: Taxonomies (cats or tags), Authors, Keyword, or Formats - keywords can have more than 1 word
- he has an option to change the number of columns but I don't have that. That may be because I have grid view but I think he does as well

> How do you make a blog post styicky in a wordpress block theme

...................................................................

## Media & Text Block block

- choose an image for the left > add a heading and a paragraph on the right then a buttons block below that - style the elements
- select the parent block > change to Wide Width
- you can choose to align the image to the top, middle or bottom

...................................................................

## Navigation block

- Navigation block > Page List block - select it and in the sidebar click edit to "detach" the page list so that you can manage the nav items individually
- when you select the navigation block you can click the 3 verrt dots for it in the right sidebar to 1) create a new menu, or 2) select another menu you created
- Navigation: Home Link block

. . . . . . . . . .

- Appearance > Editors > Navigation: you can quickly see and tweak all your menus
- You can make simple edits directly - click on the three vertical dots next to the menu item’s name, you can rename, duplicate, and delete the item as required - or Edit
- If opened in the editing mode, you can make certain changes without distractions
- You can add new pages or other menu items when you click on the plus icon. You will notice that the Navigation block is locked in this area.
- If you want to style your navigation menu, you must open a template or the template part it is part of

> _Very important tip_: to add the Homepage link, add the `Home Link` block. This means your home navigation menu will go to the home page display you set

. . . . . . . . . .

Simplify your navigation menu

- select header > navigation block > settings icon > you will see that the hamburger menu is selected by default for mobile

. . . . . . . . . .

- 📌 How to Create and Edit Menu Navigation: https://www.elegantthemes.com/blog/wordpress/wordpress-menu - classic themes is easy,

. . . . . . . . . .

- Navigation block > Page List block - select it and in the sidebar click edit to "detach" the page list so that you can manage the nav items individually
- when you select the navigation block you can click the 3 verrt dots for it in the right sidebar to 1) create a new menu, or 2) select another menu you created

. . . . . . . . . .

- in the Navigation block is a Page List block - select it and in the sidebar click edit to "detach" the page list so that you can manage the nav items individually
- when you select the navigation block you can click the 3 verrt dots for it in the right sidebar to 1) create a new menu, or 2) select another menu you created
  - click the gear icon to choose the hamburger icon
- Site Logo block

. . . . . . . . . .

- go into a template - list view and header > click on the nav block >
- my Pages template has:

```
header
  group
    group
      row
        site title
        row
          navigation
```

- when she clicks on the nav block she has a popup that has a button labeled "Select menu" and another "Start empty" - I don't have that
- inside you could have a block named Page List - if you get that select the PAge List block > edit > convert and then you will see t he blocks for each page on your site
- for a nested menu I created a Custom link, named it PAges and nested 2 pagews under it and gave it a link of `#` - it opens on Hover which I don't like

> How to create different menus in a wordpress block theme

- she used `+` and searched for "front" - selected Front PAge then hit Enter which crreated a custom link block and you should be able to search for another page

Sub-navigation:

- select a link in your nav > and she gets a floating toolbar to add an item to that menu item but I don't have that
- it looks like that creates a "Block pattern" block but that doesn't appear to be a thing anymore
- oh, there is a block called Submenu

To add a category into your menu:

- go to your categoties list > select one and click View > copy the url > paste it in

Search - the search block fucking sucks

Name your navigation:

- select the Navigation block > select the gear icon > click on Advanced > scroll down to Menu name > give it a name

> How to style the search block in a wordpress block theme

- submenu may be a block and you may be able to set it to open on click as opposed to hover

...................................................................

## Grid block

-
