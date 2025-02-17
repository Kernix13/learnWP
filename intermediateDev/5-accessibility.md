# Accessibility

## Best practices for developing an accessible theme

> https://learn.wordpress.org/lesson/best-practices-for-developing-an-accessible-theme/

...digital accessibility is a broad term that means ensuring that as many people as possible can use the web...accessibility guidelines guarantee a better browsing experience for everyone

The easiest way to deliver accessible themes, plugins, or sites is to think about it from the outset. Include it in the planning phase - learn about the fundamentals of accessible HTML and how to apply them to your WordPress themes

### The fundamentals

A valid HTML page—marked properly with landmarks, headings, text, buttons, links, forms, etc

The problems typically come later as you add styles, scripts, or media assets. As a developer of modern WordPress themes, these are exactly the technologies you'll work with—React-based Blocks, PHP-injected Patterns, and CSS compiled from theme.json

> The key is to be mindful of accessibility while you code and design.

### Semantic HTML

Instead of wrapping everything with a <div> element, take advantage of the semantically meaningful elements of HTML

### Landmarks

Landmarks are a way to define the structure of a page. They help screen readers navigate the content more easily

> If you're designing / building your theme inside the Site Editor, **it's also possible to set landmarks there**

- Landmarks: semantic html elements

To define `Group`, `Row`, and `Stack` blocks as content sectioning elements, select the block, open the block Settings and expand the Advanced section

Scroll down and set the HTML ELEMENT to header, main, section, article, aside, or footer, according to the block's functionality and position

### Headings

When adding headings to templates, always use headings in the right order, starting from H2 and continuing in a descending sequence up to H6

In the Site editor, click on **Document Overview** > **Outline** to check whether you skipped a level or if everything is correctly set

### Buttons versus links

When designing user actions, consider the following as it relates to using buttons or links:

- If you want visitors to perform an action use a button element.
- When you want them to navigate to another page, use the anchor element (`<a>`).
- _If the link should resemble a button, say, for a call-to-action on a landing page, then style it with CSS_.

### Forms

If you're designing any forms in your theme, follow these guidelines:

- Always wrap the form in a `form` element.
- On `input` fields, always set the appropriate type and matching attributes. For example, defining an input type of tel, will display a numeric keypad on mobile devices.

```html
<input type="tel" name="phone" id="phone" required />
<input type="password" autocomplete="current-password" />
```

- Don't rely on placeholder text to indicate to the user what the input field is for, always provide accessible labels `<label>`
- Use the `<search>` element for any search forms - it's only purpose is to wrap a form with label, input.search, button.search
- When designing login forms, you can use the `autocomplete` attribute to help password managers fill out the form
- By default, most browsers will display a focus ring on elements if the element has focus. If you want to change the display of these focus rings, use the `:focus-visible` pseudo-class, and don't remove focus rings entirely.

### Colours

- Be sure to create an accessible colour palette with sufficient contrast
- When editing templates, WordPress alerts you when the text and background colour combination you set fails to do that
- Don't use colour alone to convey information. Links, for example, should be marked by more than colour, and the same goes for _focus states_. When in doubt, look at the default HTML link and focus styles and follow those

### Typography

> **Limit the content width to between 50 and 70 characters; the character or ch unit is perfect for that**

- Set proper font sizes using relative units like `rem`, try to avoid using `px`
- Limit the content width to between 50 and 70 characters; the character or ch unit is perfect for that
- Use adequate line spacing based on the font size

### Respect user preferences

- A cornerstone of responsive design, media queries help create a better user experience
- Some media query types like `prefers-color-scheme` or `prefers-reduced-motion` are explicitly accessibility-driven,
- but there's also the `pointer`, `hover`, or `scripting` that adjusts components' behaviour to the user's device

### The ARIA workaround

ARIA is short for Accessible Rich Internet Applications framework, and it is often cited as a quick way to make HTML content more accessible to screen readers

However, the most important rule of ARIA is that you should only use it when you absolutely need to. Ideally, you should always use HTML features to provide the semantics required by screen readers to tell users what is going on

Misused `aria` attributes make things less accessible, so avoid them unless you don't have control over the HTML or need to handle dynamically generated content

...visit MDN's [WAI-ARIA basics](https://developer.mozilla.org/en-US/docs/Learn/Accessibility/WAI-ARIA_basics) section

To learn more, visit the W3C Web Accessibility Initiative's (WAI) [Tutorials](https://www.w3.org/WAI/tutorials/) section

. . . . . . .

## Tools for testing theme accessibility

> https://learn.wordpress.org/lesson/tools-for-testing-theme-accessibility/

### Test, fix, repeat

- Testing early and repeatedly helps you detect potential violations in new components or pages before they launch

### Automated tests

- Chromium-based browsers come with Google Lighthouse built into DevTools.
  Lighthouse is also available as a standalone webpage and an NPM package.
- Firefox has the [Accessibility Inspector](https://firefox-source-docs.mozilla.org/devtools-user/accessibility_inspector/index.html#accessibility-inspector), and Safari offers Audit.
- WebAIM's Wave is a browser extension available for Firefox and Chromium-based browsers.
- Deque Systems' axe is a [set of accessibility testing tools](https://www.deque.com/axe/): a browser extension, Figma plugin, VS Code extension, code linter, and more.
- [Pa11y](https://pa11y.org/) is a free, open-source alternative for developers.

### WordPress plugins

plugins you can install to test for accessibility issues on a WordPress site - Each has a slightly different approach to accessibility checks:

1. [Sa11y](https://wordpress.org/plugins/sa11y/)
2. [WP Tota11y](https://wordpress.org/plugins/wp-tota11y/)
3. [Editoria11y](https://wordpress.org/plugins/editoria11y-accessibility-checker/)

Finally, there's [Accessibility Checker](https://wordpress.org/plugins/accessibility-checker/) that works in the Post Editor and the front end, surfacing errors, and providing detailed explanations (including the relevant code snippet) and potential fixes. As robust as it is, Accessibility Checker currently only works reliably on production sites

### Manual testing

1. Try navigating your theme with a keyboard—no mouse. Use the `tab` key to navigate between links, buttons, and form fields. Press `enter` or `space` to activate these interactive elements.
2. Change the _color scheme_ (via the browser's DevTools) to ensure things look well in dark mode or high contrast mode.
3. Finally, navigate around the site using your device's built-in _voice control_ feature or a dedicated _screen reader_ software. This is the preferred—sometimes only—way, as many visually impaired people use the web.
