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

