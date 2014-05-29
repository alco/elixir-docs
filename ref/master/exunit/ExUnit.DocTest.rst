ExUnit.DocTest
==============================================================

.. elixir:module:: ExUnit.DocTest

   :mtype: 

Overview
--------

ExUnit.DocTest implements functionality similar to `Python's
doctest <http://docs.python.org/2/library/doctest.html>`__.

In a nutshell, it allows us to generate tests from the code examples
existing in a module/function/macro's documentation. In order to do
that, one needs to invoke the ``doctest/1`` macro from their test case
and write their examples according to some guidelines.

The syntax for examples is as follows. Every new test starts on a new
line, with an ``iex>`` prefix. Multiline expressions can be employed if
the following lines start with either ``...>`` (recommended) or ``iex>``
prefix.

The expected result should start at the next line after ``iex>`` or
``...>`` line(s) and is terminated either by a newline, new ``iex>``
prefix or end of the string literal.

Examples
~~~~~~~~

Currently, the only way to run doctests is to include them into an
ExUnit case with a ``doctest`` macro:

::

    defmodule MyModule.Test do
      use ExUnit.Case, async: true
      doctest MyModule
    end

The ``doctest`` macro is going to loop through all functions and macros
defined in ``MyModule``, parsing their documentation in search of code
examples.

A very basic example is:

::

    iex> 1+1
    2

Expressions on multiple lines are also supported:

::

    iex> Enum.map [1, 2, 3], fn(x) ->
    ...>   x * 2
    ...> end
    [2,4,6]

Multiple results can be checked within the same test:

::

    iex> a = 1
    1
    iex> a + 1
    2

If you want to keep any two tests separate, add an empty line between
them:

::

    iex> a = 1
    1

    iex> a + 1  # will fail with a "function a/0 undefined" error
    2

Similarly to iex you can use numbers in your "prompts":

::

    iex(1)> [1+2,
    ...(1)>  3]
    [3,3]

This is useful in two use cases:

-  Being able to refer to specific numbered scenarios
-  Copy-pasting examples from an actual iex session

We also allow you to select or skip some functions when calling
``doctest``. See the documentation for more info.

Opaque types
~~~~~~~~~~~~

Some types internal structure are kept hidden and instead show a
user-friendly structure when inspecting the value. The idiom in Elixir
is to print those data types as ``#Name<...>``. Doctest will test these
values by doing a string compare.

::

    iex> Enum.into([a: 10, b: 20], HashDict.new)
    #HashDict<[b: 20, a: 10]>

The above example will be tested with the following match:
``"#HashDict<[b: 20, a: 10]>" = inspect(Enum.into([a: 10, b: 20], HashDict.new))``.

Exceptions
~~~~~~~~~~

You can also showcase expressions raising an exception, for example:

::

    iex(1)> String.to_atom((fn() -> 1 end).())
    ** (ArgumentError) argument error

What DocTest will be looking for is a line starting with ``** (`` and it
will parse it accordingly to extract the exception name and message. At
this moment, the exception parser would make the parser treat the next
line as a start of a completely new expression (if it is prefixed with
``iex>``) or a no-op line with documentation. Thus, multiline messages
are not supported.

When not to use doctest
~~~~~~~~~~~~~~~~~~~~~~~

In general, doctests are not recommended when your code examples contain
side effects. For example, if a doctest prints to standard output,
doctest will not try to capture the output.

Similarly, doctests do not run in any kind of sandbox. So any module
defined in a code example is going to linger throughout the whole test
suite run.





Summary
-------

========================= =
:elixir:macro:`doctest/2` This macro is used to generate ExUnit test cases for doctests 
========================= =







Macros
------

.. elixir:macro:: ExUnit.DocTest.doctest/2
   :sig: doctest(mod, opts \\ [])


   
   This macro is used to generate ExUnit test cases for doctests.
   
   Calling ``doctest(Module)`` will generate tests for all doctests found
   in the module ``Module``
   
   Options can also be supplied:
   
   -  ``:except`` — generate tests for all functions except those listed
      (list of ``{function, arity}`` tuples)
   
   -  ``:only`` — generate tests only for functions listed (list of
      ``{function, arity}`` tuples)
   
   -  ``:import`` — when true, one can test a function defined in the
      module without referring to the module name. However, this is not
      feasible when there is a clash with a module like Kernel. In these
      cases, ``import`` should be set to ``false`` and a full ``M.f``
      construct should be used.
   
   **Examples**
   
   ::
   
       doctest MyModule, except: [trick_fun: 1]
   
   This macro is auto-imported with every
   ```ExUnit.Case`` <ExUnit.Case.html>`__.
   
   





