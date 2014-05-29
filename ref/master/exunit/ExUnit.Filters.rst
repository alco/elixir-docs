ExUnit.Filters
==============================================================

.. elixir:module:: ExUnit.Filters

   :mtype: 

Overview
--------

Conveniences for parsing and evaluating filters.





Summary
-------

=========================== =
:elixir:func:`eval/3`       Evaluates the include and exclude filters against the given tags 

:elixir:func:`normalize/2`  Normalizes include and excludes to remove duplicates and keep precedence 

:elixir:func:`parse/1`      Parses the given filters, as one would receive from the command line 

:elixir:func:`parse_path/1` Parses filters out of a path 
=========================== =



Types
-----

.. elixir:type:: ExUnit.Filters.t/0

   :elixir:type:`t/0` :: [{atom, any} | atom]
   





Functions
---------

.. elixir:function:: ExUnit.Filters.eval/3
   :sig: eval(include, exclude, tags)


   Specs:
   
 
   * eval(:elixir:type:`t/0`, :elixir:type:`t/0`, %{}) :: :ok | {:error, atom}
 

   
   Evaluates the include and exclude filters against the given tags.
   
   Expects filters to be normalized into a keyword list where each key is
   an atom and the value is a list.
   
   **Examples**
   
   ::
   
       iex> ExUnit.Filters.eval([foo: "bar"], [:foo], %{foo: "bar"})
       :ok
   
       iex> ExUnit.Filters.eval([foo: "bar"], [:foo], %{foo: "baz"})
       {:error, :foo}
   
   
   

.. elixir:function:: ExUnit.Filters.normalize/2
   :sig: normalize(include, exclude)


   Specs:
   
 
   * normalize(:elixir:type:`t/0` | nil, :elixir:type:`t/0` | nil) :: {:elixir:type:`t/0`, :elixir:type:`t/0`}
 

   
   Normalizes include and excludes to remove duplicates and keep
   precedence.
   
   **Examples**
   
   ::
   
       iex> ExUnit.Filters.normalize(nil, nil)
       {[], []}
   
       iex> ExUnit.Filters.normalize([:foo, :bar, :bar], [:foo, :baz])
       {[:foo, :bar], [:baz]}
   
   
   

.. elixir:function:: ExUnit.Filters.parse/1
   :sig: parse(filters)


   Specs:
   
 
   * parse([:elixir:type:`String.t/0`]) :: :elixir:type:`t/0`
 

   
   Parses the given filters, as one would receive from the command line.
   
   **Examples**
   
   ::
   
       iex> ExUnit.Filters.parse(["foo:bar", "baz", "line:9", "bool:true"])
       [{:foo, "bar"}, :baz, {:line, "9"}, {:bool, "true"}]
   
   
   

.. elixir:function:: ExUnit.Filters.parse_path/1
   :sig: parse_path(file)


   Specs:
   
 
   * parse_path(:elixir:type:`String.t/0`) :: {:elixir:type:`String.t/0`, any}
 

   
   Parses filters out of a path.
   
   Determines whether a given file path (supplied to ExUnit/Mix as
   arguments on the command line) includes a line number filter, and if so
   returns the appropriate ExUnit configuration options.
   
   







