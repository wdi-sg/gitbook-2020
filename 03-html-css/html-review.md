# HTML

### Objectives

* Discuss the purpose of HTML
* Construct a HTML page with common elements and attributes

### What is HTML

HTML stands for **H**yper**T**ext **M**arkup **L**anguage

HTML describes the semantic formatting of a document.

When we give an HTML file to the browser, the browser interprets it and displays the document.

_A website is an HTML document, but an HTML document is not always a website_

### Where does this all happen?

When we write our document we can refer to other resources within the same filesystem.

### What happens when I load a webpage?

In the 1st unit of WDI we won't be too concerned with the ways an HTML file can get _to_ the browser.

When we use the _open in browser_ menu option, it runs the file in your default browser directly from within your computer.

Your file is stored on the hard disk memory of your computer, and is put into the RAM memory of your computer to be run. The browser turns this code into a page that you see inside it's window.

Within this process of displaying the page many more smaller things are happening.

Some questions to ask about this process might be:

* what does it mean that the browser is reading my code?
* how do the images I specify appear on the page?
* how does my HTML know about my CSS?
* what happens when I click on a link?
* where are the images I see on the page stored?

## Going through a HTML document

### HTML elements

HTML elements consist of a start tag, an end tag, and content in-between. Example:

```markup
<h1>Here is some text</h1>
```

Elements can be nested.

```markup
<div>
  <h1>Here is <strong>some</strong> text</h1>
</div>
```

Elements can also contain attributes, which are key-value pairs.

```markup
<div data-attr="5"></div>

<img src="imageurl.png">
```

Note that the last element is an example that does **not** need a closing element. These are known as **void elements**.

Some of the more important attributes are `class` and `id`, which we will see later in CSS. Just know that class names can be used in more than one element, but ids must be unique. See below.

```markup
<div class="general-container"></div>
<div class="general-container"></div>
<span class="general-container"></span>

<div id="specific-container"></div>
```

### What is `<!DOCTYPE html>`?

This statement specifies the markup rules for the page. There are other DOCTYPEs that define [other markup standards](http://www.w3.org/QA/2002/04/valid-dtd-list.html), like XHTML.

You won't need to worry about the other document types for now, so make sure to always use `<!DOCTYPE html>` at the top of a HTML document.

### The `<html></html>` tags

These tags tell the browser we're beginning a HTML document. Put everything inside these tags.

### The `<head>` tags

The `<head></head>` tags is where hidden information about the document goes. This includes metadata, the title of the webpage \(which appears in the browser\), links to CSS and possibly JavaScript files. The head goes at the top of the page, and is declared only once.

### Meta Tags

Metadata is data \(information\) about data. The  tag provides metadata about the HTML document. Metadata will not be visible on the webpage, but will be machine parsable. Meta elements are typically used to specify page description, keywords, author of the document, last modified, and other metadata. The metadata can be used by browsers \(how to display content or reload the page\), search engines \(keywords\), or other web services.

Some common meta tags you will see are charset, content, author, and description \(for SEO\).

### The `<body>` tags

The `<body></body>` tags denote the content of the document. This content is rendered and displayed in the browser.

## HTML document tags:

Some elements are default formatted by the browser, like as in a document.

Even without CSS, the browser still knows that these tags can be formatted in a ceratin way.

### Images and Links

See the Pen [Images and Links](http://codepen.io/bhague1281/pen/NxOdgv/) by Brian Hague \([@bhague1281](http://codepen.io/bhague1281)\) on [CodePen](http://codepen.io).

 \#\#\# Lists

See the Pen [Lists](http://codepen.io/bhague1281/pen/XXxpMx/) by Brian Hague \([@bhague1281](http://codepen.io/bhague1281)\) on [CodePen](http://codepen.io).

### Tables

See the Pen [Tables](http://codepen.io/bhague1281/pen/jWeyma/) by Brian Hague \([@bhague1281](http://codepen.io/bhague1281)\) on [CodePen](http://codepen.io).

 Before CSS became mainstream, websites were designed using tables. Although they are much less frequently used, building tables is still a very useful skill to know. The tags for tables are such: \* \`

\` - create a table \* \`

|  |
| :--- |


\` - create a table row \* \`

| \` - create a table heading \* \` |
| :--- |


| \` - create a table cell \* \`\` - create the body of the table \(newer tag\) \* \`\` - create the head of the table \(newer tag\). No matter where this is located, whatever is in it will be the first row \* \`\` - create the foot of the table \(newer tag\). No matter where this is located, whatever is in it will be the last row \#\#\# Other document tags: \`\`\` |
| :--- |


 \`\`\` \#\# HTML document structure tags: \#\#\# Divs + Spans HTML provides for us two 'empty' containers to store whatever content we want. One is a div \(block element\) and the other is a span \(inline element\) When we see layout in CSS we will be using these containers to define the different parts of our document.

See the Pen [Divs vs Spans](http://codepen.io/bhague1281/pen/qbJREg/) by Brian Hague \([@bhague1281](http://codepen.io/bhague1281)\) on [CodePen](http://codepen.io).

## Forms

Forms provide the ability for the user to make inputs. Right now they have no where to go.

We don't use forms in unit 1, but we will use form _elements_ - inputs. Later on we will see how to use them in a client side app.

In unit 2 we will see the way they were meant to be used.

One of the most common ways to send data to a server is by using a form. A form has two essential attributes, action and method.

* **Action** - This specifies a route where you are going to. For example an action of '/test' will take you to the /test route \(something you have probably configured in your server side code\)
* **Method** - The HTTP Verb that this form will be using \(HTML only knows GET and POST, but there are ways to override this default which we will see when we use Node and Rails. The default method is GET so if you are making a GET request you can leave this empty.

#### Labels

Labels are text you place before/after inputs to tell the user what the input is for. The for attribute is for screen readers and if the ID of the input matches the ID of the for attribute then you can click on the label and have it automatically focus/check the input.

#### Input Types

By default, input elements will allow users to type in text. There's also a plethora of different input types, specified by a `type` attribute. Take a look at the Codepen below for some examples.

See the Pen [Form Elements](http://codepen.io/bhague1281/pen/xZygWo/) by Brian Hague \([@bhague1281](http://codepen.io/bhague1281)\) on [CodePen](http://codepen.io).

Documentation on input types: [https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input)

#### DOM \(Document Object Model\)

One last point we shall mention briefly is the DOM or Document Object Model. The DOM is technically an API for representing and interacting with elements in HTML. The easiest way to think about this is that HTML is the language we used to describe what we want, the DOM is the object created to then represents that in memory, in a tree like structure. Later we'll talk about manipulating the DOM and what we mean is changing the structure of the pages we defined in out HTML.

![](https://www.w3.org/TR/DOM-Level-2-Core/images/table.gif)

