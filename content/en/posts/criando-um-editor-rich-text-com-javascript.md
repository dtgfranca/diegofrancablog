---
  card_desc: "Building a text editor with JavaScript isn't as hard as some might think. Creating your own editor can give you much more freedom than relying on a third-party editor"
  card_image:
  card_title: Creating a rich text editor with JavaScript
  og_desc: "Building a text editor with JavaScript isn't as hard as some might think. Creating your own editor can give you much more freedom than relying on a third-party editor"
  og_image:
  og_image_alt:
  og_title: Creating a rich text editor with JavaScript
_edit_last: "1"
author: diego.tg.franca@gmail.com
  - uncategorized
date: "2023-05-05T12:37:01+00:00"
draft: "true"
fw:opt:ext:pb:page-builder:json: '[]'
  page-builder: {}
    builder_active: false
    json: '[]'
guid: http://diegofranca.dev/?p=375
parent_post_id: null
post_id: "375"
title: Creating a rich text editor with JavaScript
---
Building a text editor with JavaScript isn't as hard as some might think. Creating your own editor can give you much more freedom than relying on a third-party one.

In this tutorial, I'll build a very simple editor with only a few features: bold, italic, ordered list, and unordered list.

### Building the editor

The first step is to create the area where we'll type our text. For that we'll use a `div` and set the `contenteditable` attribute to `true`. If you're not familiar with this attribute, it makes any HTML element editable.

\[code\]

With the code above, the result is:

\[screenshot\]

### Building the toolbar

To build the toolbar we'll add the icons from https://fontawesome.com/ to our application. The result will look like this:

\[screenshot\]

The CSS code:

\[code\]

## Formatting

### Italic

### Bold

### List
