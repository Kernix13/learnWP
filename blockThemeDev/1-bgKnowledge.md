# Building Background Knowledge: The Theme Creation Process

> most of these lessons are excellent

## Different types of themes: Overview

> https://learn.wordpress.org/lesson/different-types-of-themes-overview/

- Classic Editor vs Block Editor
- Block themes: These new themes place the power of design customization into the hands of users
- Classic themes primarily used the Customizer

### Classic Themes

- to make big layout changes, adjust colors, move a logo - users needed to have a strong grasp of CSS
- Easy to use right out of the box - Ideal for new WordPress users
- Write/edit/publish posts or pages without thinking about complex customizations

### New Block Themes

- Block themes, however, primarily use the Site Editor
- The Site Editor allows users to move big elements of their site, change colors with the click of a button, and customize their theme exactly to their choosing
- There are many more options and flexibility to block themes
- Create custom blog posts and also pages using drag and drop builder
- pages where a user can add almost anything
- Design a website from top to bottom without needing any coding knowledge

### other kinds of themes

- “Hybrid” and “Classic” themes
- Hybrid Themes: A theme that contains a mix of both classic theme elements and block theme elements. These themes borrow a few elements from either the classic or block theme. PHP coding is required to build a hybrid theme
- Universal Themes: These themes can work entirely either like a classic theme or like a block theme—they are built using both the Site Editor and PHP code
  - Historically, these themes were used to bridge the gap between what the block editor (at the time) couldn’t do, and what the customizer could do

...............................................................

## How themes are designed?

> https://learn.wordpress.org/lesson/how-themes-are-designed/

- many designers turn to other tools, such as Figma or Photoshop, to begin drafting what their WordPress theme will look like - to visualize the end result before they passed along their ideas to developers

...............................................................

## How classic and block themes are developed from designs

> https://learn.wordpress.org/lesson/how-classic-and-block-themes-are-developed/

### How Themes Are Developed

From Design Image to Hard Code:

- first analyze all parts of the theme to decide what to code first
- Where do the titles, logos, and theme navigation go
- What colors are important
- How is each page element and page template itself to be laid out

### Block Themes: Skip the Code

Design in the Site Editor:

- A theme developer is able to jump straight into the Site Editor and start placing different theme blocks where they go into different template parts
- With block themes, it’s possible to get very close to a designer’s existing layout using only the Site Editor–no coding required

### Use or Distribute The Theme

> skip

- it will then go through an open-source review process, which look for things like security vulnerabilities–which were far more common in classic themes than they are now with block themes
- by designing your custom block theme using the Site Editor, your theme will automatically be very secure

### What You Will Design & Develop

While master theme designers often start with a **_block theme template_**, we will build our custom theme template by template in order to deeply understand what each file does, why it’s necessary, and how to begin building your custom block theme

You will design directly in the Site Editor, using your global styles to set colors, padding, and your site’s overall layout. You will learn the very basics of theme.json code

### Use Custom Block Themes or Distributing Block Themes For Others To Use

requirements needed to distribute your new custom theme

Advanced Developer Resources: (Optional)

1. Tool: Figma (Developer Handbook)
2. Block Theme Setup (For Existing Intermediate and Advanced Developers)
3. Developing Classic Themes Information (Advanced Developer)

...............................................................

## What a new theme developer needs to know: Anatomy of a block theme

Anatomy of a block theme:

- they are using 2022 which I think is a hybrid theme
- functions.php, readme.txt, screenshot.png, style.css, theme.json
- /assets: fonts, images, etc
- /inc: skip
- /parts: header, footer, sidebar html files
- /templates: html files for the common templates like 404.html
