===============================
`Citation Style Language 1.0`__
===============================
~~~~~~~~~~~~~~~~~~~~~~
Language Specification
~~~~~~~~~~~~~~~~~~~~~~

__ `Table of Contents`_

.. class:: fixed

   `citationstyles.org`__

__ http://citationstyles.org/

.. class:: version-links

    This version:
        http://citationstyles.org/downloads/specification-csl10-20100321.html
    Latest version:
        http://citationstyles.org/downloads/specification.html

.. class:: contributors

   Author
       * Rintze M. Zelle
       
   Contributors
       * Frank G. Bennett, Jr.
       * Bruce D'Arcus

.. |link| image:: link.png


========

.. contents:: Table of Contents

========


Introduction
------------

The Citation Style Language (CSL) is an |link| `XML
<http://en.wikipedia.org/wiki/XML>`_ format for describing the formatting of
in-text citations, notes and bibliographies. CSL offers:

-  An open format that may be used by any application
-  The ability to write compact and robust styles
-  Extensive support for style requirements
-  Automatic style localization
-  Easy distribution and updating of styles
-  A fast growing library with thousands of freely available styles

This document is meant as a complete and accurate specification of CSL 1.0.
Additional documentation, such as the CSL schema, CSL styles, and information on
how to add CSL support to applications, can be found at the official home of
CSL, |link| `citationstyles.org <http://citationstyles.org>`_.

CSL Styles - Basic Structure
----------------------------

Namespacing
~~~~~~~~~~~

All elements in CSL are |link| `namespaced
<http://en.wikipedia.org/wiki/XML_Namespace>`_. The recommended prefix ``cs`` is
attached to element names throughout this specification, but is usually omitted
from CSL styles when the default namespace is declared in the root ``cs:style``
element.

The CSL namespace
    "http://purl.org/net/xbiblio/csl"

XML Declaration
~~~~~~~~~~~~~~~

It is highly recommended to initialize each CSL style with an XML declaration,
specifying the version of XML used as well as the character encoding. In most
cases, the declaration will be:

.. sourcecode:: xml

    <?xml version="1.0" encoding="UTF-8"?>

The Root Element - ``cs:style``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The root element of a CSL style is ``cs:style``. This element carries the
following arguments:

``class``
    Specifies whether the style uses notes (value "note") or in-text citations
    ("in-text").

``default-locale`` (optional)
    Fixes style localization to the |link| `locale code
    <http://books.xmlschemata.org/relaxng/ch19-77191.html>`_ specified. This is
    desirable for most journal styles.

``version``
    Indicates with which version of the CSL schema the style is compatible.
    Should have a value of "1.0" for CSL 1.0-compatible styles.

``xmlns`` (optional)
    The namespace declaration that binds the elements in the style to the given
    namespace URI. CSL elements in the style don't need individual namespace
    declarations if this attribute is set to "http://purl.org/net/xbiblio/csl".

In addition, ``cs:style`` may carry any of the `global options`_, as well as the
`inheritable name options`_.

An example of a style preamble:

.. sourcecode:: xml

    <?xml version="1.0" encoding="UTF-8"?>
    <style xmlns="http://purl.org/net/xbiblio/csl" version="1.0" class="in-text" default-locale="fr-FR">

Child Elements of ``cs:style``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

All independent CSL styles share the same basic structure, with five possible
types of child elements in the ``cs:style`` root element. The roles of each of
these elements (which will be described in more detail later) are:

``cs:info``
    The ``cs:info`` element must be included as the first child element of
    ``cs:style``. It contains the metadata that describes the style (the name of
    the style, a unique style identifier, the style authors, etc.).

``cs:citation``
    This required element describes the formatting instructions of in-text
    citations or notes.

``cs:bibliography`` (optional)
    This optional element describes the formatting instructions of the
    bibliography.

``cs:macro`` (optional)
    Styles may include one or more ``cs:macro`` elements. Macros allow for reuse
    of formatting instructions, which helps keeping styles compact and
    maintainable.

``cs:locale`` (optional)
    Styles may include one or more ``cs:locale`` elements. These elements allow
    styles to override the default localization data (terms, date formats and
    formatting options) on a per-locale basis.

Info
^^^^

The ``cs:info`` element contains all the style's metadata, many elements of
which are borrowed from the |link| `Atom Syndication Format
<http://tools.ietf.org/html/rfc4287>`_. Although it has no influence on how
citations are formatted, complete and correct metadata is important if styles
are made publicly available. Below is an example of a ``cs:info`` element,
followed by a description of all possible elements.

.. sourcecode:: xml

    <info>
     <title>Style Title</title>
     <id>http://www.zotero.org/styles/style-title</id>
     <link href="http://www.zotero.org/styles/style-title" rel="self"/>
     <author>
      <name>Author Name</name>
      <email>name@domain.com</email>
      <uri>http://www.domain.com/name</uri>
     </author>
     <category citation-format="author-date"/>
     <category field="zoology"/>
     <updated>2008-10-29T21:01:24+00:00</updated>
     <summary>Style for Some Journal</summary>
     <rights>This work is licensed under a Creative Commons
             Attribution-Share Alike 3.0 Unported License
             http://creativecommons.org/licenses/by-sa/3.0/</rights>
    </info>

``cs:author`` and ``cs:contributor`` (optional)
    One or more of these elements may be used to acknowledge style authors and
    contributors. Authorship is generally limited to those who have written a
    new style, or have made significant changes to existing styles, while
    contributorship can be assigned to those who have made small changes. Both
    elements require one child element, cs:name, and allow for two others,
    cs:email, and cs:uri, indicating respectively the name, email address and
    URI of the author or contributor in question.

``cs:category`` (optional)
    Styles may be assigned one or more categories. This information can be used
    to organize style repositories. Two types of categories exist. The first
    category type describes how in-text citations are rendered. For this type
    the ``citation-format`` attribute is set to one of the following values:
    
    -  "author-date": e.g. "... (Doe, 1999)"
    -  "author": e.g. "... (Doe)"
    -  "numeric": e.g. "... [1]"
    -  "label": e.g. "... [doe99]"
    -  "note": the citation appears as a footnote or endnote
    
    The second category type indicates the fields or disciplines for which the
    style is relevant. For this category type the ``field`` attribute is set to
    one of the discipline `categories`_.

``cs:id``
    This required element should contain a URI. This identifier establishes the
    identity of the style. A valid, stable, and unique URL that resolves to the
    style is desired if the style is made publicly available. Keeping the same
    URI is crucial for applications that support automatic style updating.

``cs:issn``/``cs:issnl`` (optional)
    Journal-specific styles may include one or more ``cs:issn`` elements,
    containing the journal's ISSN identifiers (multiple ISSNs can be assigned to
    a single journal, e.g. for the print and online editions). In addition, the
    ``cs:issnl`` element may be used for the newly established |link| `ISSN-L
    identifier <http://www.issn.org/2-22637-What-is-an-ISSN-L.php>`_.

``cs:link`` (optional)
    The ``cs:link`` element is used to specify a URI (usually a URL), which is
    set on the ``href`` attribute. The accompanying ``rel`` attribute must be
    set to indicate the relation of the URI to the style. The possible values of
    ``rel``:
    
    -  "self": if the URI is that of the CSL style itself. Needed for automatic
       style updating.
    -  "independent-parent": if the URI is that of the parent CSL style, the
       content of which should be used for the citation formatting. Needed for
       `dependent styles`_.
    -  "template": if the URI is that of the CSL style from which the current
       independent style is derived. May be used to indicate style parentage.
    -  "documentation: if the URI points to the online style documentation.
    
    The ``cs:link`` element may contain textual content to describe the link,
    and may carry the ``xml:lang`` attribute to specify the language of either
    the link description or of the link target (the value should be a
    |link| `xsd:language locale code
    <http://books.xmlschemata.org/relaxng/ch19-77191.html>`_).

``cs:published`` (optional)
    The contents of this element must be a |link| `timestamp
    <http://books.xmlschemata.org/relaxng/ch19-77049.html>`_. This timestamp
    indicates when the style was initially created or made available.

``cs:rights`` (optional)
    This element specifies the license under which the style file is released.
    See, e.g. the |link| `Creative Commons
    <http://creativecommons.org/license/>`_. The element may include a
    ``xml:lang`` attribute to specify the language of the content (the value
    should be an |link| `xsd:language locale code
    <http://books.xmlschemata.org/relaxng/ch19-77191.html>`_).

``cs:summary`` (optional)
    This element gives a summary of the style.The element may include a
    ``xml:lang`` attribute to specify the language of the content (the value
    should be an |link| `xsd:language locale code
    <http://books.xmlschemata.org/relaxng/ch19-77191.html>`_).

``cs:title``
    The contents of this required element should be the name of the style as it
    should be shown to users. The element may include a ``xml:lang`` attribute
    to specify the language of the content (the value should be an |link|
    `xsd:language locale code
    <http://books.xmlschemata.org/relaxng/ch19-77191.html>`_).

``cs:updated``
    The contents of this required element must be a |link| `timestamp
    <http://books.xmlschemata.org/relaxng/ch19-77049.html>`_. This timestamp is
    used for automatic updating of styles.

Citation
^^^^^^^^

The ``cs:citation`` element describes the formatting of citations, which can
consist of one or multiple references to bibliographic sources, and may appear
in the form of either in-text citations (generally formatted as label [doe99],
number [1], author [Doe] or author-date descriptors [Doe 1999]) or notes. The
required ``cs:layout`` child element describes what, and how, bibliographic data
should be included in the citations (see the chapter on the `Layout element
<#layout>`_). The ``cs:citation`` element may carry attributes for
citation-specific formatting options and inheritable name options (see the
`Citation-specific Options`_ and `Inheritable Name Options`_ sections).
Finally, the optional ``cs:sort`` element, which should precede the
``cs:layout`` element, specifies how citations consisting of multiple references
should be sorted (see the chapter on `Sorting`_). An example of a
``cs:citation`` element:

.. sourcecode:: xml

    <citation option="option-value">
      <sort>
        <!-- sort keys -->
      </sort>
      <layout>
        <!-- rendering elements -->
      </layout>
    </citation>

**A note to developers of CSL processors** Note styles are unique in that
citations may effectively become full sentences. Because of this, the first
character of the output should be uppercased when a citation is footnoted
without any additional text. By contrast, if the citation occurs within a
pre-existing footnote, and is preceded by non-citation text, then it should be
printed as is.

Bibliography
^^^^^^^^^^^^

The ``cs:bibliography`` element describes the formatting of bibliographies, and
is used in a similar way as ``cs:citation``: the required ``cs:layout`` child
element describes how each reference should be formatted in the bibliography,
while the optional ``cs:sort`` element (which should precede the ``cs:layout
element) specifies the sorting order of the references in the bibliography. In
addition, the ``cs:bibliography`` element may carry attributes for
bibliography-specific formatting options and inheritable name options (see the
`Bibliography-specific Options`_ and `Inheritable Name Options`_ sections).

.. sourcecode:: xml

    <bibliography option="option-value">
      <sort>
        <!-- sort keys -->
      </sort>
      <layout>
        <!-- rendering elements -->
      </layout>
    </bibliography>

Macro
^^^^^

Macros, which are defined using ``cs:macro`` elements, can contain the same set
of `rendering elements`_ that are available within ``cs:layout`` inside
``cs:citation`` or ``cs:bibliography``. Macros allow formatting instructions to
be reused, both within the same style (e.g. the same macro could be used in both
``cs:citation`` and ``cs:bibliography``) as well as between styles. It is
therefore recommended to use common macro names as much as possible. Correct use
of macros can greatly improve the readability, compactness and maintainability
of styles. Ideally, the contents of ``cs:citation`` and ``cs:bibliography``
should be kept compact and agnostic of resource types (i.e. books, journal
articles, etc.), depending mainly on macro calls.

By convention, macros are placed after any ``cs:locale`` elements and before the
``cs:citation`` element. The ``cs:macro`` element must carry the ``name``
attribute (the value of which is used to identify the macro), and contain one or
more `rendering elements`_. Once defined, macros can be called by `rendering
elements`_ in ``cs:citation`` or ``cs:bibliography`` (from within
``cs:layout``), or by the `rendering elements`_ in other macros.

The following example shows a style that call the "title" macro. This macro
outputs the contents of the title variable, applying italics when the resource
type is "book":

.. sourcecode:: xml

    <style>
      <macro name="title">
        <choose>
          <if type="book">
            <text variable="title" font-style="italic"/>
          </if>
          <else>
            <text variable="title"/>
          </else>
        </choose>
      </macro>
      <citation>
        <layout>
          <text macro="title"/>
        </layout>
      </citation>
    </style>

Locale
^^^^^^

CSL supports localization of terms, date formats and formatting options. Default
localization data for several tens of locales is provided through
"locales-xx-XX.xml" files ("xx-XX" represents the locale code, e.g. "en-US" for
US English). Localization data can also be included in styles, using one or more
of the optional ``cs:locale`` elements, which by convention are included
directly after the ``cs:info`` element. For each ``cs:locale`` element, the
relevant locale can be indicated with the ``xml:lang`` attribute (set to an
|link| `xsd:language locale code
<http://books.xmlschemata.org/relaxng/ch19-77191.html>`_). If the attribute is
absent, the ``cs:locale`` element's localization data will apply to all locales.

See `Localized Terms`_, `Localized Dates`_ and `Localized Options`_ in the
`Locale Files - Basic Structure`_ section for more details on the use of
``cs:locale``.

An example illustrating the use of ``cs:locale`` in a CSL style:

.. sourcecode:: xml

    <style>
      <locale xml:lang="en">
        <terms>
          <term name="editortranslator" form="short">
            <single>ed. &amp; trans.</single>
            <multiple>eds. &amp; trans.</multiple>
          </term>
        </terms>
      </locale>
    </style>

Locale prioritization
'''''''''''''''''''''

Locale codes can indicate either the language (e.g. "en" for English) or the
language dialect (e.g. "en-US" for American English and "en-GB" for British
English). While the "locales-xx-XX.xml" files are only maintained for language
dialects, the (optional) ``xml:lang`` attribute on ``cs:locale`` in styles may
be set to languages as well as language dialects. The "locales-xx-XX.xml" files
must contain the full set of localization data. The ``cs:locale`` elements are
typically only used in styles to redefine the localization data provided via the
"locales-xx-XX.xml" files, and these may include only the localization data that
should be redefined. The existence of two types of locale codes (languages and
language dialects), and the ability to define localization both in
"locales-xx-XX.xml" files and in styles, requires prioritization of localization
data. This prioritization can best be illustrated with an example. If a CSL
processor is asked to localize the style output to "de-AT" (Austrian German),
the priority of the locale data is as follows:

Localization data specified in styles using ``cs:locale``

1. ``xml:lang`` set to "de-AT" (Austrian German)
2. ``xml:lang`` set to "de" (German)
3. ``xml:lang`` not set (all locales)

Localization data stored in "locales-xx-XX.xml" files

4. ``xml:lang`` set to "de-AT" (Austrian German)
5. ``xml:lang`` set to "de-DE" (Standard German)
6. ``xml:lang`` set to "en-US" (American English)

Thus, when a style does not include a ``cs:locale`` element for the "de-AT"
locale, or when it exists but is incomplete, the missing localization data is
retrieved from the ``cs:locale`` set to "de" (if present). If the set of
localization data is still incomplete, the ``cs:locale`` element without a
``xml:lang`` element is used (if present). The localization data is completed
with the data stored in the "locales-xx-XX.xml" files. If the file for "de-AT"
does not exist, fallback locales consist of "de-DE" and, as a last resort,
"en-US". Note that locale substitution is only activated when a term is not
defined. It does not occur when a term is defined, but consists of an empty
string (e.g. <term name="and"/> or <term name="and"></term>).

Dependent Styles
~~~~~~~~~~~~~~~~

In addition to independent styles, which are self-contained, CSL also supports
dependent styles, which function like aliases or shortcuts. Dependent styles can
be used when multiple journals share the same style format. In such a case, it
is sufficient to create a single independent master style for the format (e.g.
"Nature Journals"). Dependent styles, which only contain a ``cs:info`` element,
can then be added for all journals that use this format (e.g. "Nature
Biotechnology", "Nature Nanotechnology", etc.). With this approach, style
repositories can show entries for the individual journals, without the need to
duplicate formatting instructions. If the common format has to be modified, it
is sufficient to change the independent master style, which makes style
maintainance simpler and faster.

The ``cs:info`` element of dependent styles should provide the metadata of the
individual journals. A ``cs:link`` element which points to the independent
master style must be included (for this the ``rel`` attribute on the relevant
``cs:link`` element should be set to "independent-parent", see also `Info`_).

N.B. Dependent styles cannot be used to indicate changes compared to the
independent master style. If there is any difference in formatting between two
styles, however small, separate independent styles have to be created.

Locale Files - Basic Structure
------------------------------

CSL ships with a number of "locales-xx-XX.xml" files (the "xx-XX" is the locale
code, e.g. "en-US" for US English). While localization data can also be
specified in styles (see `Locale`_), locale files conveniently provide complete
sets of default localization data (terms, dates and formatting options).

The locale files, which like styles are written in XML, each contain the
localization data for a single locale. The ``cs:locale`` root element require
two attributes: ``xml:lang``, to specify the locale of the data, and
``version``, to indicates with which version of the CSL schema the locale file
is compatible (this attribute should have a value of "1.0" for CSL
1.0-compatible styles). The root element also typically carries a ``xmlns``
namespace declaration, set to the CSL namespace
("http://purl.org/net/xbiblio/csl"). The ``cs:locale`` element has three
required child elements, which are described in the sections below:
``cs:terms``, ``cs:date`` and ``cs:style-options``. An example of the
(incomplete) contents of a locale file:

.. sourcecode:: xml

    <?xml version="1.0" encoding="UTF-8"?>
    <locale xml:lang="en-US" version="1.0" xmlns="http://purl.org/net/xbiblio/csl">
      <terms>
        <term name="no date">n.d.</term>
        <term name="et-al">et al.</term>
        <term name="page">
          <single>page</single>
          <multiple>pages</multiple>
        </term>
        <term name="page" form="short">
          <single>p.</single>
          <multiple>pp.</multiple>
        </term>
      </terms>
      <date form="text">
        <date-part name="month" suffix=" "/>
        <date-part name="day" suffix=", "/>
        <date-part name="year"/>
      </date>
      <date form="numeric">
        <date-part name="year"/>
        <date-part name="month" form="numeric" prefix="-" range-delimiter="/"/>
        <date-part name="day" prefix="-" range-delimiter="/"/>
      </date>
      <style-options punctuation-in-quote="true"/>
    </locale>

Localized Terms
~~~~~~~~~~~~~~~

Terms are localized strings. For example, if a style specifies that the term
"and" should be used, the string that appears in the style output depends on the
locale: "and" for English, "und" for German. Terms are defined using ``cs:term``
elements, child elements of ``cs:terms``, itself a child element of
``cs:locale``. Terms are identified by the value of the ``name`` attribute of
``cs:term``. Two types of terms exist: simple terms, where the content of the
``cs:term`` is the localized string, and compound terms, where ``cs:term``
includes the two child elements ``cs:single`` and ``cs:multiple``, which
respectively contain the singular and plural variant of the term (e.g. "page"
and "pages"). Some terms are defined for multiple forms. In these cases,
multiple ``cs:term`` element share the same value of ``name``, but differ in the
value of the optional ``form`` attribute. The different forms are:

-  "long" - the default, e.g. "editor" and "editors" for the term
   "editor"
-  "short" - e.g. "ed" and "eds" for the term "editor"
-  "verb" - e.g. "edited by" for the term "editor"
-  "verb-short" - e.g. "ed" for the term "editor"
-  "symbol" - e.g. "�" for the term "section"

Examples of how terms are defined have been given above (`Locale Files - Basic
Structure`_). The complete list of terms can be found in `Appendix III -
Terms`_.

Localized Dates
~~~~~~~~~~~~~~~

Styles can use either localized or non-localized date formats. Localized date
formats are defined with the ``cs:date`` element as child element of
``cs:locale``. The required ``form`` attribute on ``cs:date`` must be set to
either "numeric" (for numeric date formats, e.g. "12-15-2005") or to "text"
(e.g. "December 15, 2005"). A date format is then defined by the child elements
of ``cs:date``, the ``cs:date-part`` elements. These must carry the ``name``
attribute, set to ``day``, ``month`` or ``year``. The order of the
``cs:date-part`` elements is also the display order. Additional formatting can
be achieved by setting `formatting`_ attributes on the ``cs:date`` and
``cs:date-part`` elements, as well as a number of attributes that are specific
to ``cs:date-part`` (see `Date-part`_). In addition, a `delimiter`_ may be set
on ``cs:date`` to delimit the ``cs:date-part`` elements, and `affixes`_ may be
applied to the ``cs:date-part`` elements.

N.B. Affixes are not allowed on ``cs:date`` when used as a child element of
``cs:locale``. This helps in separating locale-specific affixes (which should be
set on the ``cs:date-part`` elements) from any style-specific affixes (such as
parentheses, which should be set on the ``cs:date`` rendering element). E.g. a
macro could specify:

.. sourcecode:: xml

      <macro name="issued">
       <date variable="issued" form="numeric" prefix="(" suffix=")"/>
      </macro>

Localized Options
~~~~~~~~~~~~~~~~~

CSL 1.0 includes a single localized global option (affecting both citation and
bibliography output), ``punctuation-in-quote`` (see `Locale Options`_). This
option is set as an attribute on ``cs:style-options``, a child element of
``cs:locale``.

Rendering Elements
------------------

Rendering elements are used to specify which, and in what order, bibliographic
data should be included in citations and bibliographies. Rendering elements also
partly control the formatting of this data.

Layout
~~~~~~

As discussed in the `citation`_ and `bibliography`_ sections, ``cs:layout`` is a
required child element of both ``cs:citation`` and ``cs:bibliography``. All the
rendering elements that should appear in the citations and bibliography should
be nested inside the ``cs:layout`` element. Itself a rendering element,
``cs:layout`` accepts both `affixes`_ and `formatting`_ attributes. When used in
the ``cs:citation`` element, a `delimiter`_ can be set to separate multiple
bibliographic items in a single citation. For example, citations like "(1, 2)"
can be produced with:

.. sourcecode:: xml

    <layout prefix="(" suffix=")" delimiter=", ">
      <text variable="citation-number"/>
    </layout>

Text
~~~~

The ``cs:text`` element is used to output text, which can originate from
different sources. The source-type is indicated with an attribute, and the
attribute value acts as an identifier within the source-type. For example,

.. sourcecode:: xml

    <text variable="title" form="short" font-style="italic"/>

indicates that the source-type is a variable, and that the variable that should
be displayed is the italicized short form of "title". The different source-types
are:

-  ``variable`` - the text contents of a variable (see `Standard Variables`_).
   The optional ``form`` attribute can be set to either "long" (the default) or
   "short" to select the long or short forms of variables, e.g. the full and
   short title.
-  ``macro`` - the text generated by a macro. The value of ``macro`` should
   correspond to the value of the ``name`` attribute of the desired ``cs:macro``
   element.
-  ``term`` - the text of a localized term (see `Appendix III - Terms`_ and
   `Locale`_). The ``plural`` attribute can be set to choose either the singular
   (value "false", the default) or plural variant (value "true") of a term. In
   addition, the ``form`` attribute can be set to select the desired term form
   ("long" [default], "short", "verb", "verb-short" or "symbol"). If for a given
   term the desired form does not exist, another form may be used: "verb-short"
   reverts to "verb", "symbol" reverts to "short", and "verb" and "short" both
   revert to "long".
-  ``value`` - used to output verbatim text, which is set via the
   value of ``value`` (e.g. value="some text")

In all cases the attributes for `affixes`_, `display`_, `formatting`_,
`quotes`_, `strip-periods`_ and `text-case`_ may be applied to ``cs:text``.

Date
~~~~

The ``cs:date`` element is used to output dates, in either a localized or a
non-localized format. The desired date variable (see `Date Variables`_) is
selected with the ``variable`` attribute. If the selected variable is empty,
``cs:date`` renders the "no date" term.

Localized date formats are selected with the ``form`` attribute. This attribute
can be set to "numeric" (for numeric date formats, e.g. "12-15-2005"), or to
"text" (for date formats with a non-numeric month, e.g. "December 15, 2005").
Localized dates can be customized in two ways. First, the ``date-parts``
attribute may be used to specify which ``cs:date-part`` elements are shown. The
possible values are:

-  "year-month-day" - default, displays year, month and day
-  "year-month" - displays year and month
-  "year" - displays year only

Secondly, ``cs:date`` may include one or more ``cs:date-part`` elements (see
`Date-part`_). The attributes set on these elements override those originally
specified for the localized date formats (e.g. the ``form`` attribute of the
month-``cs:date-part`` element can be set to "short" to get abbreviated month
names in all locales.). Note that the use of ``cs:date-part`` elements for
localized dates does not affect which, and in what order, the ``cs:date-part``
elements are included in the rendered date. Also, the ``cs:date-part`` elements
may not carry the attributes for `affixes`_, as these are considered to be
locale-specific.

Non-localized date formats are self-contained: the date format is entirely
controlled by ``cs:date`` and its ``cs:date-part`` children. In contrast to
localized dates, ``cs:date`` is used without the ``form`` and ``date-parts``
attributes. Only the included ``cs:date-part`` elements will be rendered, in the
order in which they are specified. The ``cs:date-part`` elements may carry
attributes for both `affixes`_ and `formatting`_, while ``cs:date`` may carry a
`delimiter`_ (delimiting the various ``cs:date-part`` elements).

For both localized and non-localized dates, `affixes`_, `display`_ and
`formatting`_ attributes may be specified for the ``cs:date`` element.

Date-part
^^^^^^^^^

The ``cs:date-part`` element is used to control how the different date parts of
the date variable specified in the parent ``cs:date`` element are rendered. The
date parts are identified by the value of the ``name`` attribute, which can be:

``day``
    For ``day``, ``cs:date-part`` may carry the ``form`` attribute, with values:
    
    -  "numeric" - default, e.g. "1"
    -  "numeric-leading-zeros" - e.g. "01"
    -  "ordinal" - e.g. "1st"

``month``
    For ``month``, ``cs:date-part`` may carry the `strip-periods`_ and ``form``
    attributes. Abbreviated months (e.g. "Jan.", "Feb.") are `localized terms`_
    and include periods by default (if applicable). These periods are removed
    when `strip-periods`_ is set to "true" ("false" is the default). The
    ``form`` attribute can be set to:
    
    -  "long" - default, e.g. "January"
    -  "short" - e.g. "Jan."
    -  "numeric" - e.g. "1"
    -  "numeric-leading-zeros" - e.g. "01"

``year``
    For ``year``, ``cs:date-part`` may carry the ``form`` attribute, with values:
    
    -  "long" - default, e.g. "2005"
    -  "short" - e.g. "05"

All ``cs:date-part`` elements may carry the `formatting`_ and `text-case`_
attributes. Attributes for `affixes`_ are also allowed, except when ``cs:date``
is used to call a localized date format. Finally, the ``cs:date-part`` elements
may carry the ``range-delimiter`` attribute (see `Date Ranges`_).

Date Ranges
^^^^^^^^^^^

By default, date ranges are delimited by an en-dash (e.g. "May |--| July 2008").
The ``range-delimiter`` attribute can be used to specify custom date range
delimiters. The attribute value set on the largest date-part ("day", "month" or
"year") that differs between the two dates of the date range will then be used
instead of the en-dash. For example,

.. sourcecode:: xml
    
    <style>
      <citation>
        <layout>
          <date variable="issued">
            <date-part name="month" suffix=" "/>
            <date-part name="year" range-delimiter="/"/>
          </date>
        </layout>
      </citation>
    </style>

would result in "May |--| July 2008" and "May 2008/June 2009".

.. |--| unicode:: U+2013
   :trim:

AD and BC
^^^^^^^^^

The terms ``ad`` and ``bc`` (Anno Domini and Before Christ) are automatically
appended to years: ``bc`` is added to negative years (e.g. 2500BC), while ``ad``
is added to positive years of less than four digits (79AD).

Seasons
^^^^^^^

If a date includes a season instead of a month, a season term (``season-01`` to
``season-04``, respectively Spring, Summer, Autumn and Winter) will substituted
the month date-part. E.g.,

.. sourcecode:: xml
    
    <style>
      <citation>
        <layout>
          <date variable="issued">
            <date-part name="month" suffix=" "/>
            <date-part name="year"/>
          </date>
        </layout>
      </citation>
    </style>

would result in "May 2008" and "Winter 2009".

Uncertain Dates
^^^^^^^^^^^^^^^

Uncertain dates can receive special formatting by using the
``is-uncertain-date`` conditional (see `Choose`_) and the "circa" term.
The conditional tests "true" when a date is flagged as uncertain. For example,

.. sourcecode:: xml

    <style>
      <citation>
        <layout delimiter="; ">
          <choose>
            <if is-uncertain-date="issued">
              <text term="circa" form="short" suffix=" "/>
            </if>
          </choose>
          <date variable="issued">
            <date-part name="year"/>
          </date>
        </layout>
      </citation>
    </style>

would result in "2005" (normal certain date) and "ca. 2003" (uncertain date).

Number
~~~~~~

The ``cs:number`` element can be used to output any of the following variables
(selected with the ``variable`` attribute):

-  "edition"
-  "volume"
-  "issue"
-  "number"
-  "number-of-volumes"

Although these variables can also be rendered with ``cs:text``, ``cs:number``
has the benefit of offering number-specific formatting via the ``form``
attribute, with values:

-  "numeric" (default) - e.g. "1", "2", "3"
-  "ordinal" - e.g. "1st", "2nd", "3rd"
-  "long-ordinal" - e.g. "first", "second", "third"
-  "roman" - e.g. "i", "ii", "iii"

If a variable displayed with ``cs:number`` contains a mixture of numeric and
non-numeric text, only the first number encountered is used for rendering (e.g.
"12" when the entire string is "12th edition"). If a variable only contains
non-numeric text (e.g. "special edition"), the entire string is rendered, as if
`cs:text` were used instead. Fields can be tested for containing numeric content
with the ``is-numeric`` conditional, e.g. "12th edition" would test "true" while
"third edition" would test "false" (see `Choose`_).

The ``cs:number`` element may carry any of the `affixes`_, `display`_,
`formatting`_ and `text-case`_ attributes.

Names
~~~~~

The ``cs:names`` element can be used to display the contents of one or more
`name variables`_, each of which can contain multiple names (e.g. the "author"
variable will contain all the cited item's author names). The variables to be
displayed are set with the ``variable`` attribute. If multiple variables are
selected (separated by single spaces, see example below), each variable is
independently rendered in the order specified, with one exception: if the value
of ``variable`` consists of "editor" and "translator" (in either order), and if
the contents of the two name variables is identical, then the contents of only
one name variable is rendered. In addition, the "editor-translator" term is used
if the ``cs:names`` element contains a ``cs:label`` element, replacing the
default "editor" and "translator" terms (e.g., this might result in "Doe (editor
& translator)". The `delimiter`_ attribute may be set on ``cs:names`` to delimit
the names of the different name variables (e.g. the semicolon in "Doe (editor);
Johnson (translator)").

.. sourcecode:: xml

    <names variable="editor translator" delimiter="; ">
      <name/>
      <label prefix=" (" suffix=")"/>
    </names>

There are four child elements associated with the ``cs:names`` element:
``cs:name``, ``cs:et-al``, ``cs:substitute`` and ``cs:label`` (all discussed
below). In addition, the ``cs:names`` element may carry the attributes for
`affixes`_, `display`_ and `formatting`_.

Name
^^^^

The ``cs:name`` element is a required child element of ``cs:names``, and
describes both how individual names are formatted, and how names within a name
variable are separated from each other. The attributes that may be used on
``cs:name`` are:

``and``
    This attribute specifies the delimiter between the second to last and the
    last name of the names in a name variable. The value of the attribute may be
    either "text", which selects the "and" term, or "symbol", which selects the
    ampersand (&).

``delimiter``
    Specifies the text string to separate names of a name variable. The default 
    value is ", " ("J. Doe, S. Smith").

``delimiter-precedes-last``
    Determines in which cases the delimiter used to delimit names is also used
    to separate the second to last and the last name in name lists. The possible
    values are:
    
    -  "contextual" (default): the delimiter is only included for name lists
       with three or more names
       
       - 2 names: "J. Doe and T. Williams,"
       - 3 names: "J. Doe, S. Smith, and T. Williams"
    
    -  "always": the delimiter is always included
       
       - 2 names: "J. Doe, and T. Williams"
       - 3 names: "J. Doe, S. Smith, and T. Williams"
    
    -  "never": the delimiter is never included
       
       - 2 names: "J. Doe and T. Williams,"
       - 3 names: "J. Doe, S. Smith and T. Williams"

``et-al-min`` / ``et-al-use-first``
    Together, these two attributes control et-al abbreviation. When the number
    of names in a name variable matches or exceeds the number set on
    ``et-al-min``, the rendered name list is truncated at the number of names
    set on ``et-al-use-first``. If truncation occurs, the "et-al" term is
    appended to the names rendered, preceded by a space (e.g. "Doe et al.").

``et-al-subsequent-min`` / ``et-al-subsequent-use-first``
    Similar to ``et-al-min`` and ``et-al-use-first``, these attributes control
    et-al abbreviation, but now for subsequent cites (see `Note Distance`_). If
    these attributes are not set, the values of ``et-al-min`` /
    ``et-al-use-first`` are used instead.

The remaining attributes, discussed below, only affect personal names. Personal
names require a "family" name-part, and may also contain "given", "suffix",
"non-dropping-particle" and "dropping-particle" name-parts. The roles of
these name-parts, which are delimited by single spaces in rendered names, are:

-  "family": the surname minus any particles and suffixes
-  "given": the given names, which may be either full ("John Edward") or
   initialized ("J. E.")
-  "suffix": name suffix, e.g. "Jr." in "John Smith Jr." and "III" in "Bill
   Gates III"
-  "non-dropping-particle": name particles that are not dropped when only the
   last name is shown ("de" in the Dutch surname "de Koning") but which may be
   treated as a separate object from the family name (e.g. for sorting)
-  "dropping-particle": name particles that are dropped when only the surname
   is shown ("van" in "Ludwig van Beethoven", which becomes "Beethoven")

``form``
    Specifies whether all the name-parts of personal names should be displayed
    (value "long"), or only the family name and the non-dropping-particle (value
    "short"). A third value, "count", returns the total number of names that
    would be otherwise displayed by the use of the ``cs:names`` element (taking
    into account the effects of et-al abbreviation and editor/translator
    collapsing), and may be used for advanced `sorting`_.

``initialize-with``
    If this attribute is set, given names are converted to initials. The
    attribute value specifies the suffix that is included after each initial
    ("." results in "J.J. Doe"). Note that the global ``initialize-with-hyphen``
    option controls how compound given names (e.g. "Jean-Luc") are hyphenated
    when initialized (see `Hyphenation of Initialized Names`_).

``name-as-sort-order``
    Specifies that names should be displayed with the given name following the
    family name (e.g. "John Doe" becomes "Doe, John"). The attribute may have
    one of the two values:
    
    - "first": name-as-sort-order applies to the first name in each name
      variable
    - "all": name-as-sort-order applies to all names
    
    Note that the sort order of names may differ from the display order for
    names containing particles and suffixes (see `Name-part order`_). Also, this
    attribute only affects names written in the latin or Cyrillic alphabet.
    Names written in other alphabets (e.g. Asian scripts) are always shown with
    the family name preceding the given name.

``sort-separator``
    Sets the delimiter for name-parts that have switched positions as a result
    of ``name-as-sort-order``. The default value is ", " ("Doe, John"). As is
    the case for ``name-as-sort-order``, this attribute only affects names
    written in the latin or Cyrillic alphabet.

The ``cs:name`` element may also carry any of the attributes for `affixes`_ and
`formatting`_.

Name-part Order
'''''''''''''''

The order of name-parts depends on the values of the ``form`` and
``name-as-sort-order`` attributes on ``cs:name``, the value of the
``demote-non-dropping-particle`` attribute on ``cs:style`` (one of the `global
options`_), and the alphabet of the individual name. Finally, differences can
exist between the name that is displayed and the name that is used for sorting.
An overview of the different orders:

**Display order of latin/Cyrillic names**

----

:Conditions: ``form`` set to "long", 
:Order:
    1) given
    2) dropping-particle
    3) non-dropping-particle
    4) family
    5) suffix

:Example: [G�rard] [de] [la] [Martini�re] [III]

----

:Conditions: ``form`` set to "long", name-as-sort-order active,
             ``demote-non-dropping-particle`` set to "never"
             or "sort-only"
:Order:
    1) non-dropping-particle
    2) family
    3) suffix
    4) given
    5) dropping-particle

:Example: [la] [Martini�re] [III], [G�rard] [de] 

----

:Conditions: ``form`` set to "long", name-as-sort-order active,
             ``demote-non-dropping-particle`` set to 
             "display-and-sort"
:Order:
    1) family
    2) suffix
    3) given
    4) dropping-particle
    5) non-dropping-particle 

:Example: [Martini�re] [III], [G�rard] [de] [la]

----

:Conditions: ``form`` set to "short"
:Order:
    1) non-dropping-particles
    2) family
    3) suffix

:Example: [la] [Martini�re] [III]

----

**Sorting order of latin/Cyrillic names**

N.B. The sort keys are listed in descending order of importance.

----

:Conditions: ``demote-non-dropping-particle`` set to "never"

    1) non-dropping-particle + family
    2) dropping-particle
    3) given
    4) suffix

:Example: [la Martini�re] [de] [G�rard] [III]

----

:Conditions: ``demote-non-dropping-particle`` set to "sort-only" or "display-and-sort"

    1) family
    2) dropping-particle + non-dropping-particle
    3) given
    4) suffix

:Example: [Martini�re] [de la] [G�rard] [III]

----

**Display and sorting order of non-latin/Cyrillic names**

----

:Conditions: ``form`` set to "long"
:Order:
    1) family
    2) given

:Example: |Mao Zedong| [Mao Zedong]

.. |Mao Zedong| unicode:: U+6bdb U+6cfd U+4e1c

----

:Conditions: ``form`` set to "short"
:Order:
    1) family

:Example: |Mao| [Mao]

.. |Mao| unicode:: U+6bdb

----

Non-personal names lack name-parts and are sorted as is, although English
articles ("a", "an" and "the") at the start of the name are stripped. For
example, "The New York Times" sorts as "New York Times".

Name-part formatting
''''''''''''''''''''

The ``cs:name`` element may include one or two ``cs:name-part`` child elements.
These child elements accept the `formatting`_ and `text-case`_ attributes, which
allows for separate formatting of the different name parts (e.g. "Jane DOE", see
example below). The required ``name`` attribute on ``cs:name-part`` specifies
which name-parts are affected: when set to "given", the formatting only acts on
the "given" name-part. When set to "family", the formatting acts on the
"family", "dropping-particle" and "non-dropping-particle" name-parts (the
"suffix" name-part is not subject to any name-part formatting). The order of the
``cs:name-part`` elements does not affect which, and in what order, the
name-parts are rendered.

.. sourcecode:: xml

    <names variable="author">
      <name>
        <name-part name="family" text-case="uppercase">
      </name>
    </names>

Et-al
^^^^^

Et-al abbreviation, controlled via the et-al attributes on ``cs:name`` (see
`Name`_), can be further customized with the optional ``cs:et-al`` element,
which should be included directly after the ``cs:name`` element. The ``term``
attribute of this element can be set to either "et-al" (default) or to "and
others" to use either term (with this different et-al terms can be used for
citations and the bibliography). In addition, attributes for `affixes`_ and
`formatting`_ can be used, for example to italicize the et-al term:

.. sourcecode:: xml

    <names variable="author">
      <name/>
      <et-al term="and others" font-style="italic"/>
    </names>

Substitute
^^^^^^^^^^

The optional ``cs:substitute`` element, which should be included as the last
child element of ``cs:names``, controls substitution in case the `name
variables`_ specified in the parent ``cs:names`` element are empty. The
substitutions are specified as child elements of ``cs:substitute``, and can
consist of any of the standard `rendering elements`_ (with the exception of
``cs:layout``). It is also possible to use a shorthand version of ``cs:names``,
which doesn't allow for any child elements, and uses the attributes values set
on the ``cs:name`` and ``cs:et-al`` child elements of the original ``cs:names``
element. If ``cs:substitute`` contains multiple child elements, the first
element to return a non-empty result is used for substitution. Substituted
variables are repressed in the rest of the output to prevent duplication. An
example, where an empty "author" name variable is substituted by the "editor"
name variable, or, when no editors exist, by the "title" macro:

.. sourcecode:: xml

    <macro name="author">
      <names variable="author">
        <name/>
        <substitute>
          <names variable="editor"/>
          <text macro="title"/>
        </substitute>
      </names>
    </macro>

Label in ``cs:names``
^^^^^^^^^^^^^^^^^^^^^

The ``cs:label`` element, used to output text terms whose pluralization depends
on the contents of another variable (e.g. "(editors)" in "Doe and Smith
(editors)"), is discussed in detail in the `label`_ section. It should be
included after the ``cs:name`` and ``cs:et-al`` elements, but before the
``cs:substitute`` element. When used within ``cs:names``, the ``variable``
attribute should be omitted, as the value set on the parent ``cs:names`` element
is used.

Label
~~~~~

The Citation Style Language includes several variables that have matching terms.
The ``cs:label`` element can be used to render one of these terms, while
matching the term plurality with that of the corresponding variable. The
variable/term combination is selected with the ``variable`` attribute, which can
be set to either "page" or "locator". When ``cs:label`` is used as a child
element of ``cs:names``, the value of the ``variable`` attribute is
automatically inherited from the parent ``cs:names`` element. The example below
displays the "page" variable, using the singular form of the "page" term for a
single page ("page 5"), or the plural form for a page range ("pages 5-7").

.. sourcecode:: xml

    <group delimiter=" ">
      <label variable="page" form="long"/>
      <text variable="page"/>
    </group>

The ``cs:label`` element may carry attributes for `affixes`_, `formatting`_,
`text-case`_ and `strip-periods`_, as well as:

``form``
    Selects the form of the term, with possible values:
    
    -  "long": the default, e.g. "editor"/"editors" for the "editor" term
    -  "verb": e.g. "edited by" for the "editor" term
    -  "short": e.g. "ed"/"eds" for the "editor" term
    -  "verb-short": e.g. "ed" for the "editor" term
    -  "symbol": e.g. "�" for the singular "section" term

``plural``
    Sets pluralization of the term, with values:
    
    -  "contextual": the default, pluralization is dependent on the
       variable contents, e.g. "page 1" and "pages 1-3"
    -  "always": always use the plural form, e.g. "pages 1" and "pages 1-3"
    -  "never": always use the singular form, e.g. "page 1" and "page 1-3"

Group
~~~~~

The ``cs:group`` element may contain one or more `rendering elements`_ (not
``cs:layout``). ``cs:group`` itself may carry the `delimiter`_ attribute (to
delimit the enclosed elements) and the attributes for `affixes`_ (applied to the
group output as a whole), `display`_ and `formatting`_ (formatting settings are
transmitted to the enclosed elements). Note that ``cs:group`` implicitly acts as
a conditional: cs:group and its child elements are suppressed if a) at least one
rendering element in cs:group calls a variable (either directly or via a macro),
and b) all variables that are called are empty. This behavior exists to
accommodate descriptive cs:text elements. For example,

.. sourcecode:: xml

    <layout>
      <group prefix="(" suffix=")">
        <text value="Published by: "/>
        <text variable="publisher"/>
      </group>
    </layout>

results in "(Published by: Company A)" when the "publisher" variable is set to
"Company A", but doesn't generate output when the "publisher" variable is empty.

Choose
~~~~~~

The ``cs:choose`` element allows for the expression of conditional statements.
The first child element of ``cs:choose`` is always a ``cs:if`` child element. In
addition, any number of ``cs:else-if`` child elements may be included, as well
as a closing ``cs:else`` element. The ``cs:if`` and ``cs:else-if`` elements may
contain any number of `rendering elements`_ (with the exception of
``cs:layout``). The ``cs:else`` element should contain at least one rendering
element. An example of a conditional:

.. sourcecode:: xml

    <choose>
      <if type="book thesis" match="any">
        <text variable="title" font-style="italic">
      </if>
      <else-if type="chapter">
        <text variable="title" quotes="true">
      </else-if>
      <else>
        <text variable="title">
      </else>
    </choose>

Every ``cs:if`` and ``cs:else-if`` element must include at least one condition.
The different types of conditions, expressed as attributes, are:

``disambiguate``
    The contents of an <if disambiguate="true"> block is only rendered if it
    disambiguates two otherwise identical citations. This attempt at
    disambiguation will only be made when all other disambiguation methods have
    failed to uniquely identify the target source.

``is-numeric``
    Tests whether the given variables (`Appendix I - Variables`_) contain
    numeric data.
    
``is-uncertain-date``
    Tests whether the given `date variables`_ contain `uncertain dates`_.
    
``locator``
    Tests whether the locator matches the given locator variable subtype
    (see `Locators`_).

``position``
    Tests whether the position of the item cite matches the given positions. The
    different positions are (note on terminology: a *citation* refers to a
    citation group, which contains one or more *cites* to individual items):
    
    -  "first": the position of a cite that is the first to reference an item
    -  "ibid"/"ibid-with-locator"/"subsequent": a cite that references an
       earlier cited item always has the "subsequent" position. In special cases
       cites may have the "ibid" or "ibid-with-locator" position. These
       positions are only assigned when:
       
       a) the current cite immediately follows on another cite, within the
          same citation, that references the same item
            
       or
       
       b) the current cite is the first cite in the citation, and the previous
          citation includes a single cite that references the same item
            
       If either requirement is met, the presence of locators determines which
       position is assigned:

       - **Preceding cite does not have a locator**: if the current cite has a
         locator, the position of the current cite is "ibid-with-locator".
         Otherwise the position is "ibid".
       - **Preceding cite does have a locator**: if the current cite has the
         same locator, the position of the current cite is "ibid". If the
         locator differs the position is "ibid-with-locator". If the current
         cite lacks a locator the position is "subsequent".
         
    - "near-note": the position of a cite following another cite that references
      the same item. Both cites have to be located in foot or endnotes, and the
      distance between both cites may not exceed the maximum distance (measured
      in number of foot or endnotes) set with the ``near-note-distance`` option
      (see `Note Distance`_).
      
    Note that each cite can have multiple position values. Also, whenever
    position="ibid-with-locator" is true, position="ibid" is also true. And
    whenever position="ibid" or position="near-note" is true,
    position="subsequent" is also true.

``type``
    Tests whether the item matches the given types (`Appendix II - Types`_).

``variable``
    Tests whether the given variables (`Appendix I - Variables`_) contain
    non-empty values.

With the exception of ``disambiguate``, all the conditions may specify more than
one test value (variables, types, etc.), separated with spaces (e.g. "book
chapter"). In such cases the ``match`` attribute can be used as a logical
operator. The attribute can have the following values:

-  "all" (default): a condition tests "true" when it tests "true" for all of the
   given condition values
-  "any": a condition tests "true" when it tests "true" for any of the
   given condition values
-  "none": a condition tests "true" when it tests "true" for none of the
   given condition values

Style Behavior
--------------

Options
~~~~~~~

Styles can be extensively configured with (optional) options, which are set as
attributes. `Citation-specific options`_ are set on ``cs:citation``, while
`bibliography-specific options`_ are set on ``cs:bibliography``. `Global
options`_, which affect both citations and the bibliography, are set on
``cs:style``. `Inheritable name options`_ may be set on ``cs:style``,
``cs:citation`` and ``cs:bibliography``. Finally, `Locale Options`_ may be set
on ``cs:locale`` elements.

Citation-specific Options
^^^^^^^^^^^^^^^^^^^^^^^^^

Disambiguation
''''''''''''''

Disambiguation can be achieved in five ways:

1. The number of names shown can be increased.
2. A given name can be added.
3. Initialized given names can be expanded.
4. A year-suffix can be included.
5. The cite can be rendered with the ``disambiguate`` attribute of ``cs:choose``
   conditions testing "true".

Note that the term "disambiguation" in the statement above is itself ambiguous.
Steps (1), (4) and (5) aim solely to disambiguate cites that otherwise would be
the same. Steps (2) and (3), however, are different. In addition to the strict
purpose of disambiguating *cites*\ , the adding or expansion of given names may
be used for the broader purpose of disambiguating *names* throughout the
document. In the description below, this difference is referred to as "the scope
of names transformation".

The five potential steps to disambiguation are activated with the attributes
described in this section, and are always performed, if at all, in the order
listed below.

``disambiguate-add-names`` [Step (1)]
    If set to "true" ("false" is the default), names that would otherwise be
    hidden as a result of et-al abbreviation are added one by one, until either
    the target reference is uniquely identified, or all names are shown.

``disambiguate-add-givenname`` [Steps (2) & (3)]
    If set to "true" ("false" is the default), given names are added or
    expanded. For example:

    ================================  ===================================
    Original form                     Disambiguated form
    ================================  ===================================
    (Simpson 2005; Simpson 2005)      (H. Simpson 2005; B. Simpson 2005)
    (Doe 1950; Doe 1950)              (John Doe 1950; Jane Doe 1950)
    ================================  ===================================

    Note that the value of the ``givenname-disambiguation-rule`` attribute (the
    default is "all-names") determines a) the precise method of name expansion,
    and b) whether or not cites that are not themselves ambiguous but do contain
    the ambiguous name(s) are affected by this type of disambiguation.

``givenname-disambiguation-rule`` [Steps (2) & (3) supplemental]
    This attribute accepts one of five possible values, which vary in three
    respects: the scope of names transformation within the document; the steps
    included in the disambiguation attempt; and the names within a cite that are
    affected.

    **The scope of names transformation**
        With a value of "all-names", "all-names-with-initials", "primary-name",
        or "primary-name-with-initials", disambiguation is performed for all
        relevant names, without regard to ambiguity in individual cites.
        Transformations governed by these rules apply to all cites throughout
        the document. Disambiguation of cites is in this case incidental to the
        disambiguation of names.

        With a value of "by-cite", only the names within ambiguous cites are
        transformed, as required to discriminate between references. Cites that
        are not ambiguous are not affected.

    **Transformation steps**
          All five types of given name disambiguation follow the same general
          transformation steps (the specific steps applied depend on the value
          of ``givenname-disambiguation-rule``).

          1. If ``initialize-with`` is set, then:

             \(a) A ``form`` value of "short" can be incremented to "long" (e.g.
             "Doe" becomes "J. Doe").
             
             \(b) ``initialize-with`` can be ignored (e.g. "J. Doe" becomes
             "John Doe").

          2. If ``initialize-with`` is *not* set, then the ``form`` value of
             "short" can be immediately incremented to "long" (e.g. "Doe"
             becomes "John Doe").
    
    **Given name disambiguation rules**
        The effect of each given name disambiguation rule is described below. In
        all cases, transformations that do not contribute to disambiguation are
        omitted, and any names added by ``disambiguate-add-names`` that follow
        the name that results in success are discarded.

        "all-names"
            The default value. If a name is rendered the same in different cites
            (e.g. "Doe 2000" and "Doe 2001"), the name is progressively
            transformed until it can be distinguished from the others (e.g. "A.
            Doe 2000" and "B. Doe 2001"), or until the transformation steps are
            exhausted.

        "all-names-with-initials"
            Same as "all-names", but limited to step 1(a). If
            ``initialize-with`` is not set, no disambiguation attempt is made.

        "primary-name"
            Same as "all-names", but ambiguity is only checked for the
            first-listed name, and only first-listed names are affected by the
            transformation.

        "primary-name-with-initials"
            Same as "primary-name", but limited to step 1(a). If
            ``initialize-with`` is not set, no disambiguation attempt is made.

        "by-cite"
            Same as "all-names", but the transformation is limited to ambiguous
            cites. The appearance of the names transformed will not be affected
            in other cites.

``disambiguate-add-year-suffix`` [Step (4)]
    If set to "true" ("false" is the default), a year-suffix is added to cites
    that are otherwise identical (e.g. "Doe 2007, Doe 2007" becomes "Doe 2007a,
    Doe 2007b"). The placement of the year-suffix, which by default is appended
    to each cite, can be controlled by explictly rendering the "year-suffix"
    variable using ``cs:text``.

If ambiguous cites remain after the above steps have been exhausted, a final
attempt at disambiguation is performed with the ``disambiguate`` test value on
any ``cs:choose`` conditions testing "true" [Step (5)]. If this results in
successful disambiguation, any names added by ``disambiguate-add-names`` are
discarded.

Citation Collapsing
'''''''''''''''''''

``collapse``
    The collapse option activates citation collapsing. Note that "year-suffix"
    and "year-suffix-ranged" both fall back to "year" when the
    ``disambiguate-add-year-suffix`` attribute is not set to "true" (see
    `Disambiguation`_). Its possible values are:
    
    -  "citation-number": collapses numeric citation ranges (e.g. from "[1, 2,
       3, 5]" to "[1-3, 5]"). Note that only increasing ranges are collapsed,
       e.g. "[3, 2, 1]" will not collapse (to see how numeric styles can sort
       citations by the ``citation-number`` variable, see `Sorting`_).
    -  "year": when the names stored in the rendered name variables are the same
       for two subsequent cites, the latter cite is collapsed to only the year,
       e.g. from "(Doe 2000, Doe 2001)" to "(Doe 2000, 2001)".
    -  "year-suffix": collapses as "year", but also collapses identical years,
       e.g. "(Doe 2000a, b)" instead of "(Doe 2000a, 2000b)".
    -  "year-suffix-ranged": collapses as "year-suffix", but also
       collapses ranges of year-suffix markers, e.g. "(Doe 2000a-c,e)"
       instead of "(Doe 2000a, b, c, e)". 

``year-suffix-delimiter``
    Specifies the delimiter for year-suffix elements. For example, citations
    like "(Smith 1999a,b; 2000; Jones 2001)" are obtained when the ``collapse``
    attribute is set to "year-suffix", the ``delimiter`` on ``cs:layout`` in
    ``cs:citation`` is set to "; ", and the ``year-suffix-delimiter`` is set to
    ",". When the ``year-suffix-delimiter`` attribute is not set, year-suffixes
    are delimited with the delimiter set on ``cs:layout`` in ``cs:citation``.

``after-collapse-delimiter``
    Specifies the cite delimiter that should be used *after* a group of
    collapsed cites. For example, citations like "(Smith 1999a, b, 2000; Jones
    2001, Brown 2007)" are obtained when the ``collapse`` attribute is set to
    "year-suffix", the ``delimiter`` on ``cs:layout`` in ``cs:citation`` is set
    to ", " and ``after-collapse-delimiter`` is set to "; ".


Note Distance
'''''''''''''

``near-note-distance``
    The "near-note" position (see `Choose`_) tests "true" if a preceding
    note exists that: a) refers to the same item and b) has a distance (measured
    in footnotes or endnotes) to the current item that does not exceed the value
    of ``near-note-distance``. This attribute defaults to 5.

Bibliography-specific Options
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Whitespace
''''''''''

``hanging-indent``
    If set to "true" ("false" is the default), bibliographic entries are
    rendered with hanging-indents.

``second-field-align``
    If set to "flush", subsequent lines of each bibliography entry are aligned
    with the beginning of the second field. If set to "margin", the first field
    is put in the margin and all subsequent lines of text are aligned with the
    margin (as in the IEEE style). An example showing the alignment, if the
    first field is ``<text variable="citation-number" suffix=". "/>``:
    
    ::
    
        1. Adams, D. (2002). The Ultimate Hitchhiker's Guide to the
           Galaxy (1st ed.).

``line-spacing``
    Sets the spacing of lines (in units of lines, default is "1")

``entry-spacing``
    Sets the spacing of lines (in units of line-spacing, default is "1")

Reference Grouping
''''''''''''''''''

``subsequent-author-substitute``
    The value of the ``subsequent-author-substitute`` attribute (which may be
    any string) is used to replace the names in a bibliographic entry, when it
    shares these names with the preceding bibliographic entry. Note that only
    the first ``cs:names`` element rendered is affected. E.g., with
    ``subsequent-author-substitute`` set to "---":
    
    ::
    
        Asimov. Foundation, 1951.
        ---. Foundation and Empire, 1952.
        ---. Second Foundation, 1953.

Global Options
^^^^^^^^^^^^^^

Hyphenation of Initialized Names
''''''''''''''''''''''''''''''''

``initialize-with-hyphen``
    Specifies whether compound given names (e.g. "Jean-Luc") should be
    initialized with a hyphen ("J.-L.", value "true") or without ("J.L.", value
    "false"). Defaults to "true".

Page Ranges
'''''''''''

``page-range-format``
    The value of this attribute determines how page ranges are formatted.
    Available values: "expanded" (e.g. "321-328"), "minimal" ("321-8"), and
    "chicago" ("321-28") (see `Appendix IV - Page Abbreviation Rules`_ for the
    Chicago Manual of Style page range collapsing rules). If the attribute is
    not specified, the content of the page-field is left unchanged.

Name Particles
''''''''''''''

Many Western names include one or more name particles (e.g. "de" in the Dutch
name "W. de Koning"). However, not all particles are equal: name particles can
be either maintained or dropped when only the surname is shown (from now on we
will refer to these two types as non-dropping-particle and dropping-particle,
respectively). A single name can contain particles of both types (with the
non-dropping-particle always following the dropping-particle). For example, the
French name "G�rard de la Martini�re" can be deconstructed into:
    
    ::
    
        {
            "author": {
                "given": "G�rard",
                "dropping-particle": "de",
                "non-dropping-particle": "la",
                "family": "Martini�re"
            },
            {
                "given": "W.",
                "non-dropping-particle": "de",
                "family": "Koning"
            }
        }

When just the surname is shown, only the non-dropping-particle is kept: "La
Martini�re".

Whereas the dropping-particle is always treated the same, styles vary in how the
non-dropping-particle is handled in case of inverted names, where the family
name precedes the given name. First, the non-dropping-particle can be either
prepended to the family name (e.g. "de Koning, W.") or appended (after initials
or given names, e.g. "Koning, W. de"). Note that the dropping-particle is always
appended in inverted names. Secondly, if the choice has been made to prepend the
non-dropping-particle to the family name for inverted names, the author sort
order can differ. Either the non-dropping-particle remains part of the family
name (as part of the primary sort key; sort order A), or it may be separated
from the family name and become (part of) a secondary sort key, joining the
dropping-particle, if available (sort order B).

**Sort order A: non-dropping-particle not demoted**

-  primary sort key: "la Martini�re"
-  secondary sort key: "de"
-  tertiary sort key: "G�rard"

**Sort order B: non-dropping-particle demoted**

-  primary sort key: "Martini�re"
-  secondary sort key: "de la"
-  tertiary sort key: "G�rard"

Some names include a particle that should never be demoted. For these cases the
particle should just be included in the family name field, for example for the
French general Charles de Gaulle:

    ::
    
        {
            "author": {
                "family": "de Gaulle",
                "given": "Charles"
            } 
        }

The handling of particles for inverted names is set with the
``demote-non-dropping-particle`` option:

``demote-non-dropping-particle``
    Sets the display and sorting behavior of the non-dropping-particle in
    inverted names (e.g. "Koning, W. de"). The possible values are:
    
    -  "never": the non-dropping-particle is treated as part of the family name,
       whereas the dropping-particle is appended (e.g. "de Koning, W.", "la
       Martini�re, G�rard de"). The non-dropping-particle is part of the primary
       sort key (sort order A, e.g. "de Koning, W." appears under "D").
    -  "sort-only": same display behavior as "never", but the
       non-dropping-particle is demoted to a secondary sort key (see sort order
       B, e.g. "de Koning, W." appears under "K").
    -  "display-and-sort" (default): the dropping and non-dropping-particle are
       appended to the rest of the name (e.g. "Koning, W. de" and "Martini�re,
       G�rard de la"). When names are sorted, all particles are part of the
       secondary sort key (see sort order B, e.g. "Koning, W. de" appears under
       "K").

Inheritable Name Options
^^^^^^^^^^^^^^^^^^^^^^^^

Attributes for the ``cs:names`` and ``cs:name`` elements may also be set on
``cs:style``, ``cs:citation`` and ``cs:bibliography``. This eliminates the need
to repeat the same attributes and attribute values for every occurrence of the
``cs:names`` and ``cs:name`` elements.

The available inheritable attributes for ``cs:name`` are ``and``,
``delimiter-precedes-last``, ``et-al-min``, ``et-al-use-first``,
``et-al-subsequent-min``, ``et-al-subsequent-use-first``, ``initialize-with``,
``name-as-sort-order`` and ``sort-separator``. The attributes ``name-form`` and
``name-delimiter`` accompany the ``form`` and ``delimiter`` attributes on
``cs:name``. Similarly, ``names-delimiter``, the only inheritable attribute
available for ``cs:names``, accompanies the ``delimiter`` attribute on
``cs:names``.

When an inheritable name attribute is set on ``cs:style``, ``cs:citation`` or
``cs:bibliography``, its value is used for all ``cs:names`` elements within the
element carrying the attribute. When an element lower in the hierarchy includes
the same attribute with a different value, this latter value will override the
value(s) specified higher in the hierarchy.

Locale Options
^^^^^^^^^^^^^^

``punctuation-in-quote``
    Determines whether punctuation (commas and periods) is placed inside (value
    "true") or outside (default, value "false") quotation marks added with the
    ``quotes`` attribute (see `Formatting`_).

Sorting
~~~~~~~

The sort order for citations and the bibliography can be set with the
``cs:sort`` element in ``cs:citation`` and ``cs:bibliography``. If a style does
not include sorting instructions, references are listed in the order cited.

The ``cs:sort`` element must contain one or more ``cs:key`` child elements. The
sort key, set as an attribute on ``cs:key``, can be a ``variable`` (see
`Appendix I - Variables`_) or a ``macro``. The ``cs:key`` element may carry the
``sort`` attribute, with possible values of "ascending" (default) or
"descending", to indicate the sort order. The ``names-min`` and
``names-use-first`` attributes (which affect all names generated by macros
called by ``cs:key``) can be used to (further) constrain the number of names
used in the sort, overriding the values of the corresponding ``et-al-min`` and
``et-al-use-first`` and et-al-subsequent options.

Sort keys are evaluated one by one. The primary sort is performed using the
first sort key. A secondary sort (using the second sort key) is performed on
those items which share the first sort key. A tertiary sort (using the third
sort key) is performed on those items which share the first and second sort key.
This process continues until either the order of all items is fixed, or until
the sort keys are exhausted. Items for which a sort key is empty (including
empty date variables, where the "no date" term is substituted for rendering) are
placed at the end of the sort (both for ascending and descending sorts).

An example, where citations are first sorted by the output of the author macro
with overriding settings for et-al abbreviation. Entries that share the same
author macro output are further sorted in reverse order by date of issue.

.. sourcecode:: xml

    <citation>
      <sort>
        <key macro="author" names-min="3" names-use-first="3"/>
        <key variable="issued" sort="descending"/>
      </sort>
      <layout>
        <!-- rendering elements -->
      </layout>
    </citation>

The values returned for variables and macros called in ``cs:sort`` may differ
from the "ordinary" rendered values. These differences are detailed below.

Sorting Variables
^^^^^^^^^^^^^^^^^

When variables are referenced in ``cs:key`` via the ``variable`` attribute, the
string value is returned, without formatting decorations. Exceptions are name,
date and numeric variables, which are returned as follows:

**names:** `Name variables`_ can be set directly on ``cs:key`` using the
``variable`` attribute (e.g. ``<key variable="author"/>``). In this case, the
name-list from the variable will be returned as a string in the "long" ``form``
of ``cs:name``, formatted with ``name-as-sort-order`` set to "all".

**dates:** `Date variables`_ that are set directly on ``cs:key`` using the
``variable`` attribute are returned to ``cs:key`` in the YYYYMMDD format, with
zeros substituted for any missing date-parts (e.g. 20001200 for December 2000).
As a result, dates with more date-parts will come after those with fewer
date-parts, e.g. (2000, May 2000, May 1st 2000). Note that negative years are
sorted inversely, e.g. (100BC, 50BC, 50AD, 100AD). Seasons are ignored for
sorting, as the chronological order of the seasons differs between the northern
and southern hemispheres. Date ranges consist of a start date and an end date.
The start date is used for comparison with single dates. However, for items with
the same (start) date, the items with date ranges are placed after those with
single dates, e.g. (1999, 2000, 2000-2002, 2001, 2001-2003). In addition, date
ranges are subjected to a secondary sort based on the end date, e.g. (2000,
2000-2001, 2000-2004, 2000-2005, 2001).

**numbers:** If the ``variable`` attribute is used, numeric values are returned
as integers (``form`` is "numeric"). If the original variable value only
consists of non-numeric text, the value is returned as a text string.

Sorting Macros
^^^^^^^^^^^^^^

A macro called via ``cs:key`` returns whatever string value the macro would
ordinarily generate, with a few exceptions. In all cases, rich text markup is
removed from the sort key.

For name sorting, it is generally preferable to use the same macro that is used
to render the names in the context (``cs:citation`` or ``cs:bibliography``) to
which the sort applies. The first benefit of using macros is that substitution
logic becomes available (e.g. the ``editor`` variable might substitute for an
empty ``author`` variable). Secondly, et-al abbreviation can be used (using
either the ``et-al-min`` and ``et-al-use-first`` or et-al-subsequent options
defined within the macro, or the overriding ``names-min`` and
``names-use-first`` attributes set on ``cs:key``). Note that the "et-al" and
"and others" terms are not included in the sort key when et-al abbreviation
occurs. The third benefit is that names can be sorted by just the family name
and name particles, using a macro for which the ``form`` attribute on cs:name is
set to "short". Finally, it is possible to sort by the number of names in a
names-list, by calling a macro in which the ``form`` attribute of ``cs:name`` is
set to "count". In this case a count value of "3" would be obtained for a name
variable that would otherwise return "Jones, Smith, Doe". For name sorting, the
``name-as-sort-order`` attribute on ``cs:name`` elements is set to "all".

Number variables (rendered with ``cs:number``) and date variables are treated
the same as when they were called via ``variable``. The only exception is that
if a date variable is called by the ``variable`` attribute, the complete date is
returned. In contrast, macros return only those date-parts that would otherwise
be rendered (respecting the value of the ``date-parts`` attribute for localized
dates, or the listing of ``cs:date-part`` elements for non-localized dates).

Formatting
~~~~~~~~~~

The following formatting attributes may be set on ``cs:date``, ``cs:date-part``,
``cs:et-al``, ``cs:group``, ``cs:label``, ``cs:layout``, ``cs:name``,
``cs:name-part``, ``cs:names``, ``cs:number`` and ``cs:text``:

``font-style``
    Sets the font style, with values:
    
    -  "normal" (default)
    -  "italic"
    -  "oblique" (i.e. slanted)

``font-variant``
    Allows for the use of small capitals, with values:
    
    -  "normal" (default)
    -  "small-caps"

``font-weight``
    Sets the font weight, with values:
    
    -  "normal" (default)
    -  "bold"
    -  "light"

``text-decoration``
    Allows for the use of underlining, with values:
    
    -  "none" (default)
    -  "underline"

``vertical-align``
    Sets the vertical alignment, with values:
    
    -  "baseline" (default)
    -  "sup" (superscript)
    -  "sup" (subscript)

Affixes
~~~~~~~

The affixes attributes ``prefix`` and ``suffix`` may be set on ``cs:date``
(except when ``cs:date`` is used within ``cs:locale``), ``cs:date-part`` (except
when the parent ``cs:date`` element calls a localized date format),
``cs:et-al``, ``cs:group``, ``cs:label``, ``cs:layout``, ``cs:name``,
``cs:names``, ``cs:number`` and ``cs:text``. The attribute value is included
either before (``prefix``) or after (``suffix``) the displayed text. Affixes are
generally insensitive to the formatting attributes acting on the calling
element: the only exception to this rule are affixes set on ``cs:layout``. In
cases where formatting of affixes is desired, separate ``cs:text`` elements can
be used instead, with a ``value`` attribute to output verbatim text.

Delimiter
~~~~~~~~~

The ``delimiter`` attribute can be used to specify a delimiting string for
``cs:date`` (delimiting the date-parts; not allowed when ``cs:date`` calls a
localized date format), ``cs:names`` (delimiting multiple `name variables`_),
``cs:name`` (delimiting names in name lists), ``cs:group`` and ``cs:layout``
(both delimiting the direct child elements).

Display
~~~~~~~

Many of the anticipated output formats for CSL 1.0 (RTF, LaTeX, XML dialects
such as XHTML) allow styling to be applied to individual blocks of text in order
to control their appearance and position. The ``display`` attribute can be used
in ``cs:bibliography`` to allocate styling to particular text blocks for this
purpose [#]_. The attribute may be set on ``cs:date``, ``cs:group``,
``cs:names``, ``cs:number`` and ``cs:text`` elements, and accepts one of the
following values:

- "block": A block stretching from margin to margin.
- "left-margin": A block of fixed width starting at the left margin (all
  "left-margin" blocks in a bibliography share the same width, set according
  to the maximum number of characters appearing in any one such block).
- "right-inline": A block directly to the right of any immediately preceding
  "left-margin" block, and extending to the right margin.
- "indent": Block indented to the right by a standard amount.

.. [#] N.B. if ``display`` attributes are used, make sure all rendering
       elements are under the control of exactly one display attribute.

**Examples** 

(A) A similar effect as with ``second-field-align`` can be achieved with
    [#]_:
    
    .. sourcecode:: xml
    
        <bibliography>
          <layout>
            <text display="left-margin" variable="citation-number"
                prefix="[" suffix="]"/>
            <group display="right-inline">
              <!-- citation rendering elements -->
            </group>
          </layout>
        </bibliography>

.. [#] The styling definitions in the target application (CSS for HTML,
       styles for Word etc.) can be adjusted to achieve special effects,
       such as floating the labels into the margin.

----

(B) A per-author publication listing can be formatted as follows [#]_: 
    
    .. sourcecode:: xml
    
        <bibliography subsequent-author-substitute="">
          <sort>
            <key variable="author"/>
            <key variable="issued"/>
          </sort>
          <layout>
            <group display="block">
              <names variable="author"/>
            </group>
            <group display="left-margin">
              <date variable="issued">
                <date-part name="year" />
              </date>
            </group>
            <group display="right-inline">
              <text variable="title"/>
            </group>
          </layout>
        </bibliography>
    
    which would result in
    
    +-------------------+-----------------------+
    | Author1                                   |
    +-------------------+-----------------------+
    | year-publication1 | title-publication1    |
    +-------------------+-----------------------+
    | year-publication2 | title-publication2    |
    +-------------------+-----------------------+
    | Author2                                   |
    +-------------------+-----------------------+
    | year-publication3 | title-publication3    |
    +-------------------+-----------------------+
    | year-publication4 | title-publication4    |
    +-------------------+-----------------------+

.. [#] The effect of the empty ``subsequent-author-substitute`` attribute is
       to render the author name only once, at the top of the list of each
       author's publications.

----

(C) An annotated bibliography with the annotation block-indented below the
    reference can be formatted as follows:
    
    .. sourcecode:: xml
    
        <bibliography>
          <layout>
            <group display="block">
              <!-- citation rendering elements -->
            </group>
            <text display="indent" variable="abstract" />
          </layout>
        </bibliography>

Quotes
~~~~~~

The ``quotes`` attribute may set on ``cs:text``. When set to "true" ("false" is
default), the rendered text is wrapped in quotes. The quote-symbols are defined
as (localized) terms. The localized ``punctuation-in-quote`` option controls
whether punctuation appears inside or outside the quotes (see `Locale
Options`_).

Strip-periods
~~~~~~~~~~~~~

The ``strip-periods`` attribute may be set on ``cs:date-part`` (but only if
``name`` is set to "month"), ``cs:label`` and ``cs:text``. When set to "true"
("false" is the default), any periods in the rendered text are removed.

Text-case
~~~~~~~~~

The ``text-case`` attribute may be set on ``cs:date-part``, ``cs:label``,
``cs:name-part``, ``cs:number`` and ``cs:text`` and can be used to control the
text case of the rendered text. The possible values are:

-  "lowercase": displays all text in lowercase
-  "uppercase": displays all text in uppercase
-  "capitalize-first": capitalizes the first character; the case of other
   characters is not affected
-  "capitalize-all": capitalizes the first character of every word; other
   characters are displayed lowercase
-  "title": displays text in title case (the *Chicago Manual of Style* calls
   this "headline style")
-  "sentence": displays text in sentence case ("sentence style")

Appendices
----------

Appendix I - Variables
~~~~~~~~~~~~~~~~~~~~~~

Standard Variables
^^^^^^^^^^^^^^^^^^

-  abstract
-  annote
-  archive
-  archive\_location
-  archive-place
-  authority
-  call-number
-  chapter-number
-  citation-label
-  citation-number
-  collection-title
-  container-title
-  DOI
-  edition
-  event
-  event-place
-  first-reference-note-number
-  genre
-  ISBN
-  issue
-  jurisdiction
-  keyword
-  locator
-  medium
-  note
-  number
-  number-of-pages
-  number-of-volumes
-  original-publisher
-  original-publisher-place
-  original-title
-  page
-  page-first
-  publisher
-  publisher-place
-  references
-  section
-  status
-  title
-  URL
-  version
-  volume
-  year-suffix

Date Variables
^^^^^^^^^^^^^^

-  accessed
-  container
-  event-date
-  issued
-  original-date

Name Variables
^^^^^^^^^^^^^^

-  author
-  editor
-  translator
-  recipient
-  interviewer
-  publisher
-  composer
-  original-publisher
-  original-author
-  container-author (to be used when citing a section of a book,
   for example, to distinguish the author proper from the author of
   the containing work)
-  collection-editor (use for series editor)

Appendix II - Types
~~~~~~~~~~~~~~~~~~~

These are the different item types available within CSL:

-  article
-  article-magazine
-  article-newspaper
-  article-journal
-  bill
-  book
-  broadcast
-  chapter
-  entry
-  entry-dictionary
-  entry-encyclopedia
-  figure
-  graphic
-  interview
-  legislation
-  legal\_case
-  manuscript
-  map
-  motion\_picture
-  musical\_score
-  pamphlet
-  paper-conference
-  patent
-  post
-  post-weblog
-  personal\_communication
-  report
-  review
-  review-book
-  song
-  speech
-  thesis
-  treaty
-  webpage

Appendix III - Terms
~~~~~~~~~~~~~~~~~~~~

Categories
^^^^^^^^^^

-  anthropology
-  astronomy
-  biology
-  botany
-  chemistry
-  communications
-  engineering
-  generic-base - used for generic styles like Harvard and APA
-  geography
-  geology
-  history
-  humanities
-  law
-  linguistics
-  literature
-  math
-  medicine
-  philosophy
-  physics
-  political\_science
-  psychology
-  science
-  social\_science
-  sociology
-  theology
-  zoology

Locators
^^^^^^^^

-  book
-  chapter
-  column
-  figure
-  folio
-  issue
-  line
-  note
-  opus
-  page
-  paragraph
-  part
-  section
-  sub verbo
-  verse
-  volume

Months
^^^^^^

-  month-01
-  month-02
-  month-03
-  month-04
-  month-05
-  month-06
-  month-07
-  month-08
-  month-09
-  month-10
-  month-11
-  month-12

Ordinals
^^^^^^^^

-  ordinal-01
-  ordinal-02
-  ordinal-03
-  ordinal-04
-  long-ordinal-01
-  long-ordinal-02
-  long-ordinal-03
-  long-ordinal-04
-  long-ordinal-05
-  long-ordinal-06
-  long-ordinal-07
-  long-ordinal-08
-  long-ordinal-09
-  long-ordinal-10

Quotation marks
^^^^^^^^^^^^^^^

-  open-quote
-  close-quote
-  open-inner-quote
-  close-inner-quote

Roles
^^^^^

-  author
-  collection-editor
-  composer
-  container-author
-  editor
-  editorial-director
-  editortranslator
-  interviewer
-  original-author
-  recipient
-  translator

Seasons
^^^^^^^

-  season-01
-  season-02
-  season-03
-  season-04

Miscellaneous
^^^^^^^^^^^^^

-  accessed
-  ad
-  and
-  and others
-  anonymous
-  at
-  bc
-  by
-  circa
-  cited
-  edition
-  et-al
-  forthcoming
-  from
-  ibid
-  in
-  in press
-  internet
-  interview
-  letter
-  no date
-  online
-  presented at
-  reference
-  retrieved

Appendix IV - Page Abbreviation Rules
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The page abbreviation rules for the different values of the
``page-range-format`` attribute on ``cs:style`` are:

"minimum"
    All digits repeated in the second number are left out: 42-5, 321-8, 2787-816

"expanded"
    Abbreviated page ranges are expanded to their non-abbreviated form: 42-45,
    321-328, 2787-2816

"chicago"
    Page ranges are abbreviated according to the |link|
    `Chicago Manual of Style-rules <http://www.aahn.org/guidelines.html>`_:

Table: **Chicago Manual of Style page range abbreviation rules**

+------------------------+--------------------------+----------------+
| First number           | Second number            | Examples       |
+========================+==========================+================+
| Less than 100          | Use all digits           | 3-10; 71-72    |
+------------------------+--------------------------+----------------+
| 100 or multiple of 100 | Use all digits           | 100-104;       |
|                        |                          | 600-613;       |
|                        |                          | 1100-1123      |
+------------------------+--------------------------+----------------+
| 101 through 109 (in    | Use changed part only,   | 107-8; 505-17; |
| multiples of 100)      | omitting unneeded zeros  | 1002-6         |
+------------------------+--------------------------+----------------+
| 110 through 199 (in    | Use two digits, or more  | 321-25;        |
| multiples of 100)      | as needed                | 415-532;       |
|                        |                          | 11564-68;      |
|                        |                          | 13792-803      |
+------------------------+--------------------------+----------------+
| 4 digits               | If numbers are four      | 1496-1504;     |
|                        | digits long and three    | 2787-2816      |
|                        | digits change, use all   |                |
|                        | digits                   |                |
+------------------------+--------------------------+----------------+
