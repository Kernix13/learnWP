# Introduction to designing with WordPress

> https://learn.wordpress.org/course/beginner-wordpress-designer/

WordPress allows you to leverage a variety of blocks when crafting innovative designs and expressing your creative skills

## WordPress showcase for designers

### WordPress tools

- Block Editor
- Pattern libraries
- Site Editor: lets you design every aspect of your site with blocks
- Global styles: help you to define consistent design across the site
- Fonts easily upload web fonts from Google Fonts or other source
- Style Book: lets you control the appearance of individual blocks

### Plugins and blocks

- use plugins to add a form to your site, advanced galleries or even sliders
- You can also create a unique design such as this using the Grid block
- The Cover block also allows one to display images with overlay text, commonly used for headers, banners, or section dividers
- The Query Loop block enables powerful content segmentation and sophisticated layouts

....................................................................

## Using the Style Book as a design guide

> https://learn.wordpress.org/lesson/using-the-style-book-as-a-design-guide/

### Style Book

The WordPress Style Book is a powerful tool that bridges the gap between traditional design practices and WordPress’s block based editing system. Think of it as your digital style guide showcasing how different blocks or components of your site will look and interact with each other

- Appearance > Editor > Styles > click eye icon then pencil icon
- That will show the Style Book on the left and the theme's Global Style settings on the right
- The Style Book is intimately connected to WordPress’s global styles feature
- it’s important to understand that the Style Book is a different way to preview the design decisions you’ll make in Global Styles
- When you update Global Styles you can view the changes either directly in the Style Book allowing you to focus on specific blocks or you can view the changes you make in Global Styles directly in the Site Editor, allowing you to see the changes you make in a template or a page
- the Style Book can be helpful if you don’t have much content on your site

### How the Style Book is organized

The Style Book is organized into several tabs

When you design you can use the Style Book to visualize your design choices across different elements, ensure consistency in your design system, experiment with different style variations and identify areas that need refinement

when you select the Style Book you can test out and preview the style variations that come with your theme

....................................................................

## Overview of WordPress block theme terms and hierarchy

> https://learn.wordpress.org/lesson/overview-of-wordpress-block-theme-terms-and-hierarchy/

- Pages: you may easily construct different layouts for each page as needed
- Posts: are dynamic content typically used for blogs or news updates

### Block theme hierarchy

Examining each level of the hierarchy, from the smallest to the largest, will give us a clear picture of how these components fit together to create a complete WordPress site. The block theme hierarchy from smallest to largest is:

- Blocks
- Block Patterns
- Template Parts
- Templates
- Theme

Blocks:

- the foundational element, the fundamental building units in WordPress block themes
- They represent individual content elements

Block Patterns:

- pre-designed arrangements of blocks that can be easily inserted and customized
- They are reusable designs that you can add to your pages or posts

Template Parts:

- editable, reusable sections of a website and are primarily used for structural elements with specific semantic meanings

Templates:

- define the overall structure of different page and post types on your WordPress site
- They are fully customizable using blocks and incorporate template parts
- determine the layout for specific content types like pages, single posts, archives, etc

Theme:

- a block theme is the overarching design framework for your entire WordPress site
- It defines the overall look, feel, and behavior of your website.
- Themes include all templates, template parts, block patterns, and Styles

### Flexibility

Block themes’ hierarchy offers flexibility and makes customizing the design easier. You can create and customize at any level through the Site Editor, from individual blocks to entire themes

....................................................................

## Designing with a block-first mindset

> https://learn.wordpress.org/lesson/designing-with-a-block-first-mindset/

### Modularity

Block-first design means breaking down your website into smaller, reusable components that can be mixed and matched to create diverse layouts

Think of blocks as LEGO pieces. Just as you can build complex structures with simple LEGO bricks you can create intricate website designs using fundamental blocks

### Blocks

- Blocks allow you to create complex designs without writing a single line of code
- Blocks connect to a file called theme.json which sets default styles
- If you are in the Site Editor and select Global Styles, you can tweak these defaults using visual controls, ensuring design consistency while maintaining flexibility

### Reusable components

A block pattern or reusable component is a collection of blocks you can insert into your site and customize with your own content

### Block composition principles

Start small and begin with the essentials in your Style Book. Begin with foundational elements like text, images, and buttons

These form the foundation of your design system. Then start building up. Combine these basic elements into more complex blocks

Try creating a media and text pattern, and then save it as a non-synced pattern and then design the layout

Remember to think responsively: Design your blocks to work well on all screen sizes - Columns block that allows you to stack on mobile

```
Group
  Columns
    Column
      Paragraph
      Heading
      Paragraph
      Buttons
    Column
      Image
```
