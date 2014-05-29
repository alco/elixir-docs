String
==============================================================

.. elixir:module:: String

   :mtype: 

Overview
--------

A String in Elixir is a UTF-8 encoded binary.

String and binary operations
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The functions in this module act according to the Unicode Standard,
version 6.3.0. For example, ```capitalize/1`` <#capitalize/1>`__,
```downcase/1`` <#downcase/1>`__, ```strip/1`` <#strip/1>`__ are
provided by this module.

In addition to this module, Elixir provides more low-level operations
that work directly with binaries. Some of those can be found in the
```Kernel`` <Kernel.html>`__ module, as:

-  ```Kernel.binary_part/3`` <Kernel.html#binary_part/3>`__ - retrieves
   part of the binary
-  ```Kernel.bit_size/1`` <Kernel.html#bit_size/1>`__ and
   ```Kernel.byte_size/1`` <Kernel.html#byte_size/1>`__ - size related
   functions
-  ```Kernel.is_bitstring/1`` <Kernel.html#is_bitstring/1>`__ and
   ```Kernel.is_binary/1`` <Kernel.html#is_binary/1>`__ - type checking
   function
-  Plus a number of functions for working with binaries (bytes) `in the
   ``:binary`` module <http://erlang.org/doc/man/binary.html>`__

Codepoints and graphemes
~~~~~~~~~~~~~~~~~~~~~~~~

As per the Unicode Standard, a codepoint is an Unicode Character, which
may be represented by one or more bytes. For example, the character "é"
is represented with two bytes:

::

    iex> byte_size("é")
    2

However, this module returns the proper length:

::

    iex> String.length("é")
    1

Furthermore, this module also presents the concept of graphemes, which
are multiple characters that may be "perceived as a single character" by
readers. For example, the same "é" character written above could be
represented by the letter "e" followed by the accent ́:

::

    iex> string = "\x{0065}\x{0301}"
    iex> byte_size(string)
    3
    iex> String.length(string)
    1

Although the example above is made of two characters, it is perceived by
users as one.

Graphemes can also be two characters that are interpreted as one by some
languages. For example, some languages may consider "ch" as a grapheme.
However, since this information depends on the locale, it is not taken
into account by this module.

In general, the functions in this module rely on the Unicode Standard,
but does not contain any of the locale specific behaviour.

More information about graphemes can be found in the `Unicode Standard
Annex #29 <http://www.unicode.org/reports/tr29/>`__. This current Elixir
version implements Extended Grapheme Cluster algorithm.

Integer codepoints
~~~~~~~~~~~~~~~~~~

Although codepoints could be represented as integers, this module
represents all codepoints as strings. For example:

::

    iex> String.codepoints("josé")
    ["j", "o", "s", "é"]

There are a couple of ways to retrieve a character integer codepoint.
One may use the ``?`` special macro:

::

    iex> ?j
    106

    iex> ?é
    233

Or also via pattern matching:

::

    iex> << eacute :: utf8 >> = "é"
    iex> eacute
    233

As we have seen above, codepoints can be inserted into a string by their
hexadecimal code:

::

    "jos\x{0065}\x{0301}" #=>
    "josé"

Self-synchronization
~~~~~~~~~~~~~~~~~~~~

The UTF-8 encoding is self-synchronizing. This means that if malformed
data (i.e., data that is not possible according to the definition of the
encoding) is encountered, only one codepoint needs to be rejected.

This module relies on this behaviour to ignore such invalid characters.
For example, ```length/1`` <#length/1>`__ is going to return a correct
result even if an invalid codepoint is fed into it.

In other words, this module expects invalid data to be detected when
retrieving data from the external source. For example, a driver that
reads strings from a database will be the one responsible to check the
validity of the encoding.





Summary
-------

================================= =
:elixir:func:`at/2`               Returns the grapheme in the ``position`` of the given utf8 ``string``. If ``position`` is greater than ``string`` length, than it returns ``nil`` 

:elixir:func:`capitalize/1`       Converts the first character in the given string to uppercase and the remaining to lowercase 

:elixir:func:`chunk/2`            Splits the string into chunks of characters that share a common trait 

:elixir:func:`codepoints/1`       Returns all codepoints in the string 

:elixir:func:`contains?/2`        Check if ``string`` contains any of the given ``contents`` 

:elixir:func:`downcase/1`         Convert all characters on the given string to lowercase 

:elixir:func:`duplicate/2`        Returns a binary ``subject`` duplicated ``n`` times 

:elixir:func:`ends_with?/2`       Returns ``true`` if ``string`` ends with any of the suffixes given, otherwise ``false``. ``suffixes`` can be either a single suffix or a list of suffixes 

:elixir:func:`first/1`            Returns the first grapheme from an utf8 string, nil if the string is empty 

:elixir:func:`graphemes/1`        Returns unicode graphemes in the string as per Extended Grapheme Cluster algorithm outlined in the `Unicode Standard Annex #29, Unicode Text Segmentation <http://www.unicode.org/reports/tr29/>`__ 

:elixir:func:`last/1`             Returns the last grapheme from an utf8 string, ``nil`` if the string is empty 

:elixir:func:`length/1`           Returns the number of unicode graphemes in an utf8 string 

:elixir:func:`ljust/2`            Returns a new string of length ``len`` with ``subject`` left justified and padded with ``padding``. If ``padding`` is not present, it defaults to whitespace. When ``len`` is less than the length of ``subject``, ``subject`` is returned 

:elixir:func:`ljust/3`            

:elixir:func:`lstrip/1`           Returns a string where leading Unicode whitespace has been removed 

:elixir:func:`lstrip/2`           Returns a string where leading ``char`` have been removed 

:elixir:func:`match?/2`           Check if ``string`` matches the given regular expression 

:elixir:func:`next_codepoint/1`   Returns the next codepoint in a String 

:elixir:func:`next_grapheme/1`    Returns the next grapheme in a String 

:elixir:func:`printable?/1`       Checks if a string is printable considering it is encoded as UTF-8. Returns ``true`` if so, ``false`` otherwise 

:elixir:func:`replace/4`          Returns a new binary based on ``subject`` by replacing the parts matching ``pattern`` by ``replacement``. By default, it replaces all entries, except if the ``global`` option is set to ``false`` 

:elixir:func:`reverse/1`          Reverses the given string. Works on graphemes 

:elixir:func:`rjust/2`            Returns a new string of length ``len`` with ``subject`` right justified and padded with ``padding``. If ``padding`` is not present, it defaults to whitespace. When ``len`` is less than the length of ``subject``, ``subject`` is returned 

:elixir:func:`rjust/3`            

:elixir:func:`rstrip/1`           Returns a string where trailing Unicode whitespace has been removed 

:elixir:func:`rstrip/2`           Returns a string where trailing ``char`` have been removed 

:elixir:func:`slice/2`            Returns a substring from the offset given by the start of the range to the offset given by the end of the range 

:elixir:func:`slice/3`            Returns a substring starting at the offset given by the first, and a length given by the second. If the offset is greater than string length, than it returns ``nil`` 

:elixir:func:`split/1`            Divides a string into substrings at each Unicode whitespace occurrence with leading and trailing whitespace ignored 

:elixir:func:`split/3`            Divides a string into substrings based on a pattern 

:elixir:func:`split_at/2`         Splits a string into two at the specified offset. When the offset given is negative, location is counted from the end of the string 

:elixir:func:`starts_with?/2`     Returns ``true`` if ``string`` starts with any of the prefixes given, otherwise ``false``. ``prefixes`` can be either a single prefix or a list of prefixes 

:elixir:func:`strip/1`            Returns a string where leading/trailing Unicode whitespace has been removed 

:elixir:func:`strip/2`            Returns a string where leading/trailing ``char`` have been removed 

:elixir:func:`to_atom/1`          Converts a string to an atom 

:elixir:func:`to_char_list/1`     Converts a string into a char list 

:elixir:func:`to_existing_atom/1` Converts a string to an existing atom 

:elixir:func:`to_float/1`         Returns a float whose text representation is ``string`` 

:elixir:func:`to_integer/1`       Returns a integer whose text representation is ``string`` 

:elixir:func:`to_integer/2`       Returns an integer whose text representation is ``string`` in base ``base`` 

:elixir:func:`upcase/1`           Convert all characters on the given string to uppercase 

:elixir:func:`valid?/1`           Checks whether ``str`` contains only valid characters 

:elixir:func:`valid_character?/1` Checks whether ``str`` is a valid character 
================================= =



Types
-----

.. elixir:type:: String.t/0

   :elixir:type:`t/0` :: binary
   

.. elixir:type:: String.codepoint/0

   :elixir:type:`codepoint/0` :: :elixir:type:`t/0`
   

.. elixir:type:: String.grapheme/0

   :elixir:type:`grapheme/0` :: :elixir:type:`t/0`
   





Functions
---------

.. elixir:function:: String.at/2
   :sig: at(string, position)


   Specs:
   
 
   * at(:elixir:type:`t/0`, integer) :: :elixir:type:`grapheme/0` | nil
 

   
   Returns the grapheme in the ``position`` of the given utf8 ``string``.
   If ``position`` is greater than ``string`` length, than it returns
   ``nil``.
   
   **Examples**
   
   ::
   
       iex> String.at("elixir", 0)
       "e"
   
       iex> String.at("elixir", 1)
       "l"
   
       iex> String.at("elixir", 10)
       nil
   
       iex> String.at("elixir", -1)
       "r"
   
       iex> String.at("elixir", -10)
       nil
   
   
   

.. elixir:function:: String.capitalize/1
   :sig: capitalize(string)


   Specs:
   
 
   * capitalize(:elixir:type:`t/0`) :: :elixir:type:`t/0`
 

   
   Converts the first character in the given string to uppercase and the
   remaining to lowercase.
   
   This relies on the titlecase information provided by the Unicode
   Standard. Note this function makes no attempt to capitalize all words in
   the string (usually known as titlecase).
   
   **Examples**
   
   ::
   
       iex> String.capitalize("abcd")
       "Abcd"
   
       iex> String.capitalize("ﬁn")
       "Fin"
   
       iex> String.capitalize("josé")
       "José"
   
   
   

.. elixir:function:: String.chunk/2
   :sig: chunk(string, trait)


   Specs:
   
 
   * chunk(:elixir:type:`t/0`, :valid | :printable) :: [:elixir:type:`t/0`]
 

   
   Splits the string into chunks of characters that share a common trait.
   
   The trait can be one of two options:
   
   -  ``:valid`` – the string is split into chunks of valid and invalid
      character sequences
   
   -  ``:printable`` – the string is split into chunks of printable and
      non-printable character sequences
   
   Returns a list of binaries each of which contains only one kind of
   characters.
   
   If the given string is empty, an empty list is returned.
   
   **Examples**
   
   ::
   
       iex> String.chunk(<<?a, ?b, ?c, 0>>, :valid)
       ["abc\000"]
   
       iex> String.chunk(<<?a, ?b, ?c, 0, 0x0ffff::utf8>>, :valid)
       ["abc\000", <<0x0ffff::utf8>>]
   
       iex> String.chunk(<<?a, ?b, ?c, 0, 0x0ffff::utf8>>, :printable)
       ["abc", <<0, 0x0ffff::utf8>>]
   
   
   

.. elixir:function:: String.codepoints/1
   :sig: codepoints(string)


   Specs:
   
 
   * codepoints(:elixir:type:`t/0`) :: [:elixir:type:`codepoint/0`]
 

   
   Returns all codepoints in the string.
   
   **Examples**
   
   ::
   
       iex> String.codepoints("josé")
       ["j", "o", "s", "é"]
   
       iex> String.codepoints("оптими зации")
       ["о","п","т","и","м","и"," ","з","а","ц","и","и"]
   
       iex> String.codepoints("ἅἪῼ")
       ["ἅ","Ἢ","ῼ"]
   
   
   

.. elixir:function:: String.contains?/2
   :sig: contains?(string, contents)


   Specs:
   
 
   * contains?(:elixir:type:`t/0`, :elixir:type:`t/0` | [:elixir:type:`t/0`]) :: boolean
 

   
   Check if ``string`` contains any of the given ``contents``.
   
   ``matches`` can be either a single string or a list of strings.
   
   **Examples**
   
   ::
   
       iex> String.contains? "elixir of life", "of"
       true
   
       iex> String.contains? "elixir of life", ["life", "death"]
       true
   
       iex> String.contains? "elixir of life", ["death", "mercury"]
       false
   
   
   

.. elixir:function:: String.downcase/1
   :sig: downcase(binary)


   Specs:
   
 
   * downcase(:elixir:type:`t/0`) :: :elixir:type:`t/0`
 

   
   Convert all characters on the given string to lowercase.
   
   **Examples**
   
   ::
   
       iex> String.downcase("ABCD")
       "abcd"
   
       iex> String.downcase("AB 123 XPTO")
       "ab 123 xpto"
   
       iex> String.downcase("JOSÉ")
       "josé"
   
   
   

.. elixir:function:: String.duplicate/2
   :sig: duplicate(subject, n)


   Specs:
   
 
   * duplicate(:elixir:type:`t/0`, pos_integer) :: :elixir:type:`t/0`
 

   
   Returns a binary ``subject`` duplicated ``n`` times.
   
   **Examples**
   
   ::
   
       iex> String.duplicate("abc", 0)
       ""
   
       iex> String.duplicate("abc", 1)
       "abc"
   
       iex> String.duplicate("abc", 2)
       "abcabc"
   
   
   

.. elixir:function:: String.ends_with?/2
   :sig: ends_with?(string, suffixes)


   Specs:
   
 
   * ends_with?(:elixir:type:`t/0`, :elixir:type:`t/0` | [:elixir:type:`t/0`]) :: boolean
 

   
   Returns ``true`` if ``string`` ends with any of the suffixes given,
   otherwise ``false``. ``suffixes`` can be either a single suffix or a
   list of suffixes.
   
   **Examples**
   
   ::
   
       iex> String.ends_with? "language", "age"
       true
   
       iex> String.ends_with? "language", ["youth", "age"]
       true
   
       iex> String.ends_with? "language", ["youth", "elixir"]
       false
   
   
   

.. elixir:function:: String.first/1
   :sig: first(string)


   Specs:
   
 
   * first(:elixir:type:`t/0`) :: :elixir:type:`grapheme/0` | nil
 

   
   Returns the first grapheme from an utf8 string, nil if the string is
   empty.
   
   **Examples**
   
   ::
   
       iex> String.first("elixir")
       "e"
   
       iex> String.first("եոգլի")
       "ե"
   
   
   

.. elixir:function:: String.graphemes/1
   :sig: graphemes(string)


   Specs:
   
 
   * graphemes(:elixir:type:`t/0`) :: [:elixir:type:`grapheme/0`]
 

   
   Returns unicode graphemes in the string as per Extended Grapheme Cluster
   algorithm outlined in the `Unicode Standard Annex #29, Unicode Text
   Segmentation <http://www.unicode.org/reports/tr29/>`__.
   
   **Examples**
   
   ::
   
       iex> String.graphemes("Ā̀stute")
       ["Ā̀","s","t","u","t","e"]
   
   
   

.. elixir:function:: String.last/1
   :sig: last(string)


   Specs:
   
 
   * last(:elixir:type:`t/0`) :: :elixir:type:`grapheme/0` | nil
 

   
   Returns the last grapheme from an utf8 string, ``nil`` if the string is
   empty.
   
   **Examples**
   
   ::
   
       iex> String.last("elixir")
       "r"
   
       iex> String.last("եոգլի")
       "ի"
   
   
   

.. elixir:function:: String.length/1
   :sig: length(string)


   Specs:
   
 
   * length(:elixir:type:`t/0`) :: non_neg_integer
 

   
   Returns the number of unicode graphemes in an utf8 string.
   
   **Examples**
   
   ::
   
       iex> String.length("elixir")
       6
   
       iex> String.length("եոգլի")
       5
   
   
   

.. elixir:function:: String.ljust/2
   :sig: ljust(subject, len)


   Specs:
   
 
   * ljust(:elixir:type:`t/0`, pos_integer) :: :elixir:type:`t/0`
 

   
   Returns a new string of length ``len`` with ``subject`` left justified
   and padded with ``padding``. If ``padding`` is not present, it defaults
   to whitespace. When ``len`` is less than the length of ``subject``,
   ``subject`` is returned.
   
   **Examples**
   
   ::
   
       iex> String.ljust("abc", 5)
       "abc  "
   
       iex> String.ljust("abc", 5, ?-)
       "abc--"
   
   
   

.. elixir:function:: String.ljust/3
   :sig: ljust(subject, len, padding)


   Specs:
   
 
   * ljust(:elixir:type:`t/0`, pos_integer, char) :: :elixir:type:`t/0`
 

   
   
   

.. elixir:function:: String.lstrip/1
   :sig: lstrip(binary)


   
   Returns a string where leading Unicode whitespace has been removed.
   
   **Examples**
   
   ::
   
       iex> String.lstrip("   abc  ")
       "abc  "
   
   
   

.. elixir:function:: String.lstrip/2
   :sig: lstrip(other, char)


   Specs:
   
 
   * lstrip(:elixir:type:`t/0`, char) :: :elixir:type:`t/0`
 

   
   Returns a string where leading ``char`` have been removed.
   
   **Examples**
   
   ::
   
       iex> String.lstrip("_  abc  _", ?_)
       "  abc  _"
   
   
   

.. elixir:function:: String.match?/2
   :sig: match?(string, regex)


   Specs:
   
 
   * match?(:elixir:type:`t/0`, :elixir:type:`Regex.t/0`) :: boolean
 

   
   Check if ``string`` matches the given regular expression.
   
   **Examples**
   
   ::
   
       iex> String.match?("foo", ~r/foo/)
       true
   
       iex> String.match?("bar", ~r/foo/)
       false
   
   
   

.. elixir:function:: String.next_codepoint/1
   :sig: next_codepoint(string)


   Specs:
   
 
   * next_codepoint(:elixir:type:`t/0`) :: {:elixir:type:`codepoint/0`, :elixir:type:`t/0`} | nil
 

   
   Returns the next codepoint in a String.
   
   The result is a tuple with the codepoint and the remaining of the string
   or ``nil`` in case the string reached its end.
   
   As with other functions in the String module, this function does not
   check for the validity of the codepoint. That said, if an invalid
   codepoint is found, it will be returned by this function.
   
   **Examples**
   
   ::
   
       iex> String.next_codepoint("josé")
       {"j", "osé"}
   
   
   

.. elixir:function:: String.next_grapheme/1
   :sig: next_grapheme(string)


   Specs:
   
 
   * next_grapheme(:elixir:type:`t/0`) :: {:elixir:type:`grapheme/0`, :elixir:type:`t/0`} | nil
 

   
   Returns the next grapheme in a String.
   
   The result is a tuple with the grapheme and the remaining of the string
   or ``nil`` in case the String reached its end.
   
   **Examples**
   
   ::
   
       iex> String.next_grapheme("josé")
       {"j", "osé"}
   
   
   

.. elixir:function:: String.printable?/1
   :sig: printable?(b)


   Specs:
   
 
   * printable?(:elixir:type:`t/0`) :: boolean
 

   
   Checks if a string is printable considering it is encoded as UTF-8.
   Returns ``true`` if so, ``false`` otherwise.
   
   **Examples**
   
   ::
   
       iex> String.printable?("abc")
       true
   
   
   

.. elixir:function:: String.replace/4
   :sig: replace(subject, pattern, replacement, options \\ [])


   Specs:
   
 
   * replace(:elixir:type:`t/0`, :elixir:type:`t/0`, :elixir:type:`t/0`, :elixir:type:`Keyword.t/0`) :: :elixir:type:`t/0`
 

   
   Returns a new binary based on ``subject`` by replacing the parts
   matching ``pattern`` by ``replacement``. By default, it replaces all
   entries, except if the ``global`` option is set to ``false``.
   
   A ``pattern`` may be a string or a regex.
   
   **Examples**
   
   ::
   
       iex> String.replace("a,b,c", ",", "-")
       "a-b-c"
   
       iex> String.replace("a,b,c", ",", "-", global: false)
       "a-b,c"
   
   The pattern can also be a regex. In those cases, one can give ``\N`` in
   the ``replacement`` string to access a specific capture in the regex:
   
   ::
   
       iex> String.replace("a,b,c", ~r/,(.)/, ",\\1\\1")
       "a,bb,cc"
   
   Notice we had to escape the escape character ``\``. By giving ``&``, one
   can inject the whole matched pattern in the replacement string.
   
   When strings are used as a pattern, a developer can also use the
   replaced part inside the ``replacement`` via the ``:insert_replaced``
   option:
   
   ::
   
       iex> String.replace("a,b,c", "b", "[]", insert_replaced: 1)
       "a,[b],c"
   
       iex> String.replace("a,b,c", ",", "[]", insert_replaced: 2)
       "a[],b[],c"
   
       iex> String.replace("a,b,c", ",", "[]", insert_replaced: [1, 1])
       "a[,,]b[,,]c"
   
   
   

.. elixir:function:: String.reverse/1
   :sig: reverse(string)


   Specs:
   
 
   * reverse(:elixir:type:`t/0`) :: :elixir:type:`t/0`
 

   
   Reverses the given string. Works on graphemes.
   
   **Examples**
   
   ::
   
       iex> String.reverse("abcd")
       "dcba"
   
       iex> String.reverse("hello world")
       "dlrow olleh"
   
       iex> String.reverse("hello ∂og")
       "go∂ olleh"
   
   
   

.. elixir:function:: String.rjust/2
   :sig: rjust(subject, len)


   Specs:
   
 
   * rjust(:elixir:type:`t/0`, pos_integer) :: :elixir:type:`t/0`
 

   
   Returns a new string of length ``len`` with ``subject`` right justified
   and padded with ``padding``. If ``padding`` is not present, it defaults
   to whitespace. When ``len`` is less than the length of ``subject``,
   ``subject`` is returned.
   
   **Examples**
   
   ::
   
       iex> String.rjust("abc", 5)
       "  abc"
   
       iex> String.rjust("abc", 5, ?-)
       "--abc"
   
   
   

.. elixir:function:: String.rjust/3
   :sig: rjust(subject, len, padding)


   Specs:
   
 
   * rjust(:elixir:type:`t/0`, pos_integer, char) :: :elixir:type:`t/0`
 

   
   
   

.. elixir:function:: String.rstrip/1
   :sig: rstrip(binary)


   Specs:
   
 
   * rstrip(:elixir:type:`t/0`) :: :elixir:type:`t/0`
 

   
   Returns a string where trailing Unicode whitespace has been removed.
   
   **Examples**
   
   ::
   
       iex> String.rstrip("   abc  ")
       "   abc"
   
   
   

.. elixir:function:: String.rstrip/2
   :sig: rstrip(string, char)


   Specs:
   
 
   * rstrip(:elixir:type:`t/0`, char) :: :elixir:type:`t/0`
 

   
   Returns a string where trailing ``char`` have been removed.
   
   **Examples**
   
   ::
   
       iex> String.rstrip("   abc _", ?_)
       "   abc "
   
   
   

.. elixir:function:: String.slice/2
   :sig: slice(string, range)


   Specs:
   
 
   * slice(:elixir:type:`t/0`, :elixir:type:`Range.t/0`) :: :elixir:type:`t/0` | nil
 

   
   Returns a substring from the offset given by the start of the range to
   the offset given by the end of the range.
   
   If the start of the range is not a valid offset for the given string or
   if the range is in reverse order, returns ``nil``.
   
   **Examples**
   
   ::
   
       iex> String.slice("elixir", 1..3)
       "lix"
   
       iex> String.slice("elixir", 1..10)
       "lixir"
   
       iex> String.slice("elixir", 10..3)
       nil
   
       iex> String.slice("elixir", -4..-1)
       "ixir"
   
       iex> String.slice("elixir", 2..-1)
       "ixir"
   
       iex> String.slice("elixir", -4..6)
       "ixir"
   
       iex> String.slice("elixir", -1..-4)
       nil
   
       iex> String.slice("elixir", -10..-7)
       nil
   
       iex> String.slice("a", 0..1500)
       "a"
   
       iex> String.slice("a", 1..1500)
       ""
   
       iex> String.slice("a", 2..1500)
       nil
   
   
   

.. elixir:function:: String.slice/3
   :sig: slice(string, start, len)


   Specs:
   
 
   * slice(:elixir:type:`t/0`, integer, integer) :: :elixir:type:`grapheme/0` | nil
 

   
   Returns a substring starting at the offset given by the first, and a
   length given by the second. If the offset is greater than string length,
   than it returns ``nil``.
   
   **Examples**
   
   ::
   
       iex> String.slice("elixir", 1, 3)
       "lix"
   
       iex> String.slice("elixir", 1, 10)
       "lixir"
   
       iex> String.slice("elixir", 10, 3)
       nil
   
       iex> String.slice("elixir", -4, 4)
       "ixir"
   
       iex> String.slice("elixir", -10, 3)
       nil
   
       iex> String.slice("a", 0, 1500)
       "a"
   
       iex> String.slice("a", 1, 1500)
       ""
   
       iex> String.slice("a", 2, 1500)
       nil
   
   
   

.. elixir:function:: String.split/1
   :sig: split(binary)


   Specs:
   
 
   * split(:elixir:type:`t/0`) :: [:elixir:type:`t/0`]
 

   
   Divides a string into substrings at each Unicode whitespace occurrence
   with leading and trailing whitespace ignored.
   
   **Examples**
   
   ::
   
       iex> String.split("foo bar")
       ["foo", "bar"]
   
       iex> String.split("foo" <> <<194, 133>> <> "bar")
       ["foo", "bar"]
   
       iex> String.split(" foo bar ")
       ["foo", "bar"]
   
   
   

.. elixir:function:: String.split/3
   :sig: split(binary, pattern, options \\ [])


   Specs:
   
 
   * split(:elixir:type:`t/0`, :elixir:type:`t/0` | [:elixir:type:`t/0`] | :elixir:type:`Regex.t/0`, :elixir:type:`Keyword.t/0`) :: [:elixir:type:`t/0`]
 

   
   Divides a string into substrings based on a pattern.
   
   Returns a list of these substrings. The pattern can be a string, a list
   of strings or a regular expression.
   
   The string is split into as many parts as possible by default, but can
   be controlled via the ``parts: num`` option. If you pass
   ``parts: :infinity``, it will return all possible parts.
   
   Empty strings are only removed from the result if the ``trim`` option is
   set to ``true``.
   
   **Examples**
   
   Splitting with a string pattern:
   
   ::
   
       iex> String.split("a,b,c", ",")
       ["a", "b", "c"]
   
       iex> String.split("a,b,c", ",", parts: 2)
       ["a", "b,c"]
   
       iex> String.split(" a b c ", " ", trim: true)
       ["a", "b", "c"]
   
   A list of patterns:
   
   ::
   
       iex> String.split("1,2 3,4", [" ", ","])
       ["1", "2", "3", "4"]
   
   A regular expression:
   
   ::
   
       iex> String.split("a,b,c", ~r{,})
       ["a", "b", "c"]
   
       iex> String.split("a,b,c", ~r{,}, parts: 2)
       ["a", "b,c"]
   
       iex> String.split(" a b c ", ~r{\s}, trim: true)
       ["a", "b", "c"]
   
   Splitting on empty patterns returns codepoints:
   
   ::
   
       iex> String.split("abc", ~r{})
       ["a", "b", "c", ""]
   
       iex> String.split("abc", "")
       ["a", "b", "c", ""]
   
       iex> String.split("abc", "", trim: true)
       ["a", "b", "c"]
   
       iex> String.split("abc", "", parts: 2)
       ["a", "bc"]
   
   
   

.. elixir:function:: String.split_at/2
   :sig: split_at(string, offset)


   Specs:
   
 
   * split_at(:elixir:type:`t/0`, integer) :: {:elixir:type:`t/0`, :elixir:type:`t/0`}
 

   
   Splits a string into two at the specified offset. When the offset given
   is negative, location is counted from the end of the string.
   
   The offset is capped to the length of the string.
   
   Returns a tuple with two elements.
   
   **Examples**
   
   ::
   
       iex> String.split_at "sweetelixir", 5
       {"sweet", "elixir"}
   
       iex> String.split_at "sweetelixir", -6
       {"sweet", "elixir"}
   
       iex> String.split_at "abc", 0
       {"", "abc"}
   
       iex> String.split_at "abc", 1000
       {"abc", ""}
   
       iex> String.split_at "abc", -1000
       {"", "abc"}
   
   
   

.. elixir:function:: String.starts_with?/2
   :sig: starts_with?(string, prefixes)


   Specs:
   
 
   * starts_with?(:elixir:type:`t/0`, :elixir:type:`t/0` | [:elixir:type:`t/0`]) :: boolean
 

   
   Returns ``true`` if ``string`` starts with any of the prefixes given,
   otherwise ``false``. ``prefixes`` can be either a single prefix or a
   list of prefixes.
   
   **Examples**
   
   ::
   
       iex> String.starts_with? "elixir", "eli"
       true
   
       iex> String.starts_with? "elixir", ["erlang", "elixir"]
       true
   
       iex> String.starts_with? "elixir", ["erlang", "ruby"]
       false
   
   
   

.. elixir:function:: String.strip/1
   :sig: strip(string)


   Specs:
   
 
   * strip(:elixir:type:`t/0`) :: :elixir:type:`t/0`
 

   
   Returns a string where leading/trailing Unicode whitespace has been
   removed.
   
   **Examples**
   
   ::
   
       iex> String.strip("   abc  ")
       "abc"
   
   
   

.. elixir:function:: String.strip/2
   :sig: strip(string, char)


   Specs:
   
 
   * strip(:elixir:type:`t/0`, char) :: :elixir:type:`t/0`
 

   
   Returns a string where leading/trailing ``char`` have been removed.
   
   **Examples**
   
   ::
   
       iex> String.strip("a  abc  a", ?a)
       "  abc  "
   
   
   

.. elixir:function:: String.to_atom/1
   :sig: to_atom(string)


   Specs:
   
 
   * to_atom(:elixir:type:`String.t/0`) :: atom
 

   
   Converts a string to an atom.
   
   Currently Elixir does not support conversions from strings which
   contains Unicode codepoints greater than 0xFF.
   
   Inlined by the compiler.
   
   **Examples**
   
   ::
   
       iex> String.to_atom("my_atom")
       :my_atom
   
   
   

.. elixir:function:: String.to_char_list/1
   :sig: to_char_list(string)


   Specs:
   
 
   * to_char_list(:elixir:type:`t/0`) :: char_list
 

   
   Converts a string into a char list.
   
   **Examples**
   
   ::
   
       iex> String.to_char_list("æß")
       'æß'
   
   Notice that this function expect a list of integer representing UTF-8
   codepoints. If you have a raw binary, you must instead use `the
   ``:binary`` module <http://erlang.org/doc/man/binary.html>`__.
   
   

.. elixir:function:: String.to_existing_atom/1
   :sig: to_existing_atom(string)


   Specs:
   
 
   * to_existing_atom(:elixir:type:`String.t/0`) :: atom
 

   
   Converts a string to an existing atom.
   
   Currently Elixir does not support conversions from strings which
   contains Unicode codepoints greater than 0xFF.
   
   Inlined by the compiler.
   
   **Examples**
   
   ::
   
       iex> :my_atom
       iex> String.to_existing_atom("my_atom")
       :my_atom
   
       iex> String.to_existing_atom("this_atom_will_never_exist")
       ** (ArgumentError) argument error
   
   
   

.. elixir:function:: String.to_float/1
   :sig: to_float(string)


   Specs:
   
 
   * to_float(:elixir:type:`String.t/0`) :: float
 

   
   Returns a float whose text representation is ``string``.
   
   Inlined by the compiler.
   
   **Examples**
   
   ::
   
       iex> String.to_float("2.2017764e+0")
       2.2017764
   
   
   

.. elixir:function:: String.to_integer/1
   :sig: to_integer(string)


   Specs:
   
 
   * to_integer(:elixir:type:`String.t/0`) :: integer
 

   
   Returns a integer whose text representation is ``string``.
   
   Inlined by the compiler.
   
   **Examples**
   
   ::
   
       iex> String.to_integer("123")
       123
   
   
   

.. elixir:function:: String.to_integer/2
   :sig: to_integer(string, base)


   Specs:
   
 
   * to_integer(:elixir:type:`String.t/0`, pos_integer) :: integer
 

   
   Returns an integer whose text representation is ``string`` in base
   ``base``.
   
   Inlined by the compiler.
   
   **Examples**
   
   ::
   
       iex> String.to_integer("3FF", 16)
       1023
   
   
   

.. elixir:function:: String.upcase/1
   :sig: upcase(binary)


   Specs:
   
 
   * upcase(:elixir:type:`t/0`) :: :elixir:type:`t/0`
 

   
   Convert all characters on the given string to uppercase.
   
   **Examples**
   
   ::
   
       iex> String.upcase("abcd")
       "ABCD"
   
       iex> String.upcase("ab 123 xpto")
       "AB 123 XPTO"
   
       iex> String.upcase("josé")
       "JOSÉ"
   
   
   

.. elixir:function:: String.valid?/1
   :sig: valid?(arg1)


   Specs:
   
 
   * valid?(:elixir:type:`t/0`) :: boolean
 

   
   Checks whether ``str`` contains only valid characters.
   
   **Examples**
   
   ::
   
       iex> String.valid?("a")
       true
   
       iex> String.valid?("ø")
       true
   
       iex> String.valid?(<<0xffff :: 16>>)
       false
   
       iex> String.valid?("asd" <> <<0xffff :: 16>>)
       false
   
   
   

.. elixir:function:: String.valid_character?/1
   :sig: valid_character?(codepoint)


   Specs:
   
 
   * valid_character?(:elixir:type:`t/0`) :: boolean
 

   
   Checks whether ``str`` is a valid character.
   
   All characters are codepoints, but some codepoints are not valid
   characters. They may be reserved, private, or other.
   
   More info at:
   http://en.wikipedia.org/wiki/Mapping\_of\_Unicode\_characters#Noncharacters
   
   **Examples**
   
   ::
   
       iex> String.valid_character?("a")
       true
   
       iex> String.valid_character?("ø")
       true
   
       iex> String.valid_character?("\x{ffff}")
       false
   
   
   







