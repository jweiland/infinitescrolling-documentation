﻿====================================
Help writing reStructuredText
====================================

reStructuredText (frequently abbreviated as reST) is a lightweight markup language intended to be highly readable in source format. This chapter is a brief introduction to the syntax of reStructuredText, intended to provide authors with enough information to start writing their documentation. Some example below are taken from the `official documentation`_. More resources are to be found online:

* a `reminder`_ from the official web site
* a `documentation`_ from Sphinx_ (which is the documentation generator used for converting reST files into HTML and other formats)
* a `cheat sheet`_ to download
* our own `documentation in the TYPO3Wiki`_

.. _official documentation: http://docutils.sourceforge.net/docs/ref/rst/directives.html
.. _reminder: http://docutils.sourceforge.net/docs/user/rst/quickref.html
.. _documentation: http://sphinx.pocoo.org/rest.html
.. _Sphinx: http://sphinx.pocoo.org/
.. _cheat sheet: http://github.com/ralsina/rst-cheatsheet/raw/master/rst-cheatsheet.pdf
.. _documentation in the TYPO3Wiki: http://wiki.typo3.org/ReST_Syntax


ReST editor
-------------

Since reST is meant to be readable by "design", a basic editor is enough to start writing documentation. However, there are editors that are offering facilities such as syntax highlighting, conversion to HTML on the fly, ... Among them, it is worth to mention:

* PyCharm_ from JetBrains (commercial)
* An `online reST editor`_ (free)
* ... if you think you have spotted a gem that is worth being listed up, please report onto the `Mailing List`_ of the Documentation Team.

Besides that, refer to this reading_ to get a more in depth overview of the existing "players" in the market.

.. _PyCharm: http://www.jetbrains.com/pycharm/
.. _reading: http://stackoverflow.com/questions/2746692/restructuredtext-tool-support
.. _online reST editor: http://rst.ninjs.org/
.. _Mailing List: http://lists.typo3.org/cgi-bin/mailman/listinfo/typo3-project-documentation


Inline Markup
=============

Inside paragraphs and other bodies of text::

	you may additionally mark text for italics with *italics* or bold with **bold**.

	If you want something to appear as a fixed-space literal, use ``double back-quotes``.

Headings
=========

The titles of the whole document are defined as follows::

	==========
	heading 1
	==========

	heading 2
	==========

	heading 3
	---------

	heading 4
	~~~~~~~~~~~

	heading 5
	^^^^^^^^^


External Links
===============

There exist different methods for providing a link. The "alias" method is generally preferred for the sake of clarity. However, the target should be kept close to the reference to prevent them going out of sync::

	A text with a `hyperlink`_

	.. _hyperlink: http://typo3.org


Cross linking
===============

Cross linking can be achieved by the means of a plugin called Intersphinx_ which generates links across projects::

	intersphinx_mapping = {'tsref': ('http://docs.typo3.org/...', None)}

	This is a cross link to :ref:`stdWrap <tsref:stdWrap>`

@todo: enumerate the offical TYPO3 prefixes here once they are known...

.. _Intersphinx: http://sphinx.pocoo.org/latest/ext/intersphinx.html

List
=====

Lists of items come in three main flavours: enumerated, bulleted and definitions. In all list cases, you may have as many paragraphs, sublists, etc.

::

	* This is a bulleted list
		* Second level bullet
		* Some more bullet here
	* It has two items


	#. This is a numbered list
	#. It has two items too

Image
======

Whenever dealing with images, it is often recommended to use the `..figure:: directive`. A "figure" consists of image data, an optional caption (a single paragraph), and an optional legend (arbitrary body elements)::

	.. figure:: picture.png
		:scale: 50 %
		:alt: map to buried treasure

		This is the caption of the figure (a simple paragraph).

		The legend consists of all elements after the caption.  In this
		case, the legend consists of this paragraph and the following
		table:

Code
====

The "code" directive constructs a literal block. If the code language is specified, the content is parsed by the Pygments_ syntax highlighter.

::

	.. code-block:: php
		:linenos:

		/**
		 * returns an increased counter
		 */
		function inc(int $counter = -1) {
			return $counter +1;
		}

.. _Pygments: http://pygments.org/

TypoScript Reference
=====================

Defining TypoScript reference can be achieved by using the "container" directive::

	.. container:: table-row

		Property
			enableDisplayBigControlPanel

		Data type
			list of keywords

		Description
			Determines whether the checkbox “Extended view” in the list module is shown or hidden. If it is hidden, you can predefine it to be always activated or always deactivated.

		Default
			selectable

Admonitions
============

Admonitions are specially marked "topics" such as "warning", "important", "tip" or "note"::

	.. note:: This is a note admonition.

		These notes are similar to tips, but usually contain information you should pay attention to. It might be details about a step that a whole operation hinges on or it may highlight an essential sequence of tasks.

		- The note contains all indented body elements following.
		- It includes this bullet list.

	.. tip::

		Tips are bits of information that are good to know. They may offer shortcuts to save you time or even make your website better.

	.. warning::

		These notes draw your attention to things that can interrupt your service or website if not done correctly. Some actions can be difficult to undo.


Table
======

The "table" directive is used to create a titled table, to associate a title with a table::

	.. table:: Truth table for "not"

	=====  =====
	 A    not A
	=====  =====
	False  True
	True   False
	=====  =====


The "list-table" directive is used to create a table from data in a uniform two-level bullet list. "Uniform" means that each sublist (second-level list) must contain the same number of list items::

	.. list-table:: Frozen Delights!
		:widths: 15 10 30
		:header-rows: 1

		* - Treat
		 - Quantity
		 - Description
		* - Albatross
		 - 2.99
		 - On a stick!
		* - Crunchy Frog
		 - 1.49
		 - If we took the bones out, it wouldn't be
		   crunchy, now would it?
		* - Gannet Ripple
		 - 1.99
	    - On a stick!


Alternatively a grid table can be used. As tip, Emacs editor provides some facilities_ to edit grid table. A recommended tutorial can be found at http://www.emacswiki.org/emacs/TableMode. ::

	+------------+------------+-----------+
	| Header 1   | Header 2   | Header 3  |
	+============+============+===========+
	| body row 1 | column 2   | column 3  |
	+------------+------------+-----------+
	| body row 2 | Cells may span columns.|
	+------------+------------+-----------+
	| body row 3 | Cells may  | - Cells   |
	+------------+ span rows. | - contain |
	| body row 4 |            | - blocks. |
	+------------+------------+-----------+

.. _facilities: http://table.sourceforge.net/

Side bar
=========

A sidebar is typically offset by a border and "floats" to the side of the page; the document's main text may flow around::

	.. sidebar:: Here a side bar

		This box is going to be shifted to the right corner which can be useful to display pointers or other kind of side information.
