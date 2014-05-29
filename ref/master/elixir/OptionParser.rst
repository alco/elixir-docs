OptionParser
==============================================================

.. elixir:module:: OptionParser

   :mtype: 

Overview
--------

This module contains functions to parse command line arguments.





Summary
-------

=========================== =
:elixir:func:`next/2`       Low-level function that parses one option 

:elixir:func:`parse/2`      Parses ``argv`` into a keywords list 

:elixir:func:`parse_head/2` Similar to ```parse/2`` <#parse/2>`__ but only parses the head of ``argv``; as soon as it finds a non-switch, it stops parsing 
=========================== =



Types
-----

.. elixir:type:: OptionParser.argv/0

   :elixir:type:`argv/0` :: [:elixir:type:`String.t/0`]
   

.. elixir:type:: OptionParser.parsed/0

   :elixir:type:`parsed/0` :: :elixir:type:`Keyword.t/0`
   

.. elixir:type:: OptionParser.errors/0

   :elixir:type:`errors/0` :: [{:elixir:type:`String.t/0`, :elixir:type:`String.t/0` | nil}]
   

.. elixir:type:: OptionParser.options/0

   :elixir:type:`options/0` :: [switches: :elixir:type:`Keyword.t/0`, strict: :elixir:type:`Keyword.t/0`, aliases: :elixir:type:`Keyword.t/0`]
   





Functions
---------

.. elixir:function:: OptionParser.next/2
   :sig: next(argv, opts \\ [])


   Specs:
   
 
   * next(:elixir:type:`argv/0`, :elixir:type:`options/0`) :: {:ok, key :: atom, value :: term, :elixir:type:`argv/0`} | {:invalid, key :: atom, value :: term, :elixir:type:`argv/0`} | {:undefined, key :: atom, value :: term, :elixir:type:`argv/0`} | {:error, :elixir:type:`argv/0`}
 

   
   Low-level function that parses one option.
   
   It accepts the same options as ```parse/2`` <#parse/2>`__ and
   ```parse_head/2`` <#parse_head/2>`__ as both functions are built on top
   of next. This function may return:
   
   -  ``{:ok, key, value, rest}`` - the option ``key`` with ``value`` was
      successfully parsed
   
   -  ``{:invalid, key, value, rest}`` - the option ``key`` is invalid with
      ``value`` (returned when the switch type does not match the one given
      via the command line)
   
   -  ``{:undefined, key, value, rest}`` - the option ``key`` is undefined
      (returned on strict cases and the switch is unknown)
   
   -  ``{:error, rest}`` - there are no switches at the top of the given
      argv
   
   
   
   

.. elixir:function:: OptionParser.parse/2
   :sig: parse(argv, opts \\ [])


   Specs:
   
 
   * parse(:elixir:type:`argv/0`, :elixir:type:`options/0`) :: {:elixir:type:`parsed/0`, :elixir:type:`argv/0`, :elixir:type:`errors/0`}
 

   
   Parses ``argv`` into a keywords list.
   
   It returns the parsed values, remaining arguments and the invalid
   options.
   
   **Examples**
   
   ::
   
       iex> OptionParser.parse(["--debug"])
       {[debug: true], [], []}
   
       iex> OptionParser.parse(["--source", "lib"])
       {[source: "lib"], [], []}
   
       iex> OptionParser.parse(["--source-path", "lib", "test/enum_test.exs", "--verbose"])
       {[source_path: "lib", verbose: true], ["test/enum_test.exs"], []}
   
   By default, Elixir will try to automatically parse switches. Switches
   without an argument, like ``--debug`` will automatically be set to true.
   Switches followed by a value will be assigned to the value, always as
   strings.
   
   Note Elixir also converts the switches to underscore atoms, as
   ``--source-path`` becomes ``:source_path``, to better suit Elixir
   conventions.
   
   **Switches**
   
   Many times though, it is better to explicitly list the available
   switches and their formats. The switches can be specified via two
   different options:
   
   -  ``:strict`` - the switches are strict. Any switch that does not exist
      in the switch list is treated as an error;
   
   -  ``:switches`` - configure some switches. Switches that does not exist
      in the switch list are still attempted to be parsed;
   
   Note only ``:strict`` or ``:switches`` may be given at once.
   
   For each switch, the following types are supported:
   
   -  ``:boolean`` - Marks the given switch as a boolean. Boolean switches
      never consume the following value unless it is ``true`` or ``false``;
   -  ``:integer`` - Parses the switch as an integer;
   -  ``:float`` - Parses the switch as a float;
   -  ``:string`` - Returns the switch as a string;
   
   If a switch can't be parsed or is not specfied in the strict case, the
   option is returned in the invalid options list (third element of the
   returned tuple).
   
   The following extra "types" are supported:
   
   -  ``:keep`` - Keeps duplicated items in the list instead of overriding;
   
   Examples:
   
   ::
   
       iex> OptionParser.parse(["--unlock", "path/to/file"], strict: [unlock: :boolean])
       {[unlock: true], ["path/to/file"], []}
   
       iex> OptionParser.parse(["--unlock", "--limit", "0", "path/to/file"],
       ...>                    strict: [unlock: :boolean, limit: :integer])
       {[unlock: true, limit: 0], ["path/to/file"], []}
   
       iex> OptionParser.parse(["--limit", "3"], strict: [limit: :integer])
       {[limit: 3], [], []}
   
       iex> OptionParser.parse(["--limit", "xyz"], strict: [limit: :integer])
       {[], [], [{"--limit", "xyz"}]}
   
       iex> OptionParser.parse(["--unknown", "xyz"], strict: [])
       {[], ["xyz"], [{"--unknown", nil}]}
   
       iex> OptionParser.parse(["--limit", "3", "--unknown", "xyz"],
       ...>                    switches: [limit: :integer])
       {[limit: 3, unknown: "xyz"], [], []}
   
   **Negation switches**
   
   All switches starting with ``--no-`` are considered to be booleans and
   never parse the next value:
   
   ::
   
       iex> OptionParser.parse(["--no-op", "path/to/file"])
       {[no_op: true], ["path/to/file"], []}
   
   However, in case the base switch exists, it sets that particular switch
   to false:
   
   ::
   
       iex> OptionParser.parse(["--no-op", "path/to/file"], switches: [op: :boolean])
       {[op: false], ["path/to/file"], []}
   
   **Aliases**
   
   A set of aliases can be given as options too:
   
   ::
   
       iex> OptionParser.parse(["-d"], aliases: [d: :debug])
       {[debug: true], [], []}
   
   
   

.. elixir:function:: OptionParser.parse_head/2
   :sig: parse_head(argv, opts \\ [])


   Specs:
   
 
   * parse_head(:elixir:type:`argv/0`, :elixir:type:`options/0`) :: {:elixir:type:`parsed/0`, :elixir:type:`argv/0`, :elixir:type:`errors/0`}
 

   
   Similar to ```parse/2`` <#parse/2>`__ but only parses the head of
   ``argv``; as soon as it finds a non-switch, it stops parsing.
   
   See ```parse/2`` <#parse/2>`__ for more information.
   
   **Example**
   
   ::
   
       iex> OptionParser.parse_head(["--source", "lib", "test/enum_test.exs", "--verbose"])
       {[source: "lib"], ["test/enum_test.exs", "--verbose"], []}
   
       iex> OptionParser.parse_head(["--verbose", "--source", "lib", "test/enum_test.exs", "--unlock"])
       {[verbose: true, source: "lib"], ["test/enum_test.exs", "--unlock"], []}
   
   
   







