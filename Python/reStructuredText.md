# reStructuredText

reStructuredText is an official markup language for Python docs and PEPs, which has suffix `.rst`

## Syntax
### Paragraphs
* Chunks of text separated by one or more blank lines
* All lines of the same paragraph must be in the same level of indentation

### Inline markup
* italics: one asterisk `*text*`
* boldface: two asterisks `**text**`
* code samples: backquotes `` `text` ``

### Lists
* `#` sign can be used for autonumbered list
```
* This is a bulleted list.
* It has two items, the second
  item uses two lines.

1. This is a numbered list.
2. It has two items too.

#. This is a numbered list.
#. It has two items too.
```

### Headers
```
Section header
==============

Subsection header
-----------------
```

### Links
```
Download `Python <https://python.org>`_ now.

# or
Download `Python`_ now, because `Python`_ is a popular programming language

.. _Python: https://python.org
```

### Images
```
.. image:: /path/to/image.jpg
```

### Code blocks
```
::

    from datetime import datetime
    print(f"{datetime.now():%Y-%m-%d}")
```

### Tables

```
==========  ======  =======
Fruit       Color   Price
==========  ======  =======
Banana      Yellow  40$/kg
Gala Apple  Red     70$/kg
Lime        Green   57$/kg
==========  ======  =======
```

### Table of Contents
```
.. contents::
```

### Cross-referencing
```
# installation.rst
.. _install-guide:

Installation Guide
==================

1. Create and activate a virtual env
2. ``pip install`` it

# index.rst
For details on how to install, please read :ref:`install-guide`.
```

## Sphinx
A tool to generate HTMLs from reStructuredText

## Reference
* [PEP 287 -- reStructuredText Docstring Format | Python.org](https://www.python.org/dev/peps/pep-0287/)
* [reStructuredText Primer — Sphinx documentation](https://www.sphinx-doc.org/en/master/usage/restructuredtext/basics.html)
