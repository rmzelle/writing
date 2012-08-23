Translating CSL 1.0.1 Locale Files
==================================

.. contents:: **Table of Contents**
   :depth: 4

Preface
~~~~~~~

This document describes how you can help us improve the language support of
Citation Style Language (CSL) styles by translating the CSL locale file of your
favorite language.

CSL styles are either bound to one particular locale (e.g. the "British
Psychological Society" CSL style will always produce citations and
bibliographies in British English), or they (automatically) localize, e.g. to a
user-selected locale, or to the locale of the user's operating system.

All CSL styles, both those with and without a fixed locale, rely on locale files
for default localization data, which consists of translated terms commonly used
in citations and bibliographies, date formats, and grammar rules. Storing
localization data in separate files has several benefits: translations are
easier to maintain, styles are more compact (although styles can still include
their own localization data to override the defaults), and styles can be
(mostly) language-agnostic.

Below we will describe the structure of a locale file, give instructions on how
to translate all its parts, and explain how you can submit your translations.
See the `CSL specification
<http://citationstyles.org/downloads/specification.html>`_ for more in-depth
documentation on the structure and function of locale files.

Getting Started
~~~~~~~~~~~~~~~

The CSL locale files are kept in a GitHub repository at https://github.com
/citation-style-language/locales/.

Each locale file contains the localization data for one language. Locale files
are named "locales-xx-XX.xml", where "xx-XX" is a `BCP 47 language code
<http://people.w3.org/rishida/utils/subtags/index.php>`_ (e.g. the locale code
for British English is "en-GB"). The `repository wiki <https://github.com
/citation-style-language/locales/wiki>`_ lists the locale code, language, and
translation status of all locale files in the repository.

If you find that a locale file already exists for your language, but that its
translations are inaccurate or incomplete, you can start translating that file.
If there is no locale file for your language, copy the "locales-en-US.xml" file
and start from there. Don't worry about finding the correct BCP 47 locale code
for a new language; we'll be happy to look it up when you submit your new locale
file.

Modifications to existing locale files can be made directly via the GitHub
website. New locale files can be submitted as a "gist" or through a pull
request. For details, see the `instructions on submitting CSL styles
<https://github.com/citation-style-language/styles/wiki/Submitting-Styles>`_. If
you edit a locale file on your own computer, use a suitable plain text editor
(not a word processor).

Translating Locale Files
~~~~~~~~~~~~~~~~~~~~~~~~

When translating locale files, leave the overall structure of the locale file
untouched. It makes life easier for us if you don't remove existing elements,
introduce new ones, or move stuff around.

xml:lang
^^^^^^^^

At the top of the locale file you'll find the ``locale`` root element. It has an
attribute, ``xml:lang``. The value of this attribute ("en-US" in the example
below) should be set to the same language code used in the file name of the
locale file.

.. sourcecode:: xml

    <locale xmlns="http://purl.org/net/xbiblio/csl" version="1.0" xml:lang="en-US">


Locale File Metadata
^^^^^^^^^^^^^^^^^^^^

Directly below the ``locale`` root you'll find an ``info`` element. Here you can
list yourself as a translator using the ``translator`` element (and optionally
include contact information such as a website or email address). The ``rights``
element indicates under which license the locale file is released. All locale
files in our repository use the same Creative Commons license, so you don't have
to change anything here. The ``updated`` element is used to keep track of when
the locale file was last updated. Feel free to ignore it.

.. sourcecode:: xml

    <locale>
      <info>
        <translator>
          <name>John Doe</name>
          <email>john.doe@citationstyles.org</email>
          <uri>http://citationstyles.org/</uri>
        </translator>
        <rights license="http://creativecommons.org/licenses/by-sa/3.0/">This work is licensed under a Creative Commons Attribution-ShareAlike 3.0 License</rights>
        <updated>2012-07-04T23:31:02+00:00</updated>
      </info>
    </locale>

Date Formats
^^^^^^^^^^^^

Link to relevant section in CSL spec. Styles can use non-localizing and localizing dates. Every locale file should contain two date formats: text (long month form) and numeric.

Describe importance of using affixes/delimiter correctly, so dates gracefully degraded from year-month-day to year-month to year. Give bad and good example.

Grammar Options
^^^^^^^^^^^^^^^

Terms
^^^^^

Ordinals
''''''''

Cover gender-variants and ordinal suffix term usage

Submitting Contributions
~~~~~~~~~~~~~~~~~~~~~~~~

To submit changes to an existing locale file, or to submit a new locale file,
follow the `submission instructions for CSL styles <https://github.com/citation-
style-language/styles/wiki/Submitting-Styles>`_.

Questions?
~~~~~~~~~~

Post to the `Zotero forums <http://forums.zotero.org/11/>`_.