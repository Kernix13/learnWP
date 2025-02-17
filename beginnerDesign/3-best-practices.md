# Web design best practices

## Why design in the Site Editor and use it for prototyping

> https://learn.wordpress.org/lesson/why-design-in-the-site-editor-and-use-it-for-prototyping/

### Advantages of using the Site Editor

- When you master blocks, you can easily manage everything on your site since it’s entirely built with them. Blocks replace all previous methods, including shortcodes, widgets, embeds, and custom HTML, simplifying your content creation process.
- By designing directly within WordPress, you streamline the journey from concept to implementation, facilitating easier updates and maintenance. This approach also reduces traditional handover challenges between designers and developers.
- The Editor provides real-time, interactive previews of your designs, enabling immediate testing and refinement.
- Moreover, by utilizing WordPress’s native tools for design, you ensure compatibility with the platform and reduce the learning curve typically associated with external design software.

### Designing in the Site Editor

- open Site Editor > select Zoom Out option > update the typography of text then headings, update color palette, adjust buttons by selecting the Buttons block, modify header and footer, ...

**NOTE**: Go into a template > select the header > in the right styls panel you will have multiple headers variations to choose from - repeat for footer

### Web-related design principles

- key web design principles, aka Gestalt Principles, namely Proximity, Similarity, Continuity and Closure

1. Proximity: Group related elements together to create a sense of organization and structure. In the example at the top, you will notice that not enough spacing has been utilized to group related parts together.
2. Similarity: Use consistent styles for related elements to indicate their connection. In this example, the similarity between categories help users quickly find what they need. Let’s look at similarity from a different angle. In the example below, the call-to-action buttons use different colors to show different actions, but their similar size and shape make them feel connected. By using consistent styling such as color, shape or size for similar functions or content types across your website, you help users quickly recognize and understand the purpose of different elements.
3. Continuity: Align elements to create a natural flow for the eye to follow.
4. Closure: Allow users’ minds to complete shapes or patterns, reducing visual clutter. This principle is often used in logo design and icons to create simple yet memorable visuals. If we look at the WWF logo, you’ll notice we fill in the gaps to complete the image of the panda. By mastering the Site Editor and understanding these fundamental web design principles, you’re well equipped to create functional websites right within WordPress.

.................................................................

## Web accessibility guidelines to create inclusive websites

> https://learn.wordpress.org/lesson/web-accessibility-guidelines-to-create-inclusive-websites/

Web accessibility is designing websites that work for everyone, including those with visual, auditory, motor, or cognitive impairments...boosting your site’s SEO and overall usability... plus a legal requirement in some countries

### Key principles

1. COLOR CONTRAST: WebAIM Contrast Checker
2. TYPOGRAPHY: easy to read, at least 16 pixels as your base size, minimum line height of 1.5 for optimal readability, avoid all caps and small caps, and reserve underlining exclusively for links, fully justified text should not be used
3. STRUCTURE & LAYOUT: You want a clear, consistent layout with a logical reading order, proper heading hierarchy,
4. NAVIGATION: easy to use with both a mouse and a keyboard
5. FORMS: Label everything, all form elements should be operable on the keyboard
6. BUTTONS: should also have meaningful text that describes their action
7. ALT TEXT: always include descriptive alt text for images; video captions and audio transcripts should always be provided

### WordPress-specific tips

- THEMES: look for one labeled Accessibility Ready
- PLUGINS: Certain types of WordPress plugins can cause accessibility issues | Additionally you can use tools like WebAIMS WAVE to inspect the plugin for accessibility issues. There are also some great accessibility plugins out there that offer tools to check and improve the accessibility of your content

Always complete an accessibility audit as you are designing your website - designing for accessibility is an ongoing process

.................................................................

## Testing your content for accessibility

> https://learn.wordpress.org/lesson/testing-your-content-for-accessibility-copy/

...many technical accessibility problems are usually easy to detect and fix using automated tools. Proper heading levels, color contrast, meaningful alt text, link text, and so on...these are the most common accessibility failures on the web

### Built-in helpers in WordPress

WordPress includes two built-in accessibility helpers in the Editor

1. Semantic Structure: use Outline to check whether your headings are ordered correctly - WordPress marks the wrong heading levels in light orange
2. Color Contrast: If you select a text and background color combination that fails to provide sufficient contrast, WordPress will alert you

### Plugins

1. WP Tota11y: checks common accessibility compliance - incorrect heading levels, color contrast, poor link text, missing labels in form elements, and missing alt text in images
2. Sa11y: provides a comprehensive set of checks on the front end. You can toggle a few extra checks such as readability, advanced links, color contrast and form labels under Settings - also color filters to test how your page would look when viewed by people with several types of colorblindness - While the errors are clearly marked, the description is more high level and the fix isn’t as straightforward as it could be
3. Editoria11y: focuses on content and structure - No design elements like color contrast will be checked - it displays alerts on the front end and the Editor, notifying you about the document outline, heading levels, link texts and targets, also known as Open in a new tab and missing alt text in images - describes the failures in plain language, suggests fixes, and allows users to hide or dismiss the alert when it’s irrelevant
4. Accessibility Checker: adds a new section to the post or page editor window and a hovering button to the front end. It displays a summary of the errors, detailed explanations, including the relevant code snippet, potential fixes, and an option to ignore individual alerts

### OS apps and browser extensions

1. try browsing your website with a keyboard - Use the tab key to navigate between links, buttons, and form fields, and press enter or space to activate these interactive elements of the page - Make note of non-functional elements and missing visual indicators that need fixing
2. change the device’s color scheme to ensure things look and work well in dark or high contrast mode
