Macro
==============================================================

.. elixir:module:: Macro

   :mtype: 

Overview
--------

Conveniences for working with macros.





Summary
-------

================================ =
:elixir:func:`decompose_call/1`  Decomposes a local or remote call into its remote part (when provided), function name and argument list 

:elixir:func:`escape/2`          Recursively escapes a value so it can be inserted into a syntax tree 

:elixir:func:`expand/2`          Receives an AST node and expands it until it can no longer be expanded 

:elixir:func:`expand_once/2`     Receives an AST node and expands it once 

:elixir:func:`pipe/3`            Pipes ``expr`` into the ``call_args`` at the given ``position`` 

:elixir:func:`postwalk/2`        Performs a depth-first, post-order traversal of quoted expressions 

:elixir:func:`postwalk/3`        Performs a depth-first, post-order traversal of quoted expressions using an accumulator 

:elixir:func:`prewalk/2`         Performs a depth-first, pre-order traversal of quoted expressions 

:elixir:func:`prewalk/3`         Performs a depth-first, pre-order traversal of quoted expressions using an accumulator 

:elixir:func:`to_string/2`       Converts the given expression to a binary 

:elixir:func:`unescape_string/1` Unescape the given chars 

:elixir:func:`unescape_string/2` Unescape the given chars according to the map given 

:elixir:func:`unescape_tokens/1` Unescape the given tokens according to the default map 

:elixir:func:`unescape_tokens/2` Unescape the given tokens according to the given map 

:elixir:func:`unpipe/1`          Breaks a pipeline expression into a list 

:elixir:func:`update_meta/2`     Applies the given function to the node metadata if it contains one 
================================ =



Types
-----

.. elixir:type:: Macro.t/0

   :elixir:type:`t/0` :: :elixir:type:`expr/0` | {:elixir:type:`t/0`, :elixir:type:`t/0`} | atom | number | binary | pid | (... -> any) | [:elixir:type:`t/0`]
   

   Abstract Syntax Tree (AST)
   

.. elixir:type:: Macro.expr/0

   :elixir:type:`expr/0` :: {:elixir:type:`expr/0` | atom, :elixir:type:`Keyword.t/0`, atom | [:elixir:type:`t/0`]}
   

   Expr node (remaining ones are literals)
   





Functions
---------

.. elixir:function:: Macro.decompose_call/1
   :sig: decompose_call(arg1)


   Specs:
   
 
   * decompose_call(:elixir:type:`Macro.t/0`) :: {atom, [:elixir:type:`Macro.t/0`]} | {:elixir:type:`Macro.t/0`, atom, [:elixir:type:`Macro.t/0`]} | :error
 

   
   Decomposes a local or remote call into its remote part (when provided),
   function name and argument list.
   
   Returns ``:error`` when an invalid call syntax is provided.
   
   **Examples**
   
   ::
   
       iex> Macro.decompose_call(quote do: foo)
       {:foo, []}
   
       iex> Macro.decompose_call(quote do: foo())
       {:foo, []}
   
       iex> Macro.decompose_call(quote do: foo(1, 2, 3))
       {:foo, [1, 2, 3]}
   
       iex> Macro.decompose_call(quote do: Elixir.M.foo(1, 2, 3))
       {{:__aliases__, [], [:Elixir, :M]}, :foo, [1, 2, 3]}
   
       iex> Macro.decompose_call(quote do: 42)
       :error
   
   
   

.. elixir:function:: Macro.escape/2
   :sig: escape(expr, opts \\ [])


   Specs:
   
 
   * escape(term, :elixir:type:`Keyword.t/0`) :: :elixir:type:`Macro.t/0`
 

   
   Recursively escapes a value so it can be inserted into a syntax tree.
   
   One may pass ``unquote: true`` to ```escape/2`` <#escape/2>`__ which
   leaves ``unquote`` statements unescaped, effectively unquoting the
   contents on escape.
   
   **Examples**
   
   ::
   
       iex> Macro.escape(:foo)
       :foo
   
       iex> Macro.escape({:a, :b, :c})
       {:{}, [], [:a, :b, :c]}
   
       iex> Macro.escape({:unquote, [], [1]}, unquote: true)
       1
   
   
   

.. elixir:function:: Macro.expand/2
   :sig: expand(tree, env)


   
   Receives an AST node and expands it until it can no longer be expanded.
   
   This function uses ```expand_once/2`` <#expand_once/2>`__ under the
   hood. Check ```expand_once/2`` <#expand_once/2>`__ for more information
   and exmaples.
   
   

.. elixir:function:: Macro.expand_once/2
   :sig: expand_once(ast, env)


   
   Receives an AST node and expands it once.
   
   The following contents are expanded:
   
   -  Macros (local or remote);
   -  Aliases are expanded (if possible) and return atoms;
   -  Pseudo-variables (``__ENV__``, ``__MODULE__`` and ``__DIR__``);
   -  Module attributes reader (``@foo``);
   
   If the expression cannot be expanded, it returns the expression itself.
   Notice that ```expand_once/2`` <#expand_once/2>`__ performs the
   expansion just once and it is not recursive. Check
   ```expand/2`` <#expand/2>`__ for expansion until the node can no longer
   be expanded.
   
   **Examples**
   
   In the example below, we have a macro that generates a module with a
   function named ``name_length`` that returns the length of the module
   name. The value of this function will be calculated at compilation time
   and not at runtime.
   
   Consider the implementation below:
   
   ::
   
       defmacro defmodule_with_length(name, do: block) do
         length = length(Atom.to_char_list(name))
   
         quote do
           defmodule unquote(name) do
             def name_length, do: unquote(length)
             unquote(block)
           end
         end
       end
   
   When invoked like this:
   
   ::
   
       defmodule_with_length My.Module do
         def other_function, do: ...
       end
   
   The compilation will fail because ``My.Module`` when quoted is not an
   atom, but a syntax tree as follow:
   
   ::
   
       {:__aliases__, [], [:My, :Module]}
   
   That said, we need to expand the aliases node above to an atom, so we
   can retrieve its length. Expanding the node is not straight-forward
   because we also need to expand the caller aliases. For example:
   
   ::
   
       alias MyHelpers, as: My
   
       defmodule_with_length My.Module do
         def other_function, do: ...
       end
   
   The final module name will be ``MyHelpers.Module`` and not
   ``My.Module``. With ```Macro.expand/2`` <Macro.html#expand/2>`__, such
   aliases are taken into consideration. Local and remote macros are also
   expanded. We could rewrite our macro above to use this function as:
   
   ::
   
       defmacro defmodule_with_length(name, do: block) do
         expanded = Macro.expand(name, __CALLER__)
         length   = length(Atom.to_char_list(expanded))
   
         quote do
           defmodule unquote(name) do
             def name_length, do: unquote(length)
             unquote(block)
           end
         end
       end
   
   
   

.. elixir:function:: Macro.pipe/3
   :sig: pipe(expr, call_args, position)


   Specs:
   
 
   * pipe(:elixir:type:`Macro.t/0`, :elixir:type:`Macro.t/0`, integer) :: :elixir:type:`Macro.t/0` | no_return
 

   
   Pipes ``expr`` into the ``call_args`` at the given ``position``.
   
   

.. elixir:function:: Macro.postwalk/2
   :sig: postwalk(ast, fun)


   Specs:
   
 
   * postwalk(:elixir:type:`t/0`, (:elixir:type:`t/0` -> :elixir:type:`t/0`)) :: :elixir:type:`t/0`
 

   
   Performs a depth-first, post-order traversal of quoted expressions.
   
   

.. elixir:function:: Macro.postwalk/3
   :sig: postwalk(ast, acc, fun)


   Specs:
   
 
   * postwalk(:elixir:type:`t/0`, any, (:elixir:type:`t/0`, any -> {:elixir:type:`t/0`, any})) :: {:elixir:type:`t/0`, any}
 

   
   Performs a depth-first, post-order traversal of quoted expressions using
   an accumulator.
   
   

.. elixir:function:: Macro.prewalk/2
   :sig: prewalk(ast, fun)


   Specs:
   
 
   * prewalk(:elixir:type:`t/0`, (:elixir:type:`t/0` -> :elixir:type:`t/0`)) :: :elixir:type:`t/0`
 

   
   Performs a depth-first, pre-order traversal of quoted expressions.
   
   

.. elixir:function:: Macro.prewalk/3
   :sig: prewalk(ast, acc, fun)


   Specs:
   
 
   * prewalk(:elixir:type:`t/0`, any, (:elixir:type:`t/0`, any -> {:elixir:type:`t/0`, any})) :: {:elixir:type:`t/0`, any}
 

   
   Performs a depth-first, pre-order traversal of quoted expressions using
   an accumulator.
   
   

.. elixir:function:: Macro.to_string/2
   :sig: to_string(tree, fun \\ fn _ast, string -> string end)


   Specs:
   
 
   * to_string(:elixir:type:`Macro.t/0`, (:elixir:type:`Macro.t/0`, :elixir:type:`String.t/0` -> :elixir:type:`String.t/0`)) :: :elixir:type:`String.t/0`
 

   
   Converts the given expression to a binary.
   
   **Examples**
   
   ::
   
       iex> Macro.to_string(quote do: foo.bar(1, 2, 3))
       "foo.bar(1, 2, 3)"
   
   
   

.. elixir:function:: Macro.unescape_string/1
   :sig: unescape_string(chars)


   Specs:
   
 
   * unescape_string(:elixir:type:`String.t/0`) :: :elixir:type:`String.t/0`
 

   
   Unescape the given chars.
   
   This is the unescaping behaviour used by default in Elixir single- and
   double-quoted strings. Check
   ```unescape_string/2`` <#unescape_string/2>`__ for information on how to
   customize the escaping map.
   
   In this setup, Elixir will escape the following: ``\a``, ``\b``, ``\d``,
   ``\e``, ``\f``, ``\n``, ``\r``, ``\s``, ``\t`` and ``\v``. Octals are
   also escaped according to the latin1 set they represent.
   
   This function is commonly used on sigil implementations (like ``~r``,
   ``~s`` and others) which receive a raw, unescaped string.
   
   **Examples**
   
   ::
   
       iex> Macro.unescape_string("example\\n")
       "example\n"
   
   In the example above, we pass a string with ``\n`` escaped and return a
   version with it unescaped.
   
   

.. elixir:function:: Macro.unescape_string/2
   :sig: unescape_string(chars, map)


   Specs:
   
 
   * unescape_string(:elixir:type:`String.t/0`, (non_neg_integer -> non_neg_integer | false)) :: :elixir:type:`String.t/0`
 

   
   Unescape the given chars according to the map given.
   
   Check ```unescape_string/1`` <#unescape_string/1>`__ if you want to use
   the same map as Elixir single- and double-quoted strings.
   
   **Map**
   
   The map must be a function. The function receives an integer
   representing the codepoint of the character it wants to unescape. Here
   is the default mapping function implemented by Elixir:
   
   ::
   
       def unescape_map(?a), do: ?\a
       def unescape_map(?b), do: ?\b
       def unescape_map(?d), do: ?\d
       def unescape_map(?e), do: ?\e
       def unescape_map(?f), do: ?\f
       def unescape_map(?n), do: ?\n
       def unescape_map(?r), do: ?\r
       def unescape_map(?s), do: ?\s
       def unescape_map(?t), do: ?\t
       def unescape_map(?v), do: ?\v
       def unescape_map(e),  do: e
   
   If the ``unescape_map`` function returns ``false``. The char is not
   escaped and ``\`` is kept in the char list.
   
   **Octals**
   
   Octals will by default be escaped unless the map function returns
   ``false`` for ``?0``.
   
   **Hex**
   
   Hexadecimals will by default be escaped unless the map function returns
   ``false`` for ``?x``.
   
   **Examples**
   
   Using the ``unescape_map`` function defined above is easy:
   
   ::
   
       Macro.unescape_string "example\\n", &unescape_map(&1)
   
   
   

.. elixir:function:: Macro.unescape_tokens/1
   :sig: unescape_tokens(tokens)


   Specs:
   
 
   * unescape_tokens([:elixir:type:`Macro.t/0`]) :: [:elixir:type:`Macro.t/0`]
 

   
   Unescape the given tokens according to the default map.
   
   Check ```unescape_string/1`` <#unescape_string/1>`__ and
   ```unescape_string/2`` <#unescape_string/2>`__ for more information
   about unescaping.
   
   Only tokens that are binaries are unescaped, all others are ignored.
   This function is useful when implementing your own sigils. Check the
   implementation of ```Kernel.sigil_s/2`` <Kernel.html#sigil_s/2>`__ for
   examples.
   
   

.. elixir:function:: Macro.unescape_tokens/2
   :sig: unescape_tokens(tokens, map)


   Specs:
   
 
   * unescape_tokens([:elixir:type:`Macro.t/0`], (non_neg_integer -> non_neg_integer | false)) :: [:elixir:type:`Macro.t/0`]
 

   
   Unescape the given tokens according to the given map.
   
   Check ```unescape_tokens/1`` <#unescape_tokens/1>`__ and
   ```unescape_string/2`` <#unescape_string/2>`__ for more information.
   
   

.. elixir:function:: Macro.unpipe/1
   :sig: unpipe(other)


   Specs:
   
 
   * unpipe(:elixir:type:`Macro.t/0`) :: [:elixir:type:`Macro.t/0`]
 

   
   Breaks a pipeline expression into a list.
   
   Raises if the pipeline is ill-formed.
   
   

.. elixir:function:: Macro.update_meta/2
   :sig: update_meta(quoted, fun)


   Specs:
   
 
   * update_meta(:elixir:type:`t/0`, (:elixir:type:`Keyword.t/0` -> :elixir:type:`Keyword.t/0`)) :: :elixir:type:`t/0`
 

   
   Applies the given function to the node metadata if it contains one.
   
   This is often useful when used with ``Macro.prewalk/1`` to remove
   information like lines and hygienic counters from the expression for
   either storage or comparison.
   
   **Examples**
   
   ::
   
       iex> quoted = quote line: 10, do: sample()
       {:sample, [line: 10], []}
       iex> Macro.update_meta(quoted, &Keyword.delete(&1, :line))
       {:sample, [], []}
   
   
   







