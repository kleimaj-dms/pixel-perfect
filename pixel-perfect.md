# Pixel Perfect Email Development
---

>Pixel perfect is the process of taking every element into consideration, down to the individual pixels.
>In front-end development terms, pixel perfection is when the coded product and the design file are unable to be told apart when side by side.

### To Acheive Pixel Perfection:
- Developers must review the design files with an eye for extreme detail.
- Establish a relationship with the designer.
- Use a style guide.
- Use [PerfectPixel Chrome Extension](https://chrome.google.com/webstore/detail/perfectpixel-by-welldonec/dkaagdgjmgdmbnecmcefdhjekcoceebi) (overlays design file over coded result)

### Reviewing Design Files:
Note font families and the variants. Observe margin and padding values that can be applied to the page/panel templates. When using style guides, the elements are componentized and ensure they are the same every time.

## How to make emails pixel perfect:

### Make it Modular
Emails are are developed in static tables (columns and rows), 
for this reason it will render well automatically across all email clients.
However, tables are not easily editable, they will require some tweaks, and can result in a "house of cards collapse"
A solution for this is to wrap all independent elements into its own table.

#### Spacers not Line Breakers
Pay attention to the text format (font size, line-height), as opposed to adding `<br>` tags everywhere.

#### Image Embedding
Wrap images within their own table. You can stack several images vertically and use display:block css to prevent gmail from adding gaps. Use JPG images for best quality, or PNG for opacity.

### Reset Styles and Client Bugs
1. ##### Paragraph Tags
    - `<p>` tags can be inserted when using wysiwyg editors (Sendy for example).
    - Various email clients handle treatment and spacing of p tags very differently.
    - Use regular line breaks, or double line breaks for new paragraphs in your copy.
    - To achieve exact spacing outside of blocks of copy, use an empty div with a font-size inline style.
2. ##### Padding, Margin, H-space
    - Similar to p tags, these are used to achieve horizontal spacing, around images aligned within a block of text.
    - Bake the padding into the image itself, or add a gutter cell (table)
3. ##### Line-height and Lists (Outlook)
    - Outlook cannot process unordered/ordered lists with line-height, defer to a table solution
4. ##### Multi name fonts with quotes (AOL)
    - AOL cannot process fonts like "Helvetica Nueue", multi name fonts with dashes instead of quotes, such as sans-serif to prevent aol's default serif font.
5. ##### Regular Heading Tags
    - It's best to use custom classes to style your headings (.h1, .h2, .h3) this can remove the need to trouble shoot all your different headings.
6. ##### Odd Widths
    - Keep all images, tables, and cells at even widths. This will help avoid the 1 pixel shifts across various email clients.

##### Reset Styles Cheatsheet
```css
/* Force Hotmail to display emails at full width. */
.ReadMsgBody {width: 100%;}
/* Forces Hotmail to dislay normal line spacing. */
.ExternalClass {width: 100%;}
.ExternalClass, .ExternalClass p, .ExternalClass span, .ExternalClass font, .ExternalClass td, .ExternalClass div {line-height:100%;}
/* Prevents auto resizing of text on mobile devices. */
body {-webkit-text-size-adjust:none; -ms-text-size-adjust:none;}
/* Addresses various layout issues */
body {margin:0; padding:0;}
table {border-spacing:0;}
table td {border-collapse:collapse;}
/* Removes Yahoo's special link styling. */
.yshortcuts a {border-bottom: none !important;}
/* Addresses Gmail image gaps and other image issues. */
img{border:none; outline:none; display:block;}
```
### Responsive Emails

#### Table Widths
Static emails typically have the width hard coded.
With responsive emails, we will replace that so there will be a CSS class with the width in the style.
```html
<table class="fullwidth">
```
```css
.fullwidth {width:600px;}
@media only screen and (max-width: 480px) {
.fullwidth {width:300px !important;}
}
```
Note the `!important` tag is required to take precedence over the inline styles. This is only applied to styles within `@media only` sections

#### Images
There are different ways to resize images responsively.
Do not use fixed width and height, use a css class like so:
```html
<img src="https://imagepath.com/image.jpg" class"fleximage"/>
```
```css
/* within the media only section of your css: */
.fleximage {width: 280px !important};
/* height does not need to be set, it’ll scale as evenly as possible. */
```

#### Font Styling
Do not use body copy under 16px. 
Headlines should be around 22px and up.

Example body css:
```css
.h1, .h1 a:link, .h1 a:visited {
color:#393c3d;
font-family:Helvetica, Arial, sans-serif;
line-height:100%;
font-size:32px;
font-weight:normal;
text-decoration:none;
}
.body{
color:#393c3d;
font-family:Helvetica, Arial, sans-serif;
font-size:12px;
line-height:150%;
}

.body a:link, .body a:visited{
color:#00b0ff;
text-decoration:none;
font-weight:normal;
}
@media only screen and (max-width: 480px) {
.h1, .h1 a:link, .h1 a:visited {font-size:22px !important;}
.body{font-size:16px !important;}
}
```

#### Spacing
Mobile emails may vary in space from the desktopversion. Use responsive spacing tables with css controlling the line-height.

```css
.spacer {line-height:30px;}
@media only screen and (max-width: 480px) {
.spacer {line-height:10px;}
}
```

## Resources
- https://www.mediacurrent.com/blog/pixel-perfection-front-end-development
- https://www.inboxgroup.com/coding-pixel-perfect-emails-part-1/#:~:text=One%20more%20quick%20tip%20on%20creating%20pixel%20perfect,give%20you%20the%20exact%20pixel%20size%20you%20set.
- https://blog.teamtreehouse.com/pixel-perfect-front-end-development-matters
- https://chrome.google.com/webstore/detail/perfectpixel-by-welldonec/dkaagdgjmgdmbnecmcefdhjekcoceebi