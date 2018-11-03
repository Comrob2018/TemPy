---
layout: default
title: TemPy Tags
permalink: /usage/tags/
---
## Tag Creation


Create DOM elements by instantiating tag classes. Those elements are nodes in the DOM tree and can be attached, detached, moved and composed together dynamically.

There are 2 other ways to create TemPy objects:

* using the `clone()` API
* adding, subtracting or multiplying TemPy objects

```python
page = Html()
div = Div()

new_page = page.clone()

new_page_2 = page + div
new_page_3 = new_page_2 - div
list_of_5_divs = div * 5
```

## TemPy Tags

TemPy provides a class for every HTML5 element defined in the [W3C reference](https://www.w3.org/wiki/HTML/Elements), those classes can be imported from the `tempy.tags` submodule.

Each Tempy Tag class is either a `tempy.elements.Tag` with a start tag and an end tag, that can contain something, or a `tempy.elements.VoidTag` that can not contain other things and is composed of a single html tag mark.

```python
from tempy.tags import Div, Br

Div.render()  # Subclass of tempy.elements.Tag
>>> <div></div>

Br.render()  # Subclass of tempy.elements.VoidTag
>>> <br/>
```

A few TemPy tags have custom behavior:

* the `tempy.tags.Comment` tag needs as first argument the comment string: `Comment('This is my comment')`
* the `tempy.tags.Doctype` tag needs as first parameter a doctype code (`Doctype('html_frameset')`) to choose between:
    * html
    * html_strict
    * html_transitional
    * html_frameset
    * xhtml_strict
    * xhtml_transitional
    * xhtml_frameset
    * xhtml_1_1_dtd
    * xhtml_basic_1_1
* the `tempy.tags.Html` tag accepts the keyword argument "doctype", so it adds a Doctype tag before himself (default is "HTML" doctype): `Html(doctype='html_strict')`
* a `tempy.tags.A` tag with nothing inside it will render himself with the href string inside it: `A(href='www.link.com').render() -> <a href="www.link.com">www.link.com</a>`
