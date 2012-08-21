Translating CSL Locale Files
============================

.. contents:: **Table of Contents**
   :depth: 4

Preface
~~~~~~~

This document describes how you can help to improve the language support of
Citation Style Language (CSL) styles for your favorite language.

CSL styles can be bound to one particular language. For example, the British
Psychological Society CSL style will always use British English when generating
citations and bibliographies. It is also possible to allow styles to
automatically localize (an example is the Vancouver CSL style), e.g. to a user-
selected locale, or to the locale of the user's operating system.

CSL styles of both types rely on locale files for default localization data,
which consists of translations of words commonly used in citations and
bibliographies, localized date formats, and grammatical preferences. By storing
localization data in separate locale files, styles become more compact (although
styles can still provide their own localization data to override the defaults),
default localization data becomes easier to maintain, and styles themselves can
be (mostly) language-agnostic.

Below we will describe the structure of a locale file, give instructions on how
to translate all its parts, and explain how you can submit your contributions.

Getting Started
~~~~~~~~~~~~~~~

The CSL locale files are maintained in a GitHub repository at https://github.com
/citation-style-language/locales/. Each locale file contains the localization
data for one language. The file name of a locale file is always "locales-xx-
XX.xml", where "xx-XX" is a `BCP 47 language code
<http://people.w3.org/rishida/utils/subtags/index.php>`_ (e.g. the locale code
for British English is "en-GB"). The `repository wiki <https://github.com
/citation-style-language/locales/wiki>`_ contains a list of the existing locale
files, listing the locale code, language, and translation status.

If you find that a locale file already exists for your language, but that its
translations are inaccurate or incomplete, you can start translating that file.
If there is no locale file for your language, copy the "locales- en-US.xml" file
and start from there. Don't worry about finding the correct BCP 47 locale code
for a new language; we'll be happy to look it up when you submit your new locale
file.

Suggest text editor to use (plain text!)

Translating Locale Files
~~~~~~~~~~~~~~~~~~~~~~~~

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