Module
==============================================================

.. elixir:module:: Module

   :mtype: 

Overview
--------

This module provides many functions to deal with modules during
compilation time. It allows a developer to dynamically attach
documentation, add, delete and register attributes and so forth.

After a module is compiled, using many of the functions in this module
will raise errors, since it is out of their scope to inspect runtime
data. Most of the runtime data can be inspected via the
``__info__(attr)`` function attached to each compiled module.

Module attributes
~~~~~~~~~~~~~~~~~

Each module can be decorated with one or more attributes. The following
ones are currently defined by Elixir:

-  ``@after_compile``

   A hook that will be invoked right after the current module is
   compiled.

   Accepts a module or a tuple ``{<module>, <function atom>}``. The
   function must take two arguments: the module environment and its
   bytecode. When just a module is provided, the function is assumed to
   be ``__after_compile__/2``.

   **Example**

   ::

       defmodule M do
         @after_compile __MODULE__

         def __after_compile__(env, _bytecode) do
           IO.inspect env
         end
       end

-  ``@before_compile``

   A hook that will be invoked before the module is compiled.

   Accepts a module or a tuple ``{<module>, <function/macro atom>}``.
   The function/macro must take one argument: the module environment. If
   it's a macro, its returned value will be injected at the end of the
   module definition before the compilation starts.

   When just a module is provided, the function/macro is assumed to be
   ``__before_compile__/1``.

   Note: unlike ``@after_compile``, the callback function/macro must be
   placed in a separate module (because when the callback is invoked,
   the current module does not yet exist).

   **Example**

   ::

       defmodule A do
         defmacro __before_compile__(_env) do
           quote do
             def hello, do: "world"
           end
         end
       end

       defmodule B do
         @before_compile A
       end

-  ``@behaviour`` (notice the British spelling)

   Specify an OTP or user-defined behaviour.

   **Example**

   ::

       defmodule M do
         @behaviour gen_event

         # ...
       end

-  ``@compile``

   Define options for module compilation that are passed to the Erlang
   compiler.

   Accepts an atom, a tuple, or a list of atoms and tuples.

   See http://www.erlang.org/doc/man/compile.html for the list of
   supported options.

   **Example**

   ::

         defmodule M do
           @compile {:inline, myfun: 1}

           def myfun(arg) do
             to_string(arg)
           end
         end

-  ``@doc``

   Provide documentation for the function or macro that follows the
   attribute.

   Accepts a string (often a heredoc) or ``false`` where ``@doc false``
   will make the function/macro invisible to the documentation
   extraction tools like ExDoc.

   Can be invoked more than once.

   **Example**

   ::

         defmodule M do
           @doc "Hello world"
           def hello do
             "world"
           end

           @doc """
           Sum.
           """
           def sum(a, b) do
             a + b
           end
         end

-  ``@file``

   Change the filename used in stacktraces for the function or macro
   that follows the attribute.

   Accepts a string. Can be used more than once.

   **Example**

   ::

         defmodule M do
           @doc "Hello world"
           @file "hello.ex"
           def hello do
             "world"
           end
         end

-  ``@moduledoc``

   Provide documentation for the current module.

   Accepts a string (which is often a heredoc) or ``false`` where
   ``@moduledoc false`` will make the module invisible to the
   documentation extraction tools like ExDoc.

   **Example**

   ::

         defmodule M do
           @moduledoc """
           A very useful module
           """
         end

-  ``@on_definition``

   A hook that will be invoked when each function or macro in the
   current module is defined. Useful when annotating functions.

   Accepts a module or a tuple ``{<module>, <function atom>}``. The
   function must take 6 arguments:

   -  the module environment
   -  kind: ``:def``, ``:defp``, ``:defmacro``, or ``:defmacrop``
   -  function/macro name
   -  list of expanded arguments
   -  list of expanded guards
   -  expanded function body

   Note the hook receives the expanded arguments and it is invoked
   before the function is stored in the module. So
   ```Module.defines?/2`` <Module.html#defines?/2>`__ will return false
   for the first clause of every function.

   If the function/macro being defined has multiple clauses, the hook
   will be called for each clause.

   Unlike other hooks, ``@on_definition`` will only invoke functions and
   never macros. This is because the hook is invoked inside the context
   of the function (and nested function definitions are not allowed in
   Elixir).

   When just a module is provided, the function is assumed to be
   ``__on_definition__/6``.

   **Example**

   ::

         defmodule H do
           def on_def(_env, kind, name, args, guards, body) do
             IO.puts "Defining #{kind} named #{name} with args:"
             IO.inspect args
             IO.puts "and guards"
             IO.inspect guards
             IO.puts "and body"
             IO.puts Macro.to_string(body)
           end
         end

         defmodule M do
           @on_definition {H, :on_def}

           def hello(arg) when is_binary(arg) or is_list(arg) do
             "Hello" <> to_string(arg)
           end

           def hello(_) do
             :ok
           end
         end

-  ``@on_load``

   A hook that will be invoked whenever the module is loaded.

   Accepts a function atom of a function in the current module. The
   function must have arity 0 (no arguments) and has to return ``:ok``,
   otherwise the loading of the module will be aborted.

   **Example**

   ::

         defmodule M do
           @on_load :load_check

           def load_check do
             if some_condition() do
               :ok
             else
               nil
             end
           end

           def some_condition do
             false
           end
         end

-  ``@vsn``

   Specify the module version. Accepts any valid Elixir value.

   **Example**

   ::

         defmodule M do
           @vsn "1.0"
         end

The following attributes are part of typespecs and are also reserved by
Elixir (see ```Kernel.Typespec`` <Kernel.Typespec.html>`__ for more
information about typespecs):

-  ``@type`` - defines a type to be used in ``@spec``
-  ``@typep`` - defines a private type to be used in ``@spec``
-  ``@opaque`` - defines an opaque type to be used in ``@spec``
-  ``@spec`` - provides a specification for a function
-  ``@callback`` - provides a specification for the behaviour callback

In addition to the built-in attributes outlined above, custom attributes
may also be added. A custom attribute is any valid identifier prefixed
with an ``@`` and followed by a valid Elixir value:

::

      defmodule M do
        @custom_attr [some: "stuff"]
      end

For more advanced options available when defining custom attributes, see
```register_attribute/3`` <#register_attribute/3>`__.

Runtime information about a module
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

It is possible to query a module at runtime to find out which functions
and macros it defines, extract its docstrings, etc. See
```__info__/1`` <#__info__/1>`__.





Summary
-------

=================================== =
:elixir:func:`__info__/1`           Provides runtime information about functions and macros defined by the module, enables docstring extraction, etc 

:elixir:func:`add_doc/6`            Attaches documentation to a given function or type. It expects the module the function/type belongs to, the line (a non negative integer), the kind (``def`` or ``defmacro``), a tuple representing the function and its arity, the function signature (the signature should be omitted for types) and the documentation, which should be either a binary or a boolean 

:elixir:func:`concat/1`             Concatenates a list of aliases and returns a new alias 

:elixir:func:`concat/2`             Concatenates two aliases and returns a new alias 

:elixir:func:`create/3`             Creates a module with the given name and defined by the given quoted expressions. The line where the module is defined and its file can be passed as options 

:elixir:func:`defines?/2`           Checks if the module defines the given function or macro. Use ```defines?/3`` <#defines?/3>`__ to assert for a specific type 

:elixir:func:`defines?/3`           Checks if the module defines a function or macro of the given ``kind``. ``kind`` can be any of ``:def``, ``:defp``, ``:defmacro`` or ``:defmacrop`` 

:elixir:func:`definitions_in/1`     Return all functions defined in ``module`` 

:elixir:func:`definitions_in/2`     Returns all functions defined in ``module``, according to its kind 

:elixir:func:`delete_attribute/2`   Deletes all attributes that match the given key 

:elixir:func:`eval_quoted/4`        Evaluates the quoted contents in the given module's context 

:elixir:func:`function/3`           Gets an anonymous function from the given module, function and arity. The module and function are not verified to exist 

:elixir:func:`get_attribute/3`      Gets the given attribute from a module. If the attribute was marked with ``accumulate`` with ```Module.register_attribute/3`` <Module.html#register_attribute/3>`__, a list is always returned 

:elixir:func:`make_overridable/2`   Makes the given functions in ``module`` overridable. An overridable function is lazily defined, allowing a developer to customize it. See ```Kernel.defoverridable/1`` <Kernel.html#defoverridable/1>`__ for more information and documentation 

:elixir:func:`open?/1`              Check if a module is open, i.e. it is currently being defined and its attributes and functions can be modified 

:elixir:func:`overridable?/2`       Returns ``true`` if ``tuple`` in ``module`` is marked as overridable 

:elixir:func:`put_attribute/3`      Puts an Erlang attribute to the given module with the given key and value. The semantics of putting the attribute depends if the attribute was registered or not via ```register_attribute/3`` <#register_attribute/3>`__ 

:elixir:func:`register_attribute/3` Registers an attribute. By registering an attribute, a developer is able to customize how Elixir will store and accumulate the attribute values 

:elixir:func:`safe_concat/1`        Concatenates a list of aliases and returns a new alias only if the alias was already referenced. If the alias was not referenced yet, fails with ```ArgumentError`` <ArgumentError.html>`__. It handles char lists, binaries and atoms 

:elixir:func:`safe_concat/2`        Concatenates two aliases and returns a new alias only if the alias was already referenced. If the alias was not referenced yet, fails with ```ArgumentError`` <ArgumentError.html>`__. It handles char lists, binaries and atoms 

:elixir:func:`split/1`              Split the given module name into binary parts 
=================================== =





Functions
---------

.. elixir:function:: Module.__info__/1
   :sig: __info__(kind)


   Specs:
   
 
   * __info__(atom) :: term
 

   
   Provides runtime information about functions and macros defined by the
   module, enables docstring extraction, etc.
   
   Each module gets an ```__info__/1`` <#__info__/1>`__ function when it's
   compiled. The function takes one of the following atoms:
   
   -  ``:functions`` - keyword list of public functions along with their
      arities
   
   -  ``:macros`` - keyword list of public macros along with their arities
   
   -  ``:module`` - module name (``Module == Module.__info__(:module)``)
   
   In addition to the above, you may also pass to
   ```__info__/1`` <#__info__/1>`__ any atom supported by Erlang's
   ``module_info`` function which also gets defined for each compiled
   module. See http://erlang.org/doc/reference\_manual/modules.html#id69430
   for more information.
   
   

.. elixir:function:: Module.add_doc/6
   :sig: add_doc(module, line, kind, tuple, signature \\ [], doc)


   
   Attaches documentation to a given function or type. It expects the
   module the function/type belongs to, the line (a non negative integer),
   the kind (``def`` or ``defmacro``), a tuple representing the function
   and its arity, the function signature (the signature should be omitted
   for types) and the documentation, which should be either a binary or a
   boolean.
   
   **Examples**
   
   ::
   
       defmodule MyModule do
         Module.add_doc(__MODULE__, __ENV__.line + 1, :def, {:version, 0}, [], "Manually added docs")
         def version, do: 1
       end
   
   
   

.. elixir:function:: Module.concat/1
   :sig: concat(list)


   Specs:
   
 
   * concat([binary | atom]) :: atom
 

   
   Concatenates a list of aliases and returns a new alias.
   
   **Examples**
   
   ::
   
       iex> Module.concat([Foo, Bar])
       Foo.Bar
   
       iex> Module.concat([Foo, "Bar"])
       Foo.Bar
   
   
   

.. elixir:function:: Module.concat/2
   :sig: concat(left, right)


   Specs:
   
 
   * concat(binary | atom, binary | atom) :: atom
 

   
   Concatenates two aliases and returns a new alias.
   
   **Examples**
   
   ::
   
       iex> Module.concat(Foo, Bar)
       Foo.Bar
   
       iex> Module.concat(Foo, "Bar")
       Foo.Bar
   
   
   

.. elixir:function:: Module.create/3
   :sig: create(module, quoted, opts \\ [])


   
   Creates a module with the given name and defined by the given quoted
   expressions. The line where the module is defined and its file can be
   passed as options.
   
   **Examples**
   
   ::
   
       contents =
         quote do
           def world, do: true
         end
   
       Module.create(Hello, contents, Macro.Env.location(__ENV__))
   
       Hello.world #=> true
   
   **Differences from ``defmodule``**
   
   ``Module.create`` works similarly to ``defmodule`` and return the same
   results. While one could also use ``defmodule`` to define modules
   dynamically, this function is preferred when the module body is given by
   a quoted expression.
   
   Another important distinction is that ``Module.create`` allows you to
   control the environment variables used when defining the module, while
   ``defmodule`` automatically shares the same environment.
   
   

.. elixir:function:: Module.defines?/2
   :sig: defines?(module, tuple)


   
   Checks if the module defines the given function or macro. Use
   ```defines?/3`` <#defines?/3>`__ to assert for a specific type.
   
   **Examples**
   
   ::
   
       defmodule Example do
         Module.defines? __MODULE__, {:version, 0} #=> false
         def version, do: 1
         Module.defines? __MODULE__, {:version, 0} #=> true
       end
   
   
   

.. elixir:function:: Module.defines?/3
   :sig: defines?(module, tuple, kind)


   
   Checks if the module defines a function or macro of the given ``kind``.
   ``kind`` can be any of ``:def``, ``:defp``, ``:defmacro`` or
   ``:defmacrop``.
   
   **Examples**
   
   ::
   
       defmodule Example do
         Module.defines? __MODULE__, {:version, 0}, :defp #=> false
         def version, do: 1
         Module.defines? __MODULE__, {:version, 0}, :defp #=> false
       end
   
   
   

.. elixir:function:: Module.definitions_in/1
   :sig: definitions_in(module)


   
   Return all functions defined in ``module``.
   
   **Examples**
   
   ::
   
       defmodule Example do
         def version, do: 1
         Module.definitions_in __MODULE__ #=> [{:version,0}]
       end
   
   
   

.. elixir:function:: Module.definitions_in/2
   :sig: definitions_in(module, kind)


   
   Returns all functions defined in ``module``, according to its kind.
   
   **Examples**
   
   ::
   
       defmodule Example do
         def version, do: 1
         Module.definitions_in __MODULE__, :def  #=> [{:version,0}]
         Module.definitions_in __MODULE__, :defp #=> []
       end
   
   
   

.. elixir:function:: Module.delete_attribute/2
   :sig: delete_attribute(module, key)


   
   Deletes all attributes that match the given key.
   
   **Examples**
   
   ::
   
       defmodule MyModule do
         Module.put_attribute __MODULE__, :custom_threshold_for_lib, 10
         Module.delete_attribute __MODULE__, :custom_threshold_for_lib
       end
   
   
   

.. elixir:function:: Module.eval_quoted/4
   :sig: eval_quoted(module, quoted, binding \\ [], opts \\ [])


   
   Evaluates the quoted contents in the given module's context.
   
   A list of environment options can also be given as argument. See
   ```Code.eval_string/3`` <Code.html#eval_string/3>`__ for more
   information.
   
   Raises an error if the module was already compiled.
   
   **Examples**
   
   ::
   
       defmodule Foo do
         contents = quote do: (def sum(a, b), do: a + b)
         Module.eval_quoted __MODULE__, contents
       end
   
       Foo.sum(1, 2) #=> 3
   
   For convenience, you can my pass ``__ENV__`` as argument and all options
   will be automatically extracted from the environment:
   
   ::
   
       defmodule Foo do
         contents = quote do: (def sum(a, b), do: a + b)
         Module.eval_quoted __MODULE__, contents, [], __ENV__
       end
   
       Foo.sum(1, 2) #=> 3
   
   
   

.. elixir:function:: Module.function/3
   :sig: function(mod, fun, arity)


   
   Gets an anonymous function from the given module, function and arity.
   The module and function are not verified to exist.
   
   ::
   
       iex> fun = Module.function(Kernel, :is_atom, 1)
       iex> fun.(:hello)
       true
   
   
   

.. elixir:function:: Module.get_attribute/3
   :sig: get_attribute(module, key, warn \\ nil)


   Specs:
   
 
   * get_attribute(module, atom, warn :: nil | [tuple]) :: term
 

   
   Gets the given attribute from a module. If the attribute was marked with
   ``accumulate`` with
   ```Module.register_attribute/3`` <Module.html#register_attribute/3>`__,
   a list is always returned.
   
   The ``@`` macro compiles to a call to this function. For example, the
   following code:
   
   ::
   
       @foo
   
   Expands to:
   
   ::
   
       Module.get_attribute(__MODULE__, :foo, true)
   
   Notice the third argument may be given to indicate a stacktrace to be
   emitted when the attribute was not previously defined. The default value
   for ``warn`` is nil for direct calls but the ``@foo`` macro sets it to
   the proper stacktrace automatically, warning every time ``@foo`` is used
   but not set previously.
   
   **Examples**
   
   ::
   
       defmodule Foo do
         Module.put_attribute __MODULE__, :value, 1
         Module.get_attribute __MODULE__, :value #=> 1
   
         Module.register_attribute __MODULE__, :value, accumulate: true
         Module.put_attribute __MODULE__, :value, 1
         Module.get_attribute __MODULE__, :value #=> [1]
       end
   
   
   

.. elixir:function:: Module.make_overridable/2
   :sig: make_overridable(module, tuples)


   
   Makes the given functions in ``module`` overridable. An overridable
   function is lazily defined, allowing a developer to customize it. See
   ```Kernel.defoverridable/1`` <Kernel.html#defoverridable/1>`__ for more
   information and documentation.
   
   

.. elixir:function:: Module.open?/1
   :sig: open?(module)


   
   Check if a module is open, i.e. it is currently being defined and its
   attributes and functions can be modified.
   
   

.. elixir:function:: Module.overridable?/2
   :sig: overridable?(module, tuple)


   
   Returns ``true`` if ``tuple`` in ``module`` is marked as overridable.
   
   

.. elixir:function:: Module.put_attribute/3
   :sig: put_attribute(module, key, value)


   
   Puts an Erlang attribute to the given module with the given key and
   value. The semantics of putting the attribute depends if the attribute
   was registered or not via
   ```register_attribute/3`` <#register_attribute/3>`__.
   
   **Examples**
   
   ::
   
       defmodule MyModule do
         Module.put_attribute __MODULE__, :custom_threshold_for_lib, 10
       end
   
   
   

.. elixir:function:: Module.register_attribute/3
   :sig: register_attribute(module, new, opts)


   
   Registers an attribute. By registering an attribute, a developer is able
   to customize how Elixir will store and accumulate the attribute values.
   
   **Options**
   
   When registering an attribute, two options can be given:
   
   -  ``:accumulate`` - Several calls to the same attribute will accumulate
      instead of override the previous one. New attributes are always added
      to the top of the accumulated list.
   
   -  ``:persist`` - The attribute will be persisted in the Erlang Abstract
      Format. Useful when interfacing with Erlang libraries.
   
   By default, both options are ``false``.
   
   **Examples**
   
   ::
   
       defmodule MyModule do
         Module.register_attribute __MODULE__,
           :custom_threshold_for_lib,
           accumulate: true, persist: false
   
         @custom_threshold_for_lib 10
         @custom_threshold_for_lib 20
         @custom_threshold_for_lib #=> [20, 10]
       end
   
   
   

.. elixir:function:: Module.safe_concat/1
   :sig: safe_concat(list)


   Specs:
   
 
   * safe_concat([binary | atom]) :: atom | no_return
 

   
   Concatenates a list of aliases and returns a new alias only if the alias
   was already referenced. If the alias was not referenced yet, fails with
   ```ArgumentError`` <ArgumentError.html>`__. It handles char lists,
   binaries and atoms.
   
   **Examples**
   
   ::
   
       iex> Module.safe_concat([Unknown, Module])
       ** (ArgumentError) argument error
   
       iex> Module.safe_concat([List, Chars])
       List.Chars
   
   
   

.. elixir:function:: Module.safe_concat/2
   :sig: safe_concat(left, right)


   Specs:
   
 
   * safe_concat(binary | atom, binary | atom) :: atom | no_return
 

   
   Concatenates two aliases and returns a new alias only if the alias was
   already referenced. If the alias was not referenced yet, fails with
   ```ArgumentError`` <ArgumentError.html>`__. It handles char lists,
   binaries and atoms.
   
   **Examples**
   
   ::
   
       iex> Module.safe_concat(Unknown, Module)
       ** (ArgumentError) argument error
   
       iex> Module.safe_concat(List, Chars)
       List.Chars
   
   
   

.. elixir:function:: Module.split/1
   :sig: split(module)


   
   Split the given module name into binary parts.
   
   **Examples**
   
   ::
   
       Module.split Very.Long.Module.Name.And.Even.Longer
       #=> ["Very", "Long", "Module", "Name", "And", "Even", "Longer"]
   
   
   







