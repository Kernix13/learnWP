# Layout composition

## Designing with the Group block

> https://learn.wordpress.org/lesson/designing-with-the-group-block/

The Group block is a container that allows you to bundle multiple blocks together. This feature helps you organize your content and apply styles to multiple elements at once

When the Group block is created you will find different variations to choose from, namely group, row, stack and grid

### Customizing

Once you’ve added a Group block you can start filling it with content

Another option is to select all the blocks you want to group in the List View. Then you can use the block toolbar to group them or click on the three vertical dots and then select Group

You can start styling and customizing this section or group

To keep your design organized you can also rename your Group block. Click on the three vertical dots in the List View, select Rename and then add a descriptive name

### Inner blocks use content width

One thing you will notice when you add a Group block and nest other blocks within it and change the background color is that **Inner blocks use content width is enabled by default**

That means blocks inside a group inherit the width defined by your theme. So even if you change the alignment of the Group block to wide width...The inner blocks remain at a standard width typically centered but if you disable Inner blocks use content width the inner blocks will expand to full the width of the group offering more flexibility in design

### Sticky header

the Group block can be made sticky - This is especially helpful for example when you want to make a header stick

Two things to remember though is to firstly change the background color of the Group block so that it is not transparent - if you don’t change the background color the text you scroll over will be visible

And the second is to return to settings and deselect Inner blocks use content width

### Responsiveness

Lastly it is also important to note that the Group block is responsive by default and when we preview it on mobile we will see it automatically adjusts its layout

.....................................................................

## Designing with Row and Stack blocks

> https://learn.wordpress.org/lesson/designing-with-row-and-stack-blocks-copy/

Using the Group block is one of the cornerstones of mastering the block editor. When you select a Group block, you have the variations of the Group block. The standard Group block, which gathers blocks in a container, the Row block, which arranges blocks horizontally, the Stack block, which arranges blocks vertically, and the Grid block, which arranges blocks in a grid

### Using the Row block

...the power of the Row block - justification ...Change vertical alignment

### Building a header

the Row block works very effectively for headers...

### Using the Stack block

...stacking all content in a column in a Stack block - but not a button

> The next crucial step is to change the minimum height of the stack block to 100%

...Change vertical alignment in your block toolbar and then select Space between

.....................................................................

## Designing with the Columns block

> https://learn.wordpress.org/lesson/designing-with-the-columns-block-copy/

utilize the Columns block to create different designs

The Columns block is a container block that can be used to create various custom layouts. The Columns block allows you to insert text, media, and other types of content into up to six columns

### Adding and customizing a Columns block

You can choose the number and the size of the columns you want to start with

### Block Toolbar

A parent-child relationship exists between the main Columns block and the individual columns that form part of the parent block

- When you click on the alignment icon, you can change the alignment of your block to wide-width or full-width
- you can also duplicate columns to save you a lot of time and effort
- You can use the arrows to move the column to a new position or use List View to drag and drop a column where you want

### Sidebar Settings

If you wanted to add another column, you could merely click on the Inserter between two columns or select the parent block and open your sidebar settings. Then, below Columns, you have the option to increase or decrease the number of columns. Below that, we see the option to deselect or select Stack on Mobile

- In Styles, we will see that the Columns block also allows us to change the colors of both the parent block or individual columns.
- You even have the option to change the size of your Columns block
- Below Dimensions, you can adjust the padding or the space around the content of the block, you can add margin, or modify the space between columns
- You can add a border and a radius to our Columns block
- you also have the option to add a drop shadow
- you can add a Cover block to each column for a nice effect

### Transforming other blocks into a Columns block

Another great feature is that you can transform other blocks into a Columns block and even a Columns block into a Group block

.....................................................................

## Dimensions: Padding, margin, and block spacing

> https://learn.wordpress.org/lesson/dimensions-padding-margin-and-block-spacing/

dimension settings, namely padding, margin, and block spacing

One of the key features of the Block Editor is the ability to customize the dimensions of your blocks. These tools are crucial for creating visually appealing and well-structured layouts

### Accessing settings

- select the relevant block, click on Settings, at the top right, and then select Styles
- below dimensions, you will be able to change padding, margin, and block spacing
- If some of the dimension settings are not visible, click on the three vertical dots and then enable them

### Definition

- padding is the space inside a block between its content and border
- Margin is the space outside the block, separating it from other sections or elements
- thirdly, block spacing controls the gap between nested blocks within a container block, like columns or groups

### Padding

Below padding, you will see a slider or visual representation of the block with padding controls.

- You can set the padding for the horizontal and vertical sides separately
- You can also set a custom size by entering a custom value
- You can use different units like pixels, percentages, or relative units
- Click on Unlink sides to adjust padding for each side individually

### Margin

...works exactly the same way as padding

- You can use the slider to add space above or below the block.
- Or you can set a custom size
- You can even set negative margins, but this is an advanced setting
- When you click on the Unlink sides, you can set horizontal and vertical margins separately

### Block spacing

block spacing is used to create space between nested blocks within a container block - if you set a wider block spacing on a Group block or a Columns block, blocks inside are spaced apart accordingly

### Style Book

you can set default padding, margin and block spacing values for different block types in the Style Book

you can also update the padding and block spacing for the main content area of your site below layout
