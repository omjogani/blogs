---
title: HTML Handbook
date: 2024-01-16 10:00:00 -500
categories: [webdevelopment, handbook]
tags: [html, webdevelopment, handbook]
---

# HTML Cheatsheet

## History behind `index` file
Generally, We name our HTML file as `index.html` that is because earlier [Apache2](https://httpd.apache.org/) was used everywhere which will server the HTML pages.

Apache2 render the HTML file named `index.html` by default. From then we started using `index.html` and there was also `default.html` but it's not used nowadays. 

For writing HTML code faster we can use [Emmet](https://emmet.io/). VSCODE and other famous IDE gives it by default.

## Core Structure of HTML
All the tags in HTML are case insensitive. So, `<html>` and `<HTML>` are same. 
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    
</body>
</html>
```
**`<!DOCTYPE html>`** : It tells the browser that this document file is `html` file.

**`<html lang="en">`** : While HTML grown world wide we use `lang` to tell browser that it's written in English or any other language.

There are two child in `<html>` tag. 
1. `<head>`
2. `<body>`

**`<meta>`** : These tags are the information which we don't want to display we it should be known to Browser or Server. like we want to add support for emojis we can add `UTF-16` in charset, or zoom level when page loads in different devices like tablet, laptop, smartphone etc.

Best resource for meta tags - [Meta tags and Attributes that Google Supports](https://developers.google.com/search/docs/crawling-indexing/special-tags)

---

```html
<h1 title="main heading">Heading</h1>
```
In above code, entire line is called `element`, Where `h1` is tag & `title` is attribute.

---

## HTML Tags
### Heading & Paragraphs
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <title>Heading & Paragraphs</title>
</head>
<body>
    <h1>Heading One</h1>
    <h2>Heading Two</h2>
    <h3>Heading Three</h3>
    <h4>Heading Four</h4>
    <h5>Heading Five</h5>
    <h6>Heading Six</h6>

    <hr>
    <p>This is the paragraph text.
    <br>
    Content of the paragraph text.</p>

    <pre>
        line 1
        line 2

        line 3
        line 4
    </pre>
</body>
</html>
```

**[`<h1> to <h6>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/Heading_Elements)** : These are heading tag which are used to define headings in our HTML Document.

**[`<p>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/p)** : Paragraph tag is used to define normal text as paragraph in our HTML Document.

**[`<br>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/br)** : Used for line break. Content will be in new line after `<br>` tag.

**[`<hr>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/hr)** : Horizontal Line to separate the content.

**[`<pre>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/pre)** : Used to represents preformatted text which is to be presented exactly as written in the HTML Document.

## Formatting Style & Global Attributes
### Commenting
- Single line Comment
```html
<!-- <h1> Commented Text </h1> -->
```

- Multiline Comment
    
    ```html
    <!-- <h1>Commented Text</h1>
    <h1>Commented Text 2</h1>
    <h1>Commented Text 3</h1> -->
    ```

### Bold Text
```html
<p> This is <b> just bold </b> Text. </p>
<p> This is <strong> important </strong> Text.</p>
```

This is **just bold** Text. \
This is **important** Text.

---

**[`<b>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/b)** : Use `<b>` tag just to bold the content when content is not that important.

**[`<strong>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/strong)** : When Content is important (Strong Importance) and we want to bold we will use `<strong>` tag.

---

### Italicize Text

```html
<p> This is <i> Italic </i> Text. </p>
<p> This is <em> Emphasis </em> Text. </p>
```  

This is *Italic* Text. \
This is *Emphasis* Text.

---

**[`<i>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/i)** : Use `<i>` tag to Italicize the Text.

**[`<em>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/em)** : Use `<em>` tag to Italicize the Text.

---

### Subscript & Superscript
```html
<p>
    Water: H<sub>2</sub>O also known as "Water"
</p>

<p>
  <var>a<sup>2</sup></var> + <var>b<sup>2</sup></var> = <var>c<sup>2</sup></var>
</p>
```
Water: H<sub>2</sub>O also known as "Water" \
a<sup>2</sup> + b<sup>2</sup> = c<sup>2</sup>

---

**[`<sub>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/sub)**: Used to specifies inline text which should be displayed as subscript for solely typographical reasons

**[`<sup>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/sup)**: Used to specifies inline text which is to be displayed as superscript for solely typographical reasons

---

### Del, Small & Mark Tags
```html
<p>
    This is <del>deleted</del> Text.
</p>

<p>
    <small>This is smaller content...</small>
</p>

<p>
    This is <mark>highlighted</mark> Text.
</p>
```
This is <del>deleted</del> Text. \
<small>This is smaller content...</small> \
This is <mark>highlighted</mark> Text. 

---

**[`<del>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/del)** : Used to represents a range of text that has been deleted from a document.

**[`<small>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/small)** : Used to represents smaller content, generally used for copyright etc.

**[`<mark>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/mark)** : Used to mark or highlight the text in HTML Document.

---

### Quote Tags
```html
<q cite="Reference Link / Person">
    Talk is cheap, show me your code!
</q>

<blockquote cite="Reference Link / Person">
    Coding like poetry should be short and concise!
</blockquote>
```
<q>Talk is cheap, show me you code!</q>
<blockquote>Coding like poetry should be short and concise!</blockquote>

---

**[`<p>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/q)** : Used to indicate the Text as Quote with cite.

**[`<blockquote>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/blockquote)** : Used to indicate the Text as Quote with Block & cite.

---

### Abbreviation Tag
```html
<p>
    <abbr>HTML</abbr> is cool markup language!
</p>
```

**[`<abbr>`]()** : Used to indicate part of text as abbreviation text to basically display the context of the text.

---

### Link (Anchor) Tag
```html
<a href="https://omjogani.github.com/blogs/">My Blogs</a>
```

**[`<a>`]()** : Used to provide link in HTML Document. It has attribute called `target` which essentially define where to display linked URL. Earlier we were using `frame` and `frameset` where `_parent` and `_top` was useful but nowadays we make use of `_self` which is default and `_blank` to open link in new page.

We can also define the ID of the element in `href` to quickly navigate to that HTML Tag.

---

### Image Tag
```html
<img src="https://picsum.photos/200/300" alt="Random Image">
```

**[`<img>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/img)** : Used to display image. It has `alt` attribute which is used to tell user context behind the user when Image is not loaded by any reason.

There are 2 additional attributes of image called `height` and `width`. Used to represent the height and width of image.

```html
<picture>
    <source media="(min-width: 460px)" srcset="https://picsum.photos/200/300?grayscale">
    <source media="(min-width: 650px)" srcset="https://picsum.photos/200/300?blur=2">
    <img src="https://picsum.photos/200/300" alt="Random Image">
</picture>
```

**[`<picture>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/picture)** : It contains zero or more `<source>` tags as children.

**[`<source>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/source)** : Used to define one or more media resources for pictures, audio, video etc. Say, if we want to load different images as per the device like for mobile device we want to load low quality image and for desktop we want to load high quality image. We can do that using `source` tag and `media` attribute.

### Map Tag
```html
<img src="./image.png" alt="Random Image">

<map name="image-map">
    <area onclick="func()" target="" alt="" title="" href="...link..." coords="961,537,131" shape="circle">
</map>
```

**[`<map>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/map)** : Used to define certain section of Image and on click of that image we can call different action like we can navigate to any link or run function of JavaScript.

---

## Colors in HTML
### Hexadecimal Color Format
RR - Red (00 - FF) \
GG - Green (00 - FF) \
BB - Blue (00 - FF)

```html
<h1 style="color: #87CEEB;">Sky Blue Text</h1>
```

### HSL Color Format
H - Hue (0 - 360) \
S - Saturation (0% - 100%) \
L - Lightness (0% - 100%) 

```html
<h1 style="color: hsl(197, 71%, 73%);">Sky Blue Text</h1>
```

### RGB Color Format
R - Red (0 - 255) \
G - Green (0 - 255) \
B - Blue (0 - 255) 

Hence 256 x 256 x 256 = 16777216 Colors possible.
```html
<h1 style="color: rgb(137, 207, 235);">Sky Blue Text</h1>
```

Additionally we can add `A` as opacity in RGB then it would be RGBA.

```html
<h1 style="color: rgba(137, 207, 235, .5);">Sky Blue Text with Half Opacity</h1>
```
---

## Styling in HTML
### Inline CSS
We provide css styling in HTML tag it self with `style` attribute.

```html
<h1 style="color: #87CEEB;">Example of Inline CSS</h1>
```
It has highest priority of applying css. Weather you mentioned CSS `color` property in Internal or External CSS. It will get overridden for this h1 with Inline CSS.

### Internal CSS
We provide styling of HTML tags in `<style> ... </style>` in `<head>` section.
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <title>Internal CSS</title>
    <!-- Internal CSS -->
    <style>
        h1 {
            color: #87CEEB;
        }
    </style>
</head>
<body>
    <h1>Sky Blue Text</h1>
</body>
</html>
```

### External CSS
When we have lots of styling code and we want to keep it separate in a CSS file. We can use External CSS.

We basically link external CSS file to our HTML code such that it can be applied to our HTML Tags.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <title>External CSS</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <h1>Sky Blue Text</h1>
</body>
</html>
```

```css
/* style.css */
h1 {
    color: #87CEEB;
}
```

>If you have both Internal and External CSS in your HTML then order of placing the CSS will be matter. If last CSS have property defined in first CSS then it will get overridden by last CSS.