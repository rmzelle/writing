Citation Style Language 1.0 - Primer
====================================

.. contents:: **Table of Contents**
   :depth: 4

Preface
~~~~~~~

This primer is an introduction to the Citation Style Language (CSL), an open XML-based language to describe the formatting of citations and bibliographies. If you want to learn how to edit CSL styles, or use CSL styles in your own software, this primer is meant for you. For a more comprehensive and in-depth overview of CSL, see the `CSL 1.0 Specification`_.

.. _CSL 1.0 Specification: http://citationstyles.org/downloads/specification.html

What is CSL?
~~~~~~~~~~~~

If you ever had to write a scholarly manuscript, you probably were required to reference other works. And for good reason, as proper referencing plays an important role in scholarly communication by, for example, providing attribution and linking together published research. However, manually formatting references can be boring and time-consuming. The burden is even higher when you have to deal with multiple journals or publishers that each have their own particular citation style format.

Luckily, reference management software can lighten the load. Programs like Zotero, Mendeley, and Papers not only make it easier to manage your research library (and PDFs), but also provide features to automatically generate and update citations and bibliographies in text documents. But to format references in the desired style, these programs need descriptions of each style in a computer-readable format. The Citation Style Language is such a format.

Citation Formats
^^^^^^^^^^^^^^^^

Before we focus on the technical aspects of CSL, let's first take a look at the different types of citation formats that CSL supports (and doesn't support).

In-text Styles
''''''''''''''

Citation styles can be divided in two main categories. The first category consists of **"in-text"** styles, where a *citation* in the sentence directly points to one or multiple entries in the *bibliography*. Within this category, CSL distinguishes between **"author-date"**, **"author"**, **"numeric"** and **"label"** styles.

A citation can point to multiple bibliographic entries. In CSL, each individual pointer is called a *cite*. For example, the citation (Doe et al. 2002, Smith 1997) contains one cite to a 2002 publication by Doe et al. ("Doe et al. 2002"), and one to a 1997 publication by Smith ("Smith 1997"). In the context of CSL, a *bibliographic entry* is sometimes also referred to as a *reference*.

"author-date" & "author" Styles
+++++++++++++++++++++++++++++++

Cites of "author-date" styles show author names and the date of publication, e.g. (van der Klei et al. 1991; Zwart et al. 1983), whereas cites of "author" styles only show the names, e.g. (Gidijala et al.). Bibliographic entries are typically sorted alphabetically by author.

*Bibliography*

Gidijala L, Bovenberg RA, Klaassen P, van der Klei IJ, Veenhuis M, et al. (2008) Production of functionally active *Penicillium chrysogenum* isopenicillin N synthase in the yeast *Hansenula polymorpha*. BMC Biotechnol 8: 29.

van der Klei IJ, Harder W, Veenhuis M (1991) Methanol metabolism in a peroxisome-deficient mutant of *Hansenula polymorpha*: a physiological study. Arch Microbiol 156: 15-23.
   
Zwart KB, Veenhuis M, Harder W (1983) Significance of yeast peroxisomes in the metabolism of choline and ethanolamine. Antonie van Leeuwenhoek 49: 369-385.

"numeric" Styles
++++++++++++++++

Cites consist of numbers, e.g. [1,2] and [3]. Bibliographic entries are typically sorted either alphabetically by author, or in the order in which the entries are first cited.

*Bibliography*

1. Gidijala L, Bovenberg RA, Klaassen P, van der Klei IJ, Veenhuis M, et al. (2008) Production of functionally active *Penicillium chrysogenum* isopenicillin N synthase in the yeast *Hansenula polymorpha*. BMC Biotechnol 8: 29.
   
2. Zwart KB, Veenhuis M, Harder W (1983) Significance of yeast peroxisomes in the metabolism of choline and ethanolamine. Antonie van Leeuwenhoek 49: 369-385.
   
3. van der Klei IJ, Harder W, Veenhuis M (1991) Methanol metabolism in a peroxisome-deficient mutant of *Hansenula polymorpha*: a physiological study. Arch Microbiol 156: 15-23.

"numeric" Compound Styles (unsupported)
***************************************

A variation of the "numeric" in-text style format is the compound style format, popular in the field of chemistry. With these styles, bibliographic entries may consist of one [1] or multiple references [2]. Single items in preceding bibliographic entries can also be cited, e.g. [2b]. This format is not (yet) supported by CSL.

*Bibliography*

1. Gidijala L, et al. (2008) BMC Biotechnol 8: 29.
   
2. \a) Zwart KB, et al. (1983) Antonie van Leeuwenhoek 49: 369-385, b) van der Klei IJ, et al. (1991) Arch Microbiol 156: 15-23.

"label" Styles
++++++++++++++

Cites consist of short keys, e.g. [GBKv2008] and [ZwVH1983; vaHV1991]. These keys are also included in the bibliographic entries.

*Bibliography*

[GBKv2008] Gidijala L, Bovenberg RA, Klaassen P, van der Klei IJ, Veenhuis M, et al. (2008) Production of functionally active *Penicillium chrysogenum* isopenicillin N synthase in the yeast *Hansenula polymorpha*. BMC Biotechnol 8: 29.
   
[vaHV1991] van der Klei IJ, Harder W, Veenhuis M (1991) Methanol metabolism in a peroxisome-deficient mutant of *Hansenula polymorpha*: a physiological study. Arch Microbiol 156: 15-23.

[ZwVH1983] Zwart KB, Veenhuis M, Harder W (1983) Significance of yeast peroxisomes in the metabolism of choline and ethanolamine. Antonie van Leeuwenhoek 49: 369-385.

Note Styles
'''''''''''

The second category of citation styles consists of **"note"** styles. With these a *marker* (a number or a symbol) is added to the sentence when works are cited, e.g. [*]_ and [*]_. The marker points to a footnote or endnote. CSL styles do not control which number formats or symbols are used for the markers. In contrast to in-text citations, footnotes and endnotes typically contain all information required to identify the cited work(s). Some "note" styles include a bibliography to give an overview of all cited works, and to describe the works in more detail.

    .. [*] 'Voyage to St. Kilda' (3rd edit. 1753), p. 37.
    .. [*] Sir J. E. Tennent, 'Ceylon,' vol. ii. 1859, p. 107.

CSL Infrastructure
^^^^^^^^^^^^^^^^^^

To generate citations and bibliographies in any of the formats described above, a CSL-based reference manager needs:

- a **CSL style** describing a citation style.

- **item metadata**, which are the bibliographic details of the cited works. E.g., the item type (book), title ("Moby-Dick"), author (Herman Melville), etc.

- **CSL locale files** and the desired **locale**. CSL has support for style localization. For example, a single CSL style can generate both "Doe and Smith. May 5, 1993." (US English) and "Doe und Smith. 5. Mai 1993." (German). The locale files provide default localization data (e.g., translations of common terms like "in" and "and", date formats, and grammar preferences) for a wide selection of languages. Some CSL styles are set to a particular language, while others will use the provided **locale**. 

- **citing details**. Many reference managers have word processor plugins so you can easily insert citations and bibliographies into manuscripts. Here, the item metadata is supplemented by details on how the items are cited in the manuscript (e.g., the order in which the items are cited, which items are cited together in a single citation, etc.).

- a **CSL processor**, which processes all the pieces listed above and generates the formatted citations and bibliographies. Zotero and Mendeley both use the open source JavaScript `citeproc-js <https://bitbucket.org/fbennett/citeproc-js/wiki/Home>`_ CSL processor.

|csl-infrastructure|

.. |csl-infrastructure| image:: https://github.com/rmzelle/writing/raw/master/csl-infrastructure.png

XML Basics
~~~~~~~~~~

For those new to XML (or HTML), this section gives a short overview of what you need to know about XML in order to edit CSL styles and locale files. If anything here is unclear, just check one of the many XML tutorials online.

Let's take a look at the following piece of CSL XML:

.. sourcecode:: xml

    <?xml version="1.0" encoding="utf-8"?>
    <style xmlns="http://purl.org/net/xbiblio/csl" class="in-text" version="1.0">
      <info>
        <title>Academic Medicine</title>
        <id>http://www.zotero.org/styles/academic-medicine</id>
        <link href="http://www.zotero.org/styles/vancouver" rel="independent-parent"/>
        <category citation-format="numeric"/>
        <category field="medicine"/>
        <issn>1040-2446</issn>
        <updated>2012-01-11T19:01:02+00:00</updated>
        <rights>This work is licensed under a Creative Commons Attribution-ShareAlike 3.0 License: http://creativecommons.org/licenses/by-sa/3.0/</rights>
      </info>
    </style>

There are several concepts and terms you need to be familiar with. These are:

- **XML Declaration**. The first line of any style or locale file should always
  be the XML declaration. It almost all cases, this will be ``<?xml version="1.0"
  encoding="utf-8"?>``. This line designates the document as XML, and specifies
  the XML version ("1.0") and character encoding ("utf-8") used.

- **Elements and Hierarchy**. The basic building blocks of XML documents are
  elements, which are hierarchically structured. Each XML document contains a
  single root element (for CSL styles this is ``<style/>``). If an element
  contains other elements, the parent element is split into a start tag
  (``<style>``) and an end tag (``</style>``). In our example, the ``<style/>``
  element has one child element, ``<info/>``. This element has several children
  of its own, which are grandchildren of the grandparent ``<style/>`` element.
  Element tags are always wrapped in less-than ("<") and greater-than (">")
  characters (e.g., ``<style>``). For an empty-element tag, ">" is preceded by a
  forward-slash (e.g., ``<category/>``), while for end tags "<" is followed by a
  forward-slash (e.g.,``</style>``). Child elements are typically indented with spaces or tabs to show the different hierarchical levels.

- **Attributes and Element Content**. There are two ways to add additional
  information to elements. First, XML elements can carry one or more attributes
  (the order of attributes on an element is arbitrary). Every attribute needs a
  value. For example, the ``<style/>`` element carries a ``version`` attribute, set to a
  value of "1.0", indicating that the style is written in CSL 1.0. Secondly, elements can
  store non-element content between start and end tags, e.g. the content of the
  ``<id/>`` element is "http://www.zotero.org/styles/academic-medicine".

- **Namespace**. To indicate that all the elements in the style or locale file are part of CSL, the root element should always carry the ``xmlns`` attribute, set to the CSL XML namespace URI, "http://purl.org/net/xbiblio/csl". In the rest of this primer we will use the namespace prefix "cs:" when referring to CSL elements (e.g., ``cs:style`` instead of ``<style/>``).

- **Escaping**. Some characters have to be substituted when used for purposes
  other than for defining the XML structure (e.g., when used in attribute values
  or non-element content), or, in the case of the ampersand ("&"), for
  substitution itself. Escape sequences are "&lt;" for "<", "&gt;" for ">",
  "&amp;" for "&", "&apos;" for ', and "&quot;" for ". For example, the link
  "http://domain.com/?tag=a&id=4" should be escaped as ``<link
  href="http://domain.com/?tag=a&amp;id=4"/>``.

- **Well-formedness and Schema Validity**. Unlike HTML, XML does not allow for
  any markup errors. Any error, like forgetting an end tag, having more than one
  root element, or incorrect escaping will break the XML document and prevent it
  from being processed. XML documents that follow the XML specification and
  are error-free are "well-formed". For well-formed styles and locale
  files there is a second level of testing, involving the CSL schema. This
  schema describes which CSL elements and attributes are allowed and how they must
  be used. When a style or locale file is tested against the CSL schema rules (this process
  is called "validation") and passes, the file is valid CSL. Only well-formed
  and valid CSL files can be expected to work properly.

Tools for Editing
~~~~~~~~~~~~~~~~~

Text/XML editors
^^^^^^^^^^^^^^^^

CSL styles and locales can be edited with any plain text editor. However, editors with XML support can make editing easier with features like automatic indenting, tag closing, and real-time testing
for well-formedness and schema validation. Some suitable editors include `Notepad++ <http://notepad-plus-plus.org/>`_ for Windows, `TextWrangler <http://www.barebones.com/products/textwrangler/>`_ for OS X, and the cross-platform
`<oXygen/> XML Editor <http://www.oxygenxml.com/>`_ (commercial), `GNU Emacs <http://www.gnu.org/software/emacs/>`_ (in `nXML mode <http://www.thaiopensource.com/nxml-mode/>`_) and 
`jEdit <http://www.jedit.org/>`_ (with its `XML plugin <jEdit>`_).

XML Validators
^^^^^^^^^^^^^^

Instead of validating directly in the text editor, you can also use a dedicated
XML validator. See `<Validation>`_ for more information.

Zotero's Reference Test and Preview panes
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The `Zotero <http://www.zotero.org>`_ reference manager comes with two
CSL tools. After installing the Zotero for Firefox add-on, you
can access the `Zotero Preview pane <http://www.zotero.org/support/dev/citation_styles/preview_pane>`_ by entering
"chrome://zotero/content/tools/cslpreview.xul" in the Firefox address bar. The
Preview pane generates citations and bibliographies for all installed CSL
styles, using the items selected in your local Zotero library. The
`Zotero Reference Test pane <http://www.zotero.org/support/dev/citation_styles/reference_test_pane>`_, accessible via
"chrome://zotero/content/tools/csledit.xul", allows you to edit a style with
instant previewing, again using items from your Zotero library. Users of Zotero Standalone can access these tools through the Zotero preferences panel.

Citation Styles
~~~~~~~~~~~~~~~

We're now ready to see how CSL styles are actually written.

Basic Anatomy of a Style
^^^^^^^^^^^^^^^^^^^^^^^^

All CSL styles have the following basic structure:

.. sourcecode:: xml

    <?xml version="1.0" encoding="UTF-8"?>
    <style xmlns="http://purl.org/net/xbiblio/csl" version="1.0" class="in-text">
      <info/>
      <locale/>
      <macro/>
      <citation>
        <sort/>
        <layout/>
      </citation>
      <bibliography>
        <sort/>
        <layout/>
      </bibliography>
    </style>

As you can see, the ``cs:style`` root element has (up to) five different child elements. The function of each type of child element is described below. The ``cs:style`` element itself normally carries the ``xmlns`` attribute (set to the CSL namespace), the ``version`` attribute (specifying the CSL version, set to "1.0" for CSL 1.0 styles), and the ``class`` attribute (specifies whether the style type, "in-text" or "note").

Info
''''

``cs:info`` is always the first child element of the ``cs:style`` root element. It provides information about the CSL style (the style metadata), such as the style title, when the style was last updated, who wrote the style, etc.

Locales
'''''''

CSL styles can automatically localize terms, date formats, and punctuation. Default sets of localization data are stored in the `CSL locale files <https://github.com/citation-style-language/locales/wiki>`_. In some cases it is desirable to override (subsets of) the default localization data, and this can be done in styles by using one or more ``cs:locale`` elements.

Macros
''''''

Styles may contain one or more ``cs:macro`` elements. Each ``cs:macro`` element defines a macro, and each macro contains formatting instructions.

Macros have two main roles. First, they can hold formatting instructions that otherwise would be put into the ``cs:citation`` and ``cs:bibliography`` elements. Using macros in this way keeps the structure of these latter elements concise and easy to understand. Secondly, they can be used to define complex sorting rules, for cites in citations, and references in bibliographies.

Citation
''''''''

The ``cs:citation`` element describes how the in-text citations (for in-text styles) or footnotes/endnotes (for note styles) are formatted. The ``cs:sort`` child element of ``cs:citation`` can be used to specify how cites should be sorted within citations, while the ``cs:layout`` element is used to describe the format of cites and citations.

Bibliography
''''''''''''

The ``cs:bibliography`` element describes the formatting of the references in the bibliography, and functions very similar to the ``citation`` element. The ``cs:sort`` child element of ``cs:bibliography`` can be used to specify how bibliographic entries should be sorted, while the ``cs:layout`` element is used to describe the format of bibliographic entries.

Dependent Styles
''''''''''''''''

When multiple journals share the same citation style, you could create a collection of CSL styles that all have the exact same formatting instructions and which only differ in the contents of the ``cs:info`` element. But this approach has some drawbacks. For instance, if the citation style changes, you would have to update each CSL style. To make things simpler for these cases, CSL supports "dependent styles". In a dependent style, ``cs:style`` only includes the ``cs:info`` child element, which links to an independent style which contains a full set of formatting instructions to define the citation style format. E.g., dependent styles for the journals "Nature Biotechnology", "Nature Nanotechnology", etc. would all point to a single independent style, "Nature".

Dissecting a Dependent Style
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. sourcecode:: xml

    <?xml version="1.0" encoding="utf-8"?>
    <style xmlns="http://purl.org/net/xbiblio/csl" class="in-text" version="1.0">
      <info>
        <title>Academic Medicine</title>
        <id>http://www.zotero.org/styles/academic-medicine</id>
        <link href="http://www.zotero.org/styles/vancouver" rel="independent-parent"/>
        <category citation-format="numeric"/>
        <category field="medicine"/>
        <issn>1040-2446</issn>
        <updated>2012-01-11T19:01:02+00:00</updated>
        <rights>This work is licensed under a Creative Commons Attribution-Share Alike 3.0 License: http://creativecommons.org/licenses/by-sa/3.0/</rights>
      </info>
    </style>

Dependent styles are concise and the easiest to read. The CSL 1.0 style above is for the medical journal Academic Medicine (ISSN 1040-2446). It is available at http://www.zotero.org/styles/academic-medicine, available under a Creative Commons BY-SA license, and last updated on January 11th, 2012. When you use this style, the in-text numeric citation style described in the CSL style found at http://www.zotero.org/styles/vancouver will be used.

Dissecting an Independent Style
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Discuss, info section, give example of formatted citations, discuss cs:citation element (et-al-* attributes), cs:layout, delimiters/affixes, names, dates, terms/locales/redefining terms. give example of formatted bib, discuss cs:bibliography, sorting

Don't cover number, label right now.

Make style a bit more expansive with stuff from existing example primer, so journal papers are formatted halfway decent.