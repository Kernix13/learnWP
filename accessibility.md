# Designing for accessibility

> https://wordpress.tv/2022/12/20/designing-for-accessibility/

- 1 video, 43 mins

Typography

1. simplify body fonts - no italic serifs
2. constring paragraph length/width for readability - `60-80` chars
3. use large body copy - `18px` or higher, meta should be 14 or 16px
4. line height - reduce headings, min for body text `1.3`
5. don't EVER justify your text - don't center more than 3 lines
6. minimize the use of uppercase text - don't make headlines all caps - use CSS because some screen readers treat them as acronyms - for things like categories, adding letter-spacing helps readability when they are all caps

Links

1. don't rely on color only for links - use underline and/or an icon
2. make links easily distinguishable - underline and bold is better in paragraph text with an icon when opening in a new tab
3. don't bold on hover
4. maintain target size minimums - add padding to make a bigger target
5. make focus states obvious - one method is reversing or a contrasting outline
6. don't override the cursors

Forms

1. placeholder text should not replace labels - make sure contrast is high between placeholder text and input value
2. explanatory labels provide more context - `Public Username` or `Company/Campus Email`
3. Be clear with required fields - `(required)` or `*`
4. use expanded content for further conteext - `i` in a circle tooltip that a user can click for an explanation
5. placeholder text = informative - `(###) ###-####` instead of `Phone number`

Color and contrast

1. always meet AA level and AAA when needed

- checkout pinetools.com/darken-color to darken your brand colors to meet compliance - they also have lighten-color
- sometimes you may have to tweak the brand colors
- check out the info on colorandcontrast.com

2. dark/light mode user settings

- `@media (prefers-color-scheme: dark)` - load additional styles
- `@media (prefers-contrast: more)` - similarly with their settings for high contrast mode

Content

1. provide skip to nav or skip to main content links
2. simplify and keep your paragraph lengths to a minimum
3. don't use complex words
4. maintain a consistent nav
5. ensure all necessary info is visible/accessible
6. always use clear headings in the proper order

Alt Text Tips

1. always give images alt text that are a part of the content
2. don't put alt text on images that aren't necesary for information - decorative stuff like BG images
3. make sure your alt text and copy complient each other rather than duplicate each other

Video and Audio tips

1. always include transcripts and subtitles
2. include audio descriptors on your videos - like a voiceover to describe what someone in the video is doing
3. bonus for ASL (American Sign Language) included in your video
4. do not auto-play

- check out more info at rootedinrights.org/accessthat

> Keep it gender neutral - no John or Jane, use Jayden - fuck you

Motion

- cognitive impairments: brain injuries and ...

1. `@media (prefers-reduced-motion: reduce)` - to target animations and transitions

Dyslexia

1. OpenDyslexic.org - they have a font that helps ???

Handoff/Annotations

1. annotate your design files for developers - ???

Create an accessibility checklist - a11yproject.com/checklist

> EXCELLENT VIDEO
