---
title: "Style Test"
excerpt: ""
---
[block:api-header]
{
  "type": "basic",
  "title": "Basic header"
}
[/block]
Lorem ipsum dolor sit amet, consectetur adipiscing elit
[block:api-header]
{
  "type": "get",
  "title": "Get"
}
[/block]
Lorem ipsum dolor sit amet, consectetur adipiscing elit
[block:api-header]
{
  "type": "post",
  "title": "Post"
}
[/block]
Lorem ipsum dolor sit amet, consectetur adipiscing elit
[block:api-header]
{
  "type": "put",
  "title": "Put"
}
[/block]
Lorem ipsum dolor sit amet, consectetur adipiscing elit
[block:api-header]
{
  "type": "patch",
  "title": "Patch"
}
[/block]
Lorem ipsum dolor sit amet, consectetur adipiscing elit
[block:api-header]
{
  "type": "options",
  "title": "Options"
}
[/block]
Lorem ipsum dolor sit amet, consectetur adipiscing elit
[block:api-header]
{
  "type": "delete",
  "title": "Delete"
}
[/block]
Lorem ipsum dolor sit amet, consectetur adipiscing elit
[block:api-header]
{
  "type": "fn",
  "title": "Function"
}
[/block]
Lorem ipsum dolor sit amet, consectetur adipiscing elit
[block:api-header]
{
  "type": "link",
  "title": "Link"
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "This is text",
      "language": "text"
    },
    {
      "code": "This is asp",
      "language": "asp"
    },
    {
      "code": "This is CoffeeScript",
      "language": "coffeescript"
    },
    {
      "code": "This is HTML",
      "language": "html"
    },
    {
      "code": "This is XML",
      "language": "xml"
    }
  ]
}
[/block]

[block:callout]
{
  "type": "info",
  "title": "Callout",
  "body": "Callout copy"
}
[/block]

[block:callout]
{
  "type": "warning",
  "title": "Callout",
  "body": "Callout copy"
}
[/block]

[block:callout]
{
  "type": "danger",
  "title": "Callout",
  "body": "Callout copy"
}
[/block]

[block:callout]
{
  "type": "success",
  "title": "Callout",
  "body": "Callout copy"
}
[/block]

[block:parameters]
{
  "data": {
    "0-0": "Copy",
    "0-1": "Copy",
    "0-2": "Copy",
    "0-3": "Copy",
    "h-4": "test",
    "h-2": "Heading",
    "h-1": "Heading",
    "h-0": "Heading",
    "h-3": "Heading",
    "2-1": "Copy",
    "1-3": "Copy"
  },
  "cols": 3,
  "rows": 3
}
[/block]

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/41847a7-maxresdefault.jpg",
        "maxresdefault.jpg",
        1600,
        1200,
        "#70543c"
      ],
      "sizing": "smart",
      "caption": "Smart fit"
    }
  ]
}
[/block]

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/7e5bcd6-maxresdefault.jpg",
        "maxresdefault.jpg",
        1600,
        1200,
        "#70543c"
      ],
      "sizing": "full",
      "caption": "100% width"
    }
  ]
}
[/block]

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/4cd020d-maxresdefault.jpg",
        "maxresdefault.jpg",
        1600,
        1200,
        "#70543c"
      ],
      "sizing": "80",
      "caption": "80% width"
    }
  ]
}
[/block]

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/321b61c-maxresdefault.jpg",
        "maxresdefault.jpg",
        1600,
        1200,
        "#70543c"
      ],
      "border": true,
      "caption": "Bordered"
    }
  ]
}
[/block]
## Strong and Emphasize

**strong** or __strong__ ( Cmd + B )

*emphasize* or _emphasize_ ( Cmd + I )

**Sometimes I want a lot of text to be bold.
Like, seriously, a _LOT_ of text**

## Blockquotes

> Right angle brackets &gt; are used for block quotes.

## Links and Email

An email <example@example.com> link.

Simple inline link <http://chenluois.com>, another inline link [Smaller](http://smallerapp.com), one more inline link with title [Resize](http://resizesafari.com "a Safari extension").

A [reference style][id] link. Input id, then anywhere in the doc, define the link with corresponding id:

[id]: http://brandwatch.com "Brandwatch website"

Titles ( or called tool tips ) in the links are optional.

## Images

An inline image ![Smaller icon](http://smallerapp.com/favicon.ico "Title here"), title is optional.

A ![Resize icon][2] reference style image.

[2]: http://resizesafari.com/favicon.ico "Title"

##  Ordered Lists

Ordered lists are created using "1." + Space:

1. Ordered list item
2. Ordered list item
3. Ordered list item

## Unordered Lists

Unordered list are created using "*" + Space:

* Unordered list item
* Unordered list item
* Unordered list item

Or using "-" + Space:

- Unordered list item
- Unordered list item
- Unordered list item

## Hard Linebreak

End a line with two or more spaces will create a hard linebreak, called `<br />` in HTML. ( Control + Return )
Above line ended with 2 spaces.

## Horizontal Rules

Three or more asterisks or dashes:

***

---

- - - -

## Headers


# This is H1
## This is H2
### This is H3
#### This is H4
##### This is H5
###### This is H6

## Footnotes

Footnotes work mostly like reference-style links. A footnote is made of two things: a marker in the text that will become a superscript number; a footnote definition that will be placed in a list of footnotes at the end of the document. A footnote looks like this:

That's some text with a footnote.[^1]

[^1]: And that's the footnote.

## Strikethrough

Wrap with 2 tilde characters:

~~Strikethrough~~

## Fenced Code Blocks

Start with a line containing 3 or more backticks, and ends with the first line with the same number of backticks:

```
Fenced code blocks are like Stardard Markdown’s regular code
blocks, except that they’re not indented and instead rely on
a start and end fence lines to delimit the code block.
```

## Tables

A simple table looks like this:

First Header | Second Header | Third Header
------------ | ------------- | ------------
Content Cell | Content Cell  | Content Cell
Content Cell | Content Cell  | Content Cell

Specify alignement for each column by adding colons to separator lines:

First Header | Second Header | Third Header
:----------- | :-----------: | -----------:
Left         | Center        | Right
Left         | Center        | Right