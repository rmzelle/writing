Translating CSL Locale Files
============================

.. contents:: **Table of Contents**
   :depth: 4

Preface
~~~~~~~

This document describes how you can help us to improve the language support of
the Citation Style Language (CSL) by providing us with accurate localization
data for your language of choice.

CSL styles can be roughly divided into two classes. The first class contains the
styles that always generate output in one particular language. These include
most journal, publisher and institute-specific styles, such as the British
Psychological Society style, which uses British English. The second class
consists of popular styles that find use in many languages, such as the Chicago
Manual of Style styles.

CSL styles of both classes rely on locale files to provide default localization
data, which consists of translations of words commonly used in citations and
bibliographies, as well as localized date formats and grammatical preferences.
Storing localization data in separate files has several benefits: styles are
more compact (although styles can still provide their own localization data to
override the defaults), and styles themselves can be (mostly) language-agnostic.

Locale Files
~~~~~~~~~~~~

The CSL locale files are maintained in a Git repository at https://github.com
/citation-style-language/locales/. Each locale file contains the localization
data for one language. The file name of a locale file is always "locales-xx-
XX.xml", where "xx-XX" is a `BCP 47 language code
<http://people.w3.org/rishida/utils/subtags/index.php>`_ (e.g., the locale code
for British English is "en-GB"). The `repository wiki <https://github.com
/citation-style-language/locales/wiki>`_ contains a list for the existing locale
files, listing the locale code, language, and translation status.

If there is an incomplete locale file for your language, you can start
translating that file. If you cannot find a preexisting file, copy the "locales-
en-US.xml" file and start from there (if you have trouble finding the right
locale code for a new language, don't worry; we'll look it up when you submit
your locale file).

describe where to get styles, how to contribute translations

Date Formats
^^^^^^^^^^^^

Grammar Options
^^^^^^^^^^^^^^^

Terms
^^^^^

Ordinals
''''''''

Cover gender-variants and ordinal suffix term usage