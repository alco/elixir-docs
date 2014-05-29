Regex
==============================================================

.. elixir:module:: Regex

   :mtype: 

Overview
--------

Regular expressions for Elixir built on top of Erlang's ``re`` module.

As the ``re`` module, Regex is based on PCRE (Perl Compatible Regular
Expressions). More information can be found in the ```re``
documentation <http://www.erlang.org/doc/man/re.html>`__.

Regular expressions in Elixir can be created using :elixir:func:`Regex.compile!/2`
or using the special form with ```~r`` <Kernel.html#sigil_r/2>`__:

::

    # A simple regular expressions that matches foo anywhere in the string
    ~r/foo/

    # A regular expression with case insensitive and unicode options
    ~r/foo/iu

A Regex is represented internally as the :elixir:mod:`Regex` struct. Therefore,
``%Regex{}`` can be used whenever there is a need to match on them.

Modifiers
~~~~~~~~~

The modifiers available when creating a Regex are:

-  ``unicode`` (u) - enables unicode specific patterns like . it expects
   valid unicode strings to be given on match
-  ``caseless`` (i) - add case insensitivity
-  ``dotall`` (s) - causes dot to match newlines and also set newline to
   anycrlf. The new line setting can be overridden by setting ``(*CR)``
   or ``(*LF)`` or ``(*CRLF)`` or ``(*ANY)`` according to re
   documentation
-  ``multiline`` (m) - causes ``^`` and ``$`` to mark the beginning and
   end of each line. Use ``\A`` and ``\z`` to match the end or beginning
   of the string
-  ``extended`` (x) - whitespace characters are ignored except when
   escaped and allow ``#`` to delimit comments
-  ``firstline`` (f) - forces the unanchored pattern to match before or
   at the first newline, though the matched text may continue over the
   newline
-  ``ungreedy`` (r) - inverts the "greediness" of the regexp

The options not available are:

-  ``anchored`` - not available, use ``^`` or ``\A`` instead
-  ``dollar_endonly`` - not available, use ``\z`` instead
-  ``no_auto_capture`` - not available, use ``?:`` instead
-  ``newline`` - not available, use ``(*CR)`` or ``(*LF)`` or
   ``(*CRLF)`` or ``(*ANYCRLF)`` or ``(*ANY)`` at the beginning of the
   regexp according to the re documentation

Captures
~~~~~~~~

Many functions in this module allows what to capture in a regex match
via the ``:capture`` option. The supported values are:

-  ``:all`` - all captured subpatterns including the complete matching
   string. This is the default;

-  ``:first`` - only the first captured subpattern, which is always the
   complete matching part of the string. All explicitly captured
   subpatterns are discarded;

-  ``:all_but_first``- all but the first matching subpattern, i.e. all
   explicitly captured subpatterns, but not the complete matching part
   of the string;

-  ``:none`` - do not return matching subpatterns at all;

-  ``:all_names`` - captures all names in the Regex;

-  ``list(binary)`` - a list of named captures to capture;







Summary
-------

=============================== =
:elixir:func:`compile!/2`       Compiles the regular expression according to the given options. Fails with :elixir:mod:`Regex.CompileError` if the regex cannot be compiled 

:elixir:func:`compile/2`        Compiles the regular expression 

:elixir:func:`escape/1`         Escapes a string to be literally matched in a regex 

:elixir:func:`match?/2`         Returns a boolean indicating whether there was a match or not 

:elixir:func:`named_captures/3` Returns the given captures as a map or ``nil`` if no captures are found. The option ``:return`` can be set to ``:index`` to get indexes back 

:elixir:func:`names/1`          Returns a list of names in the regex 

:elixir:func:`opts/1`           Returns the regex options as a string 

:elixir:func:`re_pattern/1`     Returns the underlying ``re_pattern`` in the regular expression 

:elixir:func:`regex?/1`         Returns true if the given argument is a regex 

:elixir:func:`replace/4`        Receives a regex, a binary and a replacement, returns a new binary where the all matches are replaced by replacement 

:elixir:func:`run/3`            Runs the regular expression against the given string until the first match. It returns a list with all captures or ``nil`` if no match occurred 

:elixir:func:`scan/3`           Same as :elixir:func:`run/3`, but scans the target several times collecting all matches of the regular expression. A list of lists is returned, where each entry in the primary list represents a match and each entry in the secondary list represents the captured contents 

:elixir:func:`source/1`         Returns the regex source as a binary 

:elixir:func:`split/3`          Splits the given target into the number of parts specified 
=============================== =



Types
-----

.. elixir:type:: Regex.t/0

   :elixir:type:`t/0` :: %Regex{re_pattern: term, source: binary, opts: binary}
   





Functions
---------

.. elixir:function:: Regex.compile/2
   :sig: compile(source, options \\ "")


   Specs:
   
 
   * compile(binary, binary | [term]) :: {:ok, :elixir:type:`t/0`} | {:error, any}
 

   
   Compiles the regular expression.
   
   The given options can either be a binary with the characters
   representing the same regex options given to the ``~r`` sigil, or a list
   of options, as expected by the `Erlang ``re``
   docs <http://www.erlang.org/doc/man/re.html>`__.
   
   It returns ``{:ok, regex}`` in case of success, ``{:error, reason}``
   otherwise.
   
   **Examples**
   
   ::
   
       iex> Regex.compile("foo")
       {:ok, ~r"foo"}
   
       iex> Regex.compile("*foo")
       {:error, {'nothing to repeat', 0}}
   
   
   

.. elixir:function:: Regex.compile!/2
   :sig: compile!(source, options \\ "")


   
   Compiles the regular expression according to the given options. Fails
   with :elixir:mod:`Regex.CompileError` if the regex cannot be compiled.
   
   

.. elixir:function:: Regex.escape/1
   :sig: escape(string)


   Specs:
   
 
   * escape(:elixir:type:`String.t/0`) :: :elixir:type:`String.t/0`
 

   
   Escapes a string to be literally matched in a regex.
   
   **Examples**
   
   ::
   
       iex> Regex.escape(".")
       "\\."
   
       iex> Regex.escape("\\what if")
       "\\\\what\\ if"
   
   
   

.. elixir:function:: Regex.match?/2
   :sig: match?(regex, string)


   
   Returns a boolean indicating whether there was a match or not.
   
   **Examples**
   
   ::
   
       iex> Regex.match?(~r/foo/, "foo")
       true
   
       iex> Regex.match?(~r/foo/, "bar")
       false
   
   
   

.. elixir:function:: Regex.named_captures/3
   :sig: named_captures(regex, string, options \\ [])


   
   Returns the given captures as a map or ``nil`` if no captures are found.
   The option ``:return`` can be set to ``:index`` to get indexes back.
   
   **Examples**
   
   ::
   
       iex> Regex.named_captures(~r/c(?<foo>d)/, "abcd")
       %{"foo" => "d"}
   
       iex> Regex.named_captures(~r/a(?<foo>b)c(?<bar>d)/, "abcd")
       %{"bar" => "d", "foo" => "b"}
   
       iex> Regex.named_captures(~r/a(?<foo>b)c(?<bar>d)/, "efgh")
       nil
   
   
   

.. elixir:function:: Regex.names/1
   :sig: names(regex)


   
   Returns a list of names in the regex.
   
   **Examples**
   
   ::
   
       iex> Regex.names(~r/(?<foo>bar)/)
       ["foo"]
   
   
   

.. elixir:function:: Regex.opts/1
   :sig: opts(regex)


   
   Returns the regex options as a string.
   
   **Examples**
   
   ::
   
       iex> Regex.opts(~r(foo)m)
       "m"
   
   
   

.. elixir:function:: Regex.re_pattern/1
   :sig: re_pattern(regex)


   
   Returns the underlying ``re_pattern`` in the regular expression.
   
   

.. elixir:function:: Regex.regex?/1
   :sig: regex?(regex)


   
   Returns true if the given argument is a regex.
   
   **Examples**
   
   ::
   
       iex> Regex.regex?(~r/foo/)
       true
   
       iex> Regex.regex?(0)
       false
   
   
   

.. elixir:function:: Regex.replace/4
   :sig: replace(regex, string, replacement, options \\ [])


   
   Receives a regex, a binary and a replacement, returns a new binary where
   the all matches are replaced by replacement.
   
   The replacement can be either a string or a function. The string is used
   as a replacement for every match and it allows specific captures to be
   accessed via ``\N``, where ``N`` is the capture. In case ``\0`` is used,
   the whole match is inserted.
   
   When the replacement is a function, the function may have arity N where
   each argument maps to a capture, with the first argument being the whole
   match. If the function expects more arguments than captures found, the
   remaining arguments will receive ``""``.
   
   **Options**
   
   -  ``:global`` - when ``false``, replaces only the first occurrence
      (defaults to true)
   
   **Examples**
   
   ::
   
       iex> Regex.replace(~r/d/, "abc", "d")
       "abc"
   
       iex> Regex.replace(~r/b/, "abc", "d")
       "adc"
   
       iex> Regex.replace(~r/b/, "abc", "[\\0]")
       "a[b]c"
   
       iex> Regex.replace(~r/a(b|d)c/, "abcadc", "[\\1]")
       "[b][d]"
   
       iex> Regex.replace(~r/a(b|d)c/, "abcadc", fn _, x -> "[#{x}]" end)
       "[b][d]"
   
   
   

.. elixir:function:: Regex.run/3
   :sig: run(regex, string, options \\ [])


   
   Runs the regular expression against the given string until the first
   match. It returns a list with all captures or ``nil`` if no match
   occurred.
   
   **Options**
   
   -  ``:return`` - Set to ``:index`` to return indexes. Defaults to
      ``:binary``;
   -  ``:capture`` - What to capture in the result. Check the moduledoc for
      Regex to see the possible capture values;
   
   **Examples**
   
   ::
   
       iex> Regex.run(~r/c(d)/, "abcd")
       ["cd", "d"]
   
       iex> Regex.run(~r/e/, "abcd")
       nil
   
       iex> Regex.run(~r/c(d)/, "abcd", return: :index)
       [{2,2},{3,1}]
   
   
   

.. elixir:function:: Regex.scan/3
   :sig: scan(regex, string, options \\ [])


   
   Same as :elixir:func:`run/3`, but scans the target several times collecting all
   matches of the regular expression. A list of lists is returned, where
   each entry in the primary list represents a match and each entry in the
   secondary list represents the captured contents.
   
   **Options**
   
   -  ``:return`` - Set to ``:index`` to return indexes. Defaults to
      ``:binary``;
   -  ``:capture`` - What to capture in the result. Check the moduledoc for
      Regex to see the possible capture values;
   
   **Examples**
   
   ::
   
       iex> Regex.scan(~r/c(d|e)/, "abcd abce")
       [["cd", "d"], ["ce", "e"]]
   
       iex> Regex.scan(~r/c(?:d|e)/, "abcd abce")
       [["cd"], ["ce"]]
   
       iex> Regex.scan(~r/e/, "abcd")
       []
   
   
   

.. elixir:function:: Regex.source/1
   :sig: source(regex)


   
   Returns the regex source as a binary.
   
   **Examples**
   
   ::
   
       iex> Regex.source(~r(foo))
       "foo"
   
   
   

.. elixir:function:: Regex.split/3
   :sig: split(regex, string, options \\ [])


   
   Splits the given target into the number of parts specified.
   
   **Options**
   
   -  ``:parts`` - when specified, splits the string into the given number
      of parts. If not specified, ``:parts`` is defaulted to ``:infinity``,
      which will split the string into the maximum number of parts possible
      based on the given pattern.
   
   -  ``:trim`` - when true, remove blank strings from the result;
   
   **Examples**
   
   ::
   
       iex> Regex.split(~r/-/, "a-b-c")
       ["a","b","c"]
   
       iex> Regex.split(~r/-/, "a-b-c", [parts: 2])
       ["a","b-c"]
   
       iex> Regex.split(~r/-/, "abc")
       ["abc"]
   
       iex> Regex.split(~r//, "abc")
       ["a", "b", "c", ""]
   
       iex> Regex.split(~r//, "abc", trim: true)
       ["a", "b", "c"]
   
   
   







