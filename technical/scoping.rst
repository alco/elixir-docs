Scoping Rules in Elixir (and Erlang)
====================================

.. contents:: :local:

For everyday use it is sufficient to understand the basics of scoping
rules in Elixir: that there's the top level scope and function clause
scope, and that named functions have their own peculiar differences from
the more conventional anonymous functions.

But there are, in fact, quite a few rules you need to know to get a
complete picture of the way scopes work in Elixir. In this technical
article we will take a close look at all of the scoping rules and learn
in what ways they differ from Erlang.

Types of Scope
--------------

In Elixir there are two types of scope:

-  the top level scope
-  function clause scope

There are a number of constructs that create new scope:

-  modules and module-like structures: ``defmodule``, ``defprotocol``,
   ``defimpl``
-  functions: ``fn``, ``def``, ``defp``
-  comprehensions: ``for``
-  ``try`` block bodies

Most of the time user code in Elixir is structured in the following way.
At the top level we define modules. Each module contains a number of
attributes and function clauses. Inside a function clause there can be
arbitrary number of expressions including control flow constructs like
``case``, ``if``, or ``try``:

.. code:: elixir

    abc = "abc"            T ---------------------+
                                                  |
    defmodule M do             M ---------------+ |
      @doc "factorial"                          | |
      @limit 13                                 | |
                                                | |
      def foo(n) do                F ---------+ | |
        x = case n do                         | | |  # T: top level scope
          0 -> 1                              | | |
          i when i > 0 -> n * foo(n - 1)      | | |  # M: module's scope
          _ -> :undef                         | | |
        end                                   | | |  # F: function clause scope
                                              | | |
        for x <- [1,2,3] do            C ---+ | | |  # C: comprehension's scope
          -x                                | | | |
        end                            -----+ | | |
                                              | | |
      end                          -----------+ | |
                                                | |
    end                        -----------------+ |
                            ----------------------+

Another way to visualise that structure, schematically:

::

    # Figure 1

    +------------------------------------------------------------+
    | Top level                                                  |
    |                                                            |
    |  +------------------------+     +------------------------+ |
    |  | Module                 |     | Module                 | |
    |  |                        |     |                        | |
    |  | +--------------------+ |     | +--------------------+ | |
    |  | | Function clause    | |     | | Function clause    | | |
    |  | |                    | |     | |                    | | |
    |  | | +----------------+ | |     | | +----------------+ | | |
    |  | | | Comprehension  | | |     | | | Comprehension  | | | |
    |  | | +----------------+ | |     | | +----------------+ | | |
    |  | | +----------------+ | | ... | | +----------------+ | | |
    |  | | | Anon. function | | |     | | | Anon. function | | | |
    |  | | +----------------+ | |     | | +----------------+ | | |
    |  | | +----------------+ | |     | | +----------------+ | | |
    |  | | | Try block      | | |     | | | Try block      | | | |
    |  | | +----------------+ | |     | | +----------------+ | | |
    |  | +--------------------+ |     | +--------------------+ | |
    |  +------------------------+     +------------------------+ |
    |                                                            |
    +------------------------------------------------------------+

When working in the interactive shell, the scope hierarchy is usually
flat ("function clause" in the graphic below now refers to anonymous
functions instead of named functions):

::

    # Figure 2

    +-----------------------+
    | Top level             |
    |                       |
    |  +-----------------+  |
    |  | Module          |  |
    |  +-----------------+  |
    |  +-----------------+  |
    |  | Function clause |  |
    |  +-----------------+  |
    |  +-----------------+  |
    |  | Comprehension   |  |
    |  +-----------------+  |
    |  +-----------------+  |
    |  | Anon. function  |  |
    |  +-----------------+  |
    |  +-----------------+  |
    |  | Try block       |  |
    |  +-----------------+  |
    |                       |
    +-----------------------+

Those are the two most commonly seen structures for code organisation in
Elixir.

In the general case, however, all scopes are arbitrarily nestable: we
could imagine a ``case`` expression inside a comprehension or a
top-level ``if`` expression defining different modules depending on some
condition. For example:

.. code:: elixir

    f = fn x ->
      case x do
        1 ->
          defmodule M do
            def say do
              "one"
            end
          end
        2 ->
         defmodule N do
            def say do
              "two"
            end
          end
      end
    end

    # no module has been defined yet
    M.say       #=> undefined function: M.say/0
    N.say       #=> undefined function: N.say/0

    # define M
    f.(1)
    M.say       #=> "one"
    N.say       #=> undefined function: N.say/0

    # define N
    f.(2)
    M.say       #=> "one"
    N.say       #=> "two"

In order to understand how the example above works, you should be aware
of the fact the a module definition creates the module as its
side-effect, so the module itself will be available globally. Only the
name of the module is affected by the nesting of the ``defmodule`` call
as we'll see later in this article.

Elixir Scopes Are Lexical
-------------------------

This means that it is possible to determine the scope of every
identifier only by looking at the source code.

All variable bindings introduced in a scope are available until the end
of that scope. Elixir has a few special forms that treat scopes a little
differently (namely ``require``, ``import``, and ``alias``). We will
examine them at the end of this article.

Scope Nesting and Shadowing
---------------------------

According to the rules of lexical scope, any variables defined in the
surrounding scope are accessible in all other scopes it contains.

In **Figure 1** above, any variable defined in the top level scope will
be accessible in the module's scope and any scope nested inside it, and
so on.

There is an exception to this rule which applies only to named
functions: any variable coming from the surrounding scope has to be
unquoted inside a function clause body.

Any variable in a nested scope whose name coincides with a variable from
the surrounding scope will shadow that outer variable. In other words,
the variable inside the nested scope temporarily hides the variable from
the surrounding scope, but does not affect it in any way.

The Top Level Scope
-------------------

The top level scope includes every variable and identifier defined
outside of any other scope.

.. code:: elixir

    x        #=> undefined function: x/0

    x = 1
    x        #=> 1

    f = fn -> x end
    f.()     #=> 1

Named functions cannot be defined at the top level because a named
function always belongs within a module. However, named functions can be
imported into any lexical scope (including the top level scope) like
this:

.. code:: elixir

    import String, only: [reverse: 1]

    reverse "Hello"  #=> "olleH"

In fact, all functions and macros from the ``Kernel`` module are
autoimported in the top level scope by the compiler.

Function Clause Scope
---------------------

Each function clause defines a new lexical scope: any new variable bound
inside it will not be available outside of that clause:

.. code:: elixir

    defmodule M do
      def foo(x), do: -x

      # this 'x' is completely independent from the one in 'foo/1'
      def bar(x), do: 2*x

      x = 1

      # shadowing in action: the 'x' in the argument list creates a variable
      # local to the function clause's body and has nothing to do with the
      # previously defined 'x'
      f = fn(x) ->
        x = x + 1
      end

      y = f.(x)
      IO.puts "The correct answer is #{y} == #{f.(x)}"
      # output: The correct answer is 2 == 2

      # in this case the argument 'y' shadows the named function 'y/0'
      def y(y), do: y*2

      # here the reference to 'y' inside the function
      # body is actually a recursive call to 'y/0'
      def y, do: y*2
    end

    M.foo 3      #=> -3
    M.bar 4      #=> 8

    M.y -2       #=> -4
    M.y          #=> infinite loop

Apart from named functions, a new function clause scope is created for
each module-like block, anonymous function, ``try`` block body, or
comprehension body (see below).

.. code:: elixir

    f = fn(x) ->
      a = x - 1
    end

    a            #=> undefined function: a/0

    g = fn(f) ->
      g = f
    end

    f            #=> (still the anonymous function defined above)
    g            #=> (the anonymous function we've just defined)

Named Functions And Modules
---------------------------

As mentioned before, named function have a couple of peculiarities.

First, defining a named function does not introduce a new binding into
the current scope:

.. code:: elixir

    defmodule M do
      def foo, do: "hi"

      foo()  # will cause CompileError: undefined function foo/0
    end

Second, named functions cannot directly access surrounding scope, one
has to use ``unquote`` to achieve that:

.. code:: elixir

    defmodule M do
      a = 1

      # 'a' inside unquote() unambiguously refers to 'a' defined
      # in the module's scope
      def a, do: unquote(a)

      # 'a' inside the body unambiguously refers to the function 'a/0'
      def a(b), do: a + b
    end

    M.a          #=> 1
    M.a 3        #=> 4

Module scope works just like function clause scope: any variables
defined between ``defmodule`` (or ``defprotocol``, etc.) and its
corresponding ``end`` will not be accessible outside of the module, but
they will be available in the nested scopes of that module as per usual
(modulo the unquoting caveat of named functions mentioned above).

It is important to understand that a module's scope exists as long as it
is being compiled. In other words, variables are not "compiled into" the
module. The ``Module.function`` syntax is only applicable to named
functions and that's another thing that makes such functions special:

.. code:: elixir

    defmodule M do
      x = "hello"

      def hi, do: unquote(x)
    end

    M.hi         #=> "hello"
    M.x          #=> undefined function: x/0

You may be wondering how local function calls work when named functions
don't produce name bindings and don't have direct access to the
surrounding scope. The answer to this lies in the following rule
followed by Elixir when trying to resolve an identifier to its value:

    Any unbound identifier is treated as a local function call.

Let's see how this works in code:

.. code:: elixir

    defmodule P do
      def f, do: "I am P's f"
      def g, do: f
    end

    defmodule Q do
      def f, do: "I am Q's f"
      def g, do: f
    end

    # both P's 'g' and Q's 'g' refer to their local buddy named 'f'
    P.g          #=> "I am P's f"
    Q.g          #=> "I am Q's f"

    # let's make 'f' local in the top level scope
    f            #=> undefined function: f/0
    import P
    f            #=> "I am P's f"

One more note about module naming and nested modules: modules are always
defined at the top level, no matter in what scope the actual call to
``defmodule`` is located. This means that as long the VM can find the
.beam file with the module's code at run time, it does not matter in
which scope you reference that module's name.

What the scoping does affect is the name the module will get:

.. code:: elixir

    defmodule P do
      # The actual module name will be P.Q, but it is implicitly aliased to Q
      # in P's scope
      defmodule Q do
        def q(false), do: "sorry"
        def q(true) do
          # The actual module name will be P.Q.M
          defmodule M do
            def say, do: "hi"
          end
        end
      end

      # Q is resolved to P.Q
      def foo do
        Q.q false
      end

      # At run time, this has the same exact implementation as foo
      def bar do
        P.Q.q false
      end
    end

    P.foo         #=> "sorry"
    P.bar         #=> "sorry"
    P.Q.q false   #=> "sorry"

    # the module hasn't been defined yet
    P.Q.M.say     #=> undefined function: P.Q.M.say/0

    # after this call the P.Q.M module will become available
    P.Q.q true
    P.Q.M.say     #=> "hi"

Case-like Clauses
-----------------

Control flow constructs ``case``, ``receive``, and ``cond`` share a
common trait:

-  any variable introduced in a clause pattern/condition will be
   accessible only within that clause's body

-  any variable introduced inside some (but not all) clause bodies will
   become available in the surrounding scope (possibly with the default
   ``nil`` value)

Here are some examples of those rules in action:

.. code:: elixir

    case x do
      # both 'result' and 'a' are visible only within this clause's body
      {:ok, result}=a -> IO.inspect(result); a

      # 'error' is actually bound in the surrounding scope; its value will be nil
      # if 'x' does not match :error
      :error -> error = true

      # ordinary shadowing: this 'x' is visible only within the clause's body and
      # it doesn't affect the 'x' from the surrounding scope
      [x] -> IO.inspect(x)
    end

    result  #=> undefined function: result/0
    a       #=> undefined function: a/0

    error   #=> true if x == :error, otherwise nil

Note: due to a bug in the 0.12.x series, ``cond``'s conditions actually
leak bindings to the surrounding scope. This should be fixed in 0.13.1.

.. code:: elixir

    cond do
      a0 = false -> a = a0
      b = 1      -> b
      c = 2      -> c = 2
      true       -> d = 3
    end

    a      #=> false (bound to false inside the 1st condition's body)
    b      #=> undefined function: b/0
    c      #=> nil (the 2nd condition is truthy, so `c = 2` was not evaluated)
    d      #=> nil (the body with `d = 3` was not evaluated,
           #        so 'd' also leaks with the default value)

.. code:: elixir

    if x = 3 do
      case y = :ok do
        :ok -> :ok
        :error -> a = "it's an error"
      end
    else
      z = 11
    end

    x      #=> 3
    y      #=> :ok
    a      #=> nil
    z      #=> nil

Try Blocks
----------

The ``try`` block works similar to ``case`` and ``receive``, but it
creates new scope, so it never leaks variable bindings to the
surrounding scope.

.. code:: elixir

    try do
      # all of the variables defined here are local to this block
      # (like in a function clause scope)
      a = 1
      b = a + 1
      c = d
    rescue
      # these work like bindings in `case` patterns
      x in [RuntimeError] -> y = x
      x -> z = x
    end

    # none of the variables have leaked
    a       #=> undefined function: a/0
    b       #=> undefined function: b/0
    c       #=> undefined function: c/0
    d       #=> undefined function: d/0
    x       #=> undefined function: x/0
    y       #=> undefined function: y/0
    z       #=> undefined function: z/0

Comprehensions
--------------

Comprehensions consist of two parts: the generator and the body.

Variables introduced in the generator part will only be visible within
the body.

.. code:: elixir

    for a = x <- [1, 2, 3, 4], do: b = {a, x}
    #=> [{1, 1}, {2, 2}, {3, 3}, {4, 4}]

    a       #=> undefined function: a/0
    x       #=> undefined function: x/0

The comprehension body itself works like function clause scope:

.. code:: elixir

    for x <- ["abc", "def"] do
      # import takes effect only within the comprehension's body
      import String, only: [reverse: 1]
      b = reverse x
    end
    #=> ["cba", "fed"]

    b
    #=> undefined function: b/0

    reverse "hello"
    #=> undefined function: reverse/1

``require``, ``import``, and ``alias``
--------------------------------------

All of the rules described so far apply to variable bindings. When it
comes to one of these three special forms, their effect persists until
the end of the ``do`` block they are called in. Effectively, those forms
see a slightly different scope division in which control flow constructs
create a new lexical scope:

.. code:: elixir

    # top level scope

    defmodule M do
      # new scope
      import String, only: [reverse: 1]

      def foo do
        # new scope
        import String, only: [strip: 1]

        IO.puts reverse("abc")   # ok: inherited from the surrounding scope

        if true do
          # new scope
          import String, only: [downcase: 1]
        else
          # new scope
          import String, only: [upcase: 1]
        end

        " hello "
        |> strip      # ok: made local in the current scope with 'import'
        |> downcase   # error: no local function downcase/1
        |> upcase     # ditto
      end

      def bar do
        # new scope

        IO.puts reverse("abc")   # ok: inherited from the surrounding scope
        strip(" hello ")         # error: no local function strip/1
      end
    end

Differences from Erlang
-----------------------

Most of the scoping rules described here have been inherited from
Erlang.

One notable difference is that modules simply contain forms and function
clauses, they don't have scope nor allow arbitrary expressions like
modules in Elixir do.

There are two differences in the way case clause scope works in Erlang:

1) both bindings introduced in the pattern and in the body of a clause
   modify the surrounding scope

2) those variables that are bound in some (but not all) of the clauses
   will remain unbound in the surrounding scope (instead of getting the
   ``nil`` value like they do in Elixir); they are also called *unsafe*
   variables

.. code:: erlang

    case 1 of
      1=A -> B = A;
      _   -> C = 1
    end.

    A.  %=> 1
    B.  %=> 1
    C.  %=> variable 'C' is unbound

There is an ``if`` construct in Erlang that looks similar to ``cond``,
but works differently. It only allows guard expressions as conditions
and those do not let you introduce variable bindings. Variables bound in
clause bodies leak to the surrounding scope the same way they do in
``case``.

.. code:: erlang

    X = 1,
    if
      X -> A = X;
      true -> B = X
    end.

    A.  %=> variable 'A' is unbound
    B.  %=> 1

    %%%

    Y = true,
    if
      Y -> P = Y;
      true -> Q = Y
    end.

    P.  %=> true
    Q.  %=> variable 'Q' is unbound

Refer to `this
page <http://erlang.org/doc/reference_manual/expressions.html#id77105>`__
for more information about Erlang control flow constructs.

An assorted list of resources that describe various aspects of Erlang's
scoping rules:

-  `Matching, Guards and Scope of
   Variables <http://www.erlang.org/doc/getting_started/seq_prog.html#id63042>`__
   from Erlang's Getting Started guide.
-  `Scope of
   variables <http://www.erlang.org/course/advanced.html#scope>`__ in
   the Erlang course.
-  `Static rules of variable scoping in
   Erlang <http://icai.ektf.hu/pdf/ICAI2007-vol2-pp137-145.pdf>`__ paper
-  `case expression
   scope <https://groups.google.com/d/msg/erlang-programming/MTmJpL-pXic/has8ZfpUL5UJ>`__
   question on Erlang's mailing list

