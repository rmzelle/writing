Primer
======

by Rintze M. Zelle, PhD

|CCBYSA|_

.. |CCBYSA| image:: http://i.creativecommons.org/l/by-sa/3.0/80x15.png
.. _CCBYSA: http://creativecommons.org/licenses/by-sa/3.0/

.. contents:: **Table of Contents**
   :depth: 4

Preface
~~~~~~~

This primer is an introduction to the `Citation Style Language`_ (CSL), an open XML-based language to describe the formatting of citations and bibliographies. For a more technical and in-depth description of CSL, see the `CSL Specification`_.

.. _Citation Style Language: http://citationstyles.org
.. _CSL Specification: http://citationstyles.org/downloads/specification.html

What is CSL?
~~~~~~~~~~~~

If you ever wrote a research paper, you probably included references to other works. Referencing is important in scholarly communication, as it provides attribution, and links together published research. However, manually formatting references can become very time-consuming, especially when you're dealing with multiple journals that each have their own citation style.

Luckily, reference management software can help out. Programs like Zotero, Mendeley, and Papers not only help you manage your research library, but can also automatically generate citations and bibliographies. But to format references in the desired style, these programs need descriptions of each citation style in a language the computer can understand. As you might have guessed, the Citation Style Language (CSL) is such a language.

Citation Formats
~~~~~~~~~~~~~~~~

There are hundreds, if not thousands of different citation styles in use around the world. Fortunately, most citation styles fall within a few basic categories. CSL distinguishes between the following types:

In-text Styles
^^^^^^^^^^^^^^

Citation styles can be divided in two main categories. The first category consists of **in-text** styles, where a *citation* in the sentence directly points to one or multiple entries in the *bibliography*. CSL subdivides this category in **author-date**, **author**, **numeric** and **label** styles.

Each citation points to one or more *bibliographic entries*. In CSL, each individual pointer is called a *cite*. For example, the citation "(Doe et al. 2002, Smith 1997)" contains two cites: one to a 2002 publication by Doe et al., and one to a 1997 publication by Smith. In the context of CSL, bibliographic entries are sometimes also called *references*.

"author-date" & "author" Styles
'''''''''''''''''''''''''''''''

Cites of **author-date** styles show author names and the date of publication, e.g. "(Van der Klei et al. 1991; Zwart et al. 1983)", whereas cites of **author** styles only show names, e.g. "(Gidijala et al.)". Bibliographic entries are typically sorted alphabetically by author.

Note that many style guides use the confusing term "Harvard" to refer to **author-date** formats, even though most of these styles have no connection to Harvard University. There is also no such thing as a single official "Harvard" style.

**Example Bibliography**

Gidijala L, Bovenberg RA, Klaassen P, van der Klei IJ, Veenhuis M, et al. (2008) Production of functionally active *Penicillium chrysogenum* isopenicillin N synthase in the yeast *Hansenula polymorpha*. BMC Biotechnol 8: 29.

van der Klei IJ, Harder W, Veenhuis M (1991) Methanol metabolism in a peroxisome-deficient mutant of *Hansenula polymorpha*: a physiological study. Arch Microbiol 156: 15-23.

Zwart KB, Veenhuis M, Harder W (1983) Significance of yeast peroxisomes in the metabolism of choline and ethanolamine. Antonie van Leeuwenhoek 49: 369-385.

"numeric" Styles
''''''''''''''''

Cites of **numeric** styles consist of numbers, e.g. "[1, 2]" and "[3]". Bibliographic entries are typically sorted either alphabetically by author, or put in the order by which they have been first cited.

**Example Bibliography**

1. Gidijala L, Bovenberg RA, Klaassen P, van der Klei IJ, Veenhuis M, et al. (2008) Production of functionally active *Penicillium chrysogenum* isopenicillin N synthase in the yeast *Hansenula polymorpha*. BMC Biotechnol 8: 29.

2. Zwart KB, Veenhuis M, Harder W (1983) Significance of yeast peroxisomes in the metabolism of choline and ethanolamine. Antonie van Leeuwenhoek 49: 369-385.

3. van der Klei IJ, Harder W, Veenhuis M (1991) Methanol metabolism in a peroxisome-deficient mutant of *Hansenula polymorpha*: a physiological study. Arch Microbiol 156: 15-23.

"numeric" Compound Styles
'''''''''''''''''''''''''

Compound styles are a variation of the **numeric** in-text style format. With these styles, popular in the field of chemistry, bibliographic entries may contain multiple references. Once a citation has defined such a bibliographic entry (e.g, "[2]"), it becomes possible to cite individual items within the entry (e.g., "[2b]"). This format is not yet supported by CSL.

**Example Bibliography**

1. Gidijala L, et al. (2008) BMC Biotechnol 8: 29.

2. \a) Zwart KB, et al. (1983) Antonie van Leeuwenhoek 49: 369-385, b) van der Klei IJ, et al. (1991) Arch Microbiol 156: 15-23.

"label" Styles
''''''''''''''

Cites of **label** styles consist of short keys, e.g. "[GBKv2008]" and "[ZwVH1983; vaHV1991]". These keys are also included in the bibliographic entries. CSL has limited support for this format, since it currently doesn't allow for (style-specific) customisation of the key format.

**Example Bibliography**

[GBKv2008] Gidijala L, Bovenberg RA, Klaassen P, van der Klei IJ, Veenhuis M, et al. (2008) Production of functionally active *Penicillium chrysogenum* isopenicillin N synthase in the yeast *Hansenula polymorpha*. BMC Biotechnol 8: 29.

[vaHV1991] van der Klei IJ, Harder W, Veenhuis M (1991) Methanol metabolism in a peroxisome-deficient mutant of *Hansenula polymorpha*: a physiological study. Arch Microbiol 156: 15-23.

[ZwVH1983] Zwart KB, Veenhuis M, Harder W (1983) Significance of yeast peroxisomes in the metabolism of choline and ethanolamine. Antonie van Leeuwenhoek 49: 369-385.

Note Styles
^^^^^^^^^^^

The second category of citation styles consists of **note** styles. Here a *marker*, which can be a number or a symbol, is added to the sentence when works are cited, e.g. "[*]_" and "[*]_". Each marker points to a footnote or endnote. CSL styles do not control which number formats or symbols are used for the markers, which is left to the word processor. In contrast to **in-text** citations, footnotes and endnotes typically contain all information required to identify the cited works. Some **note** styles include a bibliography to give an overview of all cited works, and to describe the works in more detail.

    .. [*] 'Voyage to St. Kilda' (3rd edit. 1753), p. 37.
    .. [*] Sir J. E. Tennent, 'Ceylon,' vol. ii. 1859, p. 107.

The CSL Ecosystem
~~~~~~~~~~~~~~~~~

To understand how CSL works, let's start by taking a look at the various bits and pieces of the CSL ecosystem:

|csl-infrastructure|

.. |csl-infrastructure| image:: https://github.com/rmzelle/writing/raw/master/csl-infrastructure.png
   :width: 257pt

Independent and Dependent Styles
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Styles! Everything in the world of CSL revolves around styles. But not all CSL styles are alike. There are two types: **independent styles** and **dependent styles**.

An **independent CSL style** has two functions: first, it needs to define a citation format. What does the format look like? Is it an "author-date" style, or a "note" style? Are cites ordered alphabetically, or by date? Should bibliographic entries include DOIs? What punctuation and capitalization should be used? Does the year of publication come before or after the title? Etcetera, etcetera. Secondly, the CSL style must describe itself. We call this self-describing information **style metadata**, and it can include the title of the journal for which the CSL style was created, a link to that journal's website, the name of the creator of the CSL style, etc.

A **dependent CSL style**, on the other hand, only contains **style metadata**. Instead of providing a definition of a citation format, a dependent style simply refers to an independent CSL style (its "parent"), whose citation format will be used instead.

Dependent styles come in handy when multiple CSL styles share the same citation format. Take a publisher which uses a single citation format for all its journals. If we were limited to using independent CSL styles, every journal's CSL style would need to contain a full definition of the citation format, even though it would be the same for each journal. This would produce a collection of bulky styles that are hard to maintain. If the publisher makes a change to its citation format, we would have to update every single independent CSL style.

Dependent styles solve these problems. For example, the journals "Nature Biotechnology", "Nature Chemistry", and "Nature" all use the same citation format. We therefore created dependent CSL styles for "Nature Biotechnology" and "Nature Chemistry" that both point to our independent CSL style for "Nature". Since they don't define a citation format, dependent styles are a fraction of the size of an independent style. And, if the Nature Publishing Group ever decides to change the "Nature" citation format across its journals, we only have to correct the citation format in the "Nature" CSL style, without having to touch any of its dependents.

Locale Files
^^^^^^^^^^^^

I have a little secret to share with you: most independent styles aren't actually fully independent.

When you write an independent CSL style, you can hard-code all language-specific information into the style. For example, you can put "Retrieved from" before the URL of a cited item, and use "YYYY, Month DD" as the date format:

Hartman, P., Bezos, J. P., Kaphan, S., & Spiegel, J. (1999, September 28). Method and system for placing a purchase order via a communications network. Retrieved from https://www.google.com/patents/US5960411

However, such a style would only be usable in US English. If you needed a German variant of this citation format, you would have to change all the translations and date formats within the style.

To make it easier to adapt CSL styles to other languages, and to even allow a single CSL style to be used in more than one language, CSL uses **locale files**. These files contain various language-specific preferences: translations, date formats, and grammar. CSL styles can be written to be mostly language-agnostic, where they rely on these locale files for their localization.

In our example above, we could rewrite the CSL style to use the "retrieved" and "from" terms, and to use the localized "text" date format. Now, if the CSL style is set to German, it will retrieve the German translations and date format from the German locale file, and produce:

Hartman, P., Bezos, J. P., Kaphan, S., & Spiegel, J. (28. September 1999). Method and system for placing a purchase order via a communications network. Abgerufen von https://www.google.com/patents/US5960411

By using locale files, we only need to define translations, date formats, and grammar once per language. This helps keeping styles compact, and makes locale data much easier to maintain. Since citation formats for a given language don't always agree on a translation or date format, it is possible to overwrite any locale data in CSL styles.

Item Metadata
^^^^^^^^^^^^^

Next up are the bibliographic details of the items you wish to cite: the **item metadata**.

For example, the bibliographic entry for a journal article may show the names of the authors, the year in which the article was published, the article title, the journal title, the volume and issue in which the article appeared, the page numbers of the article, and the article's Digital Object Identifier (DOI). All these details help the reader identify and find the referenced work.

Reference managers make it easy to create a library of items. While many reference managers have their own way of storing item metadata, most support common bibliographic exchange formats such as BibTeX and RIS. The citeproc-js CSL processor introduced a JSON-based format for storing item metadata in a way citeproc-js could understand. Several other CSL processors have since adopted this "CSL JSON" format (also known as "citeproc JSON").

CSL Processors
^^^^^^^^^^^^^^

With CSL styles, locale files, and item metadata in hand, we now need a piece of software to parse all this information, and generate citations and bibliographies in the correct format. This is the job of the **CSL processor**. While the CSL project doesn't develop CSL processors itself, there are various open source CSL processors available.

Citing Details
^^^^^^^^^^^^^^

Citations often contain information other than just the item metadata. These **citing details** include the order in which items are cited in the document, which can affect the order of references in the bibliography and their numbering. Position can also play a role when items are cited multiple times in the same document: subsequent cites are often more compact than the first cite to an item. Another example is the use of locators, which guide the reader to a specific section within the cited work, such as the page numbers within a chapter where a certain argument is made, e.g. "(Doe, 2000, p. 43-44)".

XML Basics
~~~~~~~~~~

For those new to XML, this section gives a short overview of what you need to know about XML in order to read and edit CSL styles and locale files. For more background, just check one of the many XML tutorials online.

Let's take a look at the following dependent CSL style:

.. sourcecode:: xml

    <?xml version="1.0" encoding="utf-8"?>
    <style xmlns="http://purl.org/net/xbiblio/csl" version="1.0" default-locale="en-US">
      <info>
        <title>Applied and Environmental Microbiology</title>
        <id>http://www.zotero.org/styles/applied-and-environmental-microbiology</id>
        <link href="http://www.zotero.org/styles/applied-and-environmental-microbiology"
              rel="self"/>
        <link href="http://www.zotero.org/styles/american-society-for-microbiology"
              rel="independent-parent"/>
        <link href="http://aem.asm.org/" rel="documentation"/>
        <category citation-format="numeric"/>
        <category field="biology"/>
        <issn>0099-2240</issn>
        <eissn>1098-5336</eissn>
        <updated>2012-09-09T21:58:08+00:00</updated>
        <rights license="http://creativecommons.org/licenses/by-sa/3.0/">This work is
    licensed under a Creative Commons Attribution-ShareAlike 3.0 License</rights>
      </info>
    </style>

There are several concepts and terms you need to be familiar with. These are:

- **XML Declaration**. The first line of each style and locale file is usually the XML declaration. In most cases, this will be ``<?xml version="1.0" encoding="utf-8"?>``. This line designates the document as XML, and specifies the XML version ("1.0") and character encoding ("utf-8") used.

- **Elements and Hierarchy**. The basic building blocks of XML documents are elements. Each XML document contains a single root element (for CSL styles this is ``<style/>``). If an element contains other elements, this parent element is split into a start tag (``<style>``) and an end tag (``</style>``). In our example, the ``<style/>`` element has one child element, ``<info/>``. This element has several children of its own, which are grandchildren of the grandparent ``<style/>`` element. Element tags are always wrapped in less-than ("<") and greater-than (">") characters (e.g., ``<style>``). For empty-element tags, ">" is preceded by a forward-slash (e.g., ``<category/>``), while for end tags "<" is followed by a forward-slash (e.g., ``</style>``). Child elements are typically indented with spaces or tabs to show the different hierarchical levels. In the CSL project, we use 2 spaces per level.

- **Attributes and Element Content**. There are two ways to add additional information to elements. First, XML elements can carry one or more attributes (the order of attributes on an element is arbitrary). Every attribute needs a value. For example, the ``<style/>`` element carries a ``version`` attribute, set to a value of "1.0", indicating that the style is written in CSL 1.0. Secondly, elements can store non-element content between start and end tags, e.g. the content of the ``<title/>`` element is "Applied and Environmental Microbiology".

- **Namespace**. To indicate that all the elements in the style or locale file are part of CSL, the root element always carries the ``xmlns`` attribute, set to the CSL XML namespace URI, "http://purl.org/net/xbiblio/csl". In the rest of this primer we will use the namespace prefix "cs:" when referring to CSL elements (e.g., ``cs:style`` instead of ``<style/>``).

- **Escaping**. Some characters have to be substituted when used for purposes other than for defining the XML structure (e.g., when used in attribute values or non-element content), or, in the case of the ampersand ("&"), for substitution itself. Escape sequences are "&lt;" for "<", "&gt;" for ">", "&amp;" for "&", "&apos;" for ', and "&quot;" for ". For example, the link "http://domain.com/?tag=a&id=4" is escaped as ``<link href="http://domain.com/?tag=a&amp;id=4"/>``.

- **Well-formedness and Schema Validity**. Unlike HTML, XML does not allow for any markup errors. Any error, like forgetting an end tag, having more than one root element, or incorrect escaping will break the XML document and can prevent it from being processed. XML documents that follow the XML specification and are error-free are "well-formed". For well-formed CSL styles and locale files there is a second level of testing, involving the CSL schema. Our schema describes which CSL elements and attributes are allowed and how they must be used. When a style or locale file is tested against the rules of the CSL schema and passes, the file is valid CSL (this process is called "validation"). Only well-formed and valid CSL files can be expected to work properly.

Dissecting a Dependent Style
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Lets look again at the dependent style we showed above. This time, we include XML comments to describe each part of the style (XML comments start with ``<!--`` and end with ``-->``, and are ignored by the CSL processor).

.. sourcecode:: xml

    <!-- The CSL style begins with the XML declaration -->
    <?xml version="1.0" encoding="utf-8"?>
    <!-- The cs:style root element. The "default-locale" attribute sets this style's
         locale to US English. -->
    <style xmlns="http://purl.org/net/xbiblio/csl" version="1.0" default-locale="en-US">
      <info>
        <!-- cs:title stores the style's title. This style is for the journal
             "Applied and Environmental Microbiology". -->
        <title>Applied and Environmental Microbiology</title>
        <!-- cs:id stores the style's ID, used by the CSL processor to identify
             the style. -->
        <id>http://www.zotero.org/styles/applied-and-environmental-microbiology</id>
        <!-- The "self" URL is where this style can be found online. -->
        <link href="http://www.zotero.org/styles/applied-and-environmental-microbiology"
              rel="self"/>
        <!-- The "independent-parent" URL is where the independent parent style can be
             found online. -->
        <link href="http://www.zotero.org/styles/american-society-for-microbiology"
              rel="independent-parent"/>
        <!-- The "documentation" URL is where documentation about this citation style can
             be found online. -->
        <link href="http://aem.asm.org/" rel="documentation"/>
        <!-- cs:category describes the type of style. The "citation-format" attribute
             indicates that this style uses "numeric" in-text citations, while the "field"
             attribute indicates that this style is relevant to the field of biology. -->
        <category citation-format="numeric"/>
        <category field="biology"/>
        <!-- cs:issn and cs:eissn store the journal's print and electronic ISSN,
             respectively -->
        <issn>0099-2240</issn>
        <eissn>1098-5336</eissn>
        <!-- cs:updated stores the timestamp of when the style was last updated -->
        <updated>2012-09-09T21:58:08+00:00</updated>
        <!-- cs:rights specifies the license under which the style is made available -->
        <rights license="http://creativecommons.org/licenses/by-sa/3.0/">This work is
    licensed under a Creative Commons Attribution-ShareAlike 3.0 License</rights>
      </info>
    </style>

As you can see, dependent styles don't contain any formatting instructions. Instead, the style above leans on the independent CSL style for the American Society for Microbiology.

Reading Independent Styles
~~~~~~~~~~~~~~~~~~~~~~~~~~



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

Dissecting an Independent Style
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Discuss, info section, give example of formatted citations, discuss cs:citation element (et-al-* attributes), cs:layout, delimiters/affixes, names, dates, terms/locales/redefining terms. give example of formatted bib, discuss cs:bibliography, sorting

Don't cover number, label right now.

Make style a bit more expansive with stuff from existing example primer, so journal papers are formatted halfway decent.
