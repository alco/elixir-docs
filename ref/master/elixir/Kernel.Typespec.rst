Kernel.Typespec
==============================================================

.. elixir:module:: Kernel.Typespec

   :mtype: 

Overview
--------

Provides macros and functions for working with typespecs.

Elixir comes with a notation for declaring types and specifications.
Elixir is dynamically typed, as such typespecs are never used by the
compiler to optimize or modify code. Still, using typespecs is useful as
documentation and tools such as
`Dialyzer <http://www.erlang.org/doc/man/dialyzer.html>`__ can analyze
the code with typespecs to find bugs.

The attributes ``@type``, ``@opaque``, ``@typep``, ``@spec`` and
``@callback`` available in modules are handled by the equivalent macros
defined by this module. See sub-sections "Defining a type" and "Defining
a specification" below.

Types and their syntax
~~~~~~~~~~~~~~~~~~~~~~

The type syntax provided by Elixir is fairly similar to the one in
`Erlang <http://www.erlang.org/doc/reference_manual/typespec.html>`__.

Most of the built-in types provided in Erlang (for example, ``pid()``)
are expressed the same way: ``pid()`` or simply ``pid``. Parametrized
types are also supported (``list(integer)``) and so are remote types
(``Enum.t``).

Integers and atom literals are allowed as types (ex. ``1``, ``:atom`` or
``false``). All other types are built of unions of predefined types.
Certain shorthands are allowed, such as ``[...]``, ``<<>>`` and
``{...}``.

Predefined types
^^^^^^^^^^^^^^^^

::

    Type :: any         # the top type, the set of all terms
          | none        # the bottom type, contains no terms
          | pid
          | port
          | reference
          | Atom
          | Bitstring
          | float
          | Fun
          | Integer
          | List
          | Tuple
          | Union
          | UserDefined # Described in section "Defining a type"

    Atom :: atom
          | ElixirAtom # `:foo`, `:bar`, ...

    Bitstring :: <<>>
               | << _ :: M >>             # M is a positive integer
               | << _ :: _ * N >>         # N is a positive integer
               | << _ :: M, _ :: _ * N >>

    Fun :: (... -> any)    # any function
         | (... -> Type)   # any arity, returning Type
         | (() -> Type))
         | (TList -> Type)

    Integer :: integer
             | ElixirInteger                # ..., -1, 0, 1, ... 42 ...
             | ElixirInteger..ElixirInteger # an integer range

    List :: list(Type)                        # proper list ([]-terminated)
          | improper_list(Type1, Type2)       # Type1=contents, Type2=termination
          | maybe_improper_list(Type1, Type2) # Type1 and Type2 as above
          | nonempty_list(Type)               # proper non-empty list
          | []                                # empty list
          | [Type]                            # shorthand for list(Type)
          | [Type, ...]                       # shorthand for nonempty_list(Type)

    Tuple :: tuple     # a tuple of any size
           | {}        # empty tuple
           | {TList}

    TList :: Type
           | Type, TList

    Union :: Type1 | Type2

Bit strings
^^^^^^^^^^^

Bit string with a base size of 3:

::

    << _ :: 3 >>

Bit string with a unit size of 8:

::

    << _ :: _ * 8 >>

Anonymous functions
^^^^^^^^^^^^^^^^^^^

Any anonymous function:

::

    ((...) -> any)
    (... -> any)

Anonymous function with arity of zero:

::

    (() -> type)

Anonymous function with some arity:

::

    ((type, type) -> type)
    (type, type -> type)

Built-in types
~~~~~~~~~~~~~~

+---------------------------+-------------------------------------------------------------------------------+
| Built-in type             | Defined as                                                                    |
+===========================+===============================================================================+
| ``term``                  | ``any``                                                                       |
+---------------------------+-------------------------------------------------------------------------------+
| ``binary``                | ``<< _ :: _ * 8 >>``                                                          |
+---------------------------+-------------------------------------------------------------------------------+
| ``bitstring``             | ``<< _ :: _ * 1 >>``                                                          |
+---------------------------+-------------------------------------------------------------------------------+
| ``boolean``               | ``false`` \| ``true``                                                         |
+---------------------------+-------------------------------------------------------------------------------+
| ``byte``                  | ``0..255``                                                                    |
+---------------------------+-------------------------------------------------------------------------------+
| ``char``                  | ``0..0xffff``                                                                 |
+---------------------------+-------------------------------------------------------------------------------+
| ``number``                | ``integer`` \| ``float``                                                      |
+---------------------------+-------------------------------------------------------------------------------+
| ``list``                  | ``[any]``                                                                     |
+---------------------------+-------------------------------------------------------------------------------+
| ``maybe_improper_list``   | ``maybe_improper_list(any, any)``                                             |
+---------------------------+-------------------------------------------------------------------------------+
| ``nonempty_list``         | ``nonempty_list(any)``                                                        |
+---------------------------+-------------------------------------------------------------------------------+
| ``iodata``                | ``iolist`` \| ``binary``                                                      |
+---------------------------+-------------------------------------------------------------------------------+
| ``iolist``                | ``maybe_improper_list(byte`` \| ``binary`` \| ``iolist, binary`` \| ``[])``   |
+---------------------------+-------------------------------------------------------------------------------+
| ``module``                | ``atom``                                                                      |
+---------------------------+-------------------------------------------------------------------------------+
| ``mfa``                   | ``{atom, atom, arity}``                                                       |
+---------------------------+-------------------------------------------------------------------------------+
| ``arity``                 | ``0..255``                                                                    |
+---------------------------+-------------------------------------------------------------------------------+
| ``node``                  | ``atom``                                                                      |
+---------------------------+-------------------------------------------------------------------------------+
| ``timeout``               | ``:infinity`` \| ``non_neg_integer``                                          |
+---------------------------+-------------------------------------------------------------------------------+
| ``no_return``             | ``none``                                                                      |
+---------------------------+-------------------------------------------------------------------------------+
| ``fun``                   | ``(... -> any)``                                                              |
+---------------------------+-------------------------------------------------------------------------------+

Some built-in types cannot be expressed with valid syntax according to
the language defined above.

+-----------------------+-------------------------+
| Built-in type         | Can be interpreted as   |
+=======================+=========================+
| ``non_neg_integer``   | ``0..``                 |
+-----------------------+-------------------------+
| ``pos_integer``       | ``1..``                 |
+-----------------------+-------------------------+
| ``neg_integer``       | ``..-1``                |
+-----------------------+-------------------------+

Types defined in other modules are referred to as "remote types", they
are referenced as ``Module.type_name`` (ex. ``Enum.t`` or ``String.t``).

Defining a type
~~~~~~~~~~~~~~~

::

    @type type_name :: type
    @typep type_name :: type
    @opaque type_name :: type

A type defined with ``@typep`` is private. An opaque type, defined with
``@opaque`` is a type where the internal structure of the type will not
be visible, but the type is still public.

Types can be parametrised by defining variables as parameters, these
variables can then be used to define the type.

::

    @type dict(key, value) :: [{key, value}]

Defining a specification
~~~~~~~~~~~~~~~~~~~~~~~~

::

    @spec function_name(type1, type2) :: return_type
    @callback function_name(type1, type2) :: return_type

Callbacks are used to define the callbacks functions of behaviours (see
```Behaviour`` <Behaviour.html>`__).

Guards can be used to restrict type variables given as arguments to the
function.

::

    @spec function(arg) :: [arg] when arg: atom

Type variables with no restriction can also be defined.

::

    @spec function(arg) :: [arg] when arg: var

Specifications can be overloaded just like ordinary functions.

::

    @spec function(integer) :: atom
    @spec function(atom)    :: integer

Notes
~~~~~

Elixir discourages the use of type ``string`` as it might be confused
with binaries which are referred to as "strings" in Elixir (as opposed
to character lists). In order to use the type that is called ``string``
in Erlang, one has to use the ``char_list`` type which is a synonym for
``string``. If you use ``string``, you'll get a warning from the
compiler.

If you want to refer to the "string" type (the one operated on by
functions in the ```String`` <String.html>`__ module), use ``String.t``
type instead.





Summary
-------

================================== =
:elixir:func:`beam_callbacks/1`    Returns all callbacks available from the module's beam code 

:elixir:func:`beam_specs/1`        Returns all specs available from the module's beam code 

:elixir:func:`beam_typedocs/1`     Returns all type docs available from the module's beam code 

:elixir:func:`beam_types/1`        Returns all types available from the module's beam code 

:elixir:macro:`defcallback/1`      Defines a callback. This macro is responsible for handling the attribute ``@callback`` 

:elixir:func:`define_callback/3`   Defines a ``callback`` by receiving Erlang's typespec 

:elixir:func:`define_spec/3`       Defines a ``spec`` by receiving Erlang's typespec 

:elixir:func:`define_type/3`       Defines a ``type``, ``typep`` or ``opaque`` by receiving Erlang's typespec 

:elixir:func:`defines_callback?/3` Returns ``true`` if the current module defines a callback. This function is only available for modules being compiled 

:elixir:func:`defines_spec?/3`     Returns ``true`` if the current module defines a given spec. This function is only available for modules being compiled 

:elixir:func:`defines_type?/3`     Returns ``true`` if the current module defines a given type (private, opaque or not). This function is only available for modules being compiled 

:elixir:macro:`defopaque/1`        Defines an opaque type. This macro is responsible for handling the attribute ``@opaque`` 

:elixir:macro:`defspec/1`          Defines a spec. This macro is responsible for handling the attribute ``@spec`` 

:elixir:macro:`deftype/1`          Defines a type. This macro is responsible for handling the attribute ``@type`` 

:elixir:macro:`deftypep/1`         Defines a private type. This macro is responsible for handling the attribute ``@typep`` 

:elixir:func:`spec_to_ast/2`       Converts a spec clause back to Elixir AST 

:elixir:func:`type_to_ast/1`       Converts a type clause back to Elixir AST 
================================== =





Functions
---------

.. elixir:function:: Kernel.Typespec.beam_callbacks/1
   :sig: beam_callbacks(module)


   Specs:
   
 
   * beam_callbacks(module | binary) :: [tuple] | nil
 

   
   Returns all callbacks available from the module's beam code.
   
   The result is returned as a list of tuples where the first element is
   spec name and arity and the second is the spec.
   
   The module must have a corresponding beam file which can be located by
   the runtime system.
   
   

.. elixir:function:: Kernel.Typespec.beam_specs/1
   :sig: beam_specs(module)


   Specs:
   
 
   * beam_specs(module | binary) :: [tuple] | nil
 

   
   Returns all specs available from the module's beam code.
   
   The result is returned as a list of tuples where the first element is
   spec name and arity and the second is the spec.
   
   The module must have a corresponding beam file which can be located by
   the runtime system.
   
   

.. elixir:function:: Kernel.Typespec.beam_typedocs/1
   :sig: beam_typedocs(module)


   Specs:
   
 
   * beam_typedocs(module | binary) :: [tuple] | nil
 

   
   Returns all type docs available from the module's beam code.
   
   The result is returned as a list of tuples where the first element is
   the pair of type name and arity and the second element is the
   documentation.
   
   The module must have a corresponding beam file which can be located by
   the runtime system.
   
   

.. elixir:function:: Kernel.Typespec.beam_types/1
   :sig: beam_types(module)


   Specs:
   
 
   * beam_types(module | binary) :: [tuple] | nil
 

   
   Returns all types available from the module's beam code.
   
   The result is returned as a list of tuples where the first element is
   the type (``:typep``, ``:type`` and ``:opaque``).
   
   The module must have a corresponding beam file which can be located by
   the runtime system.
   
   

.. elixir:function:: Kernel.Typespec.define_callback/3
   :sig: define_callback(module, tuple, definition)


   
   Defines a ``callback`` by receiving Erlang's typespec.
   
   

.. elixir:function:: Kernel.Typespec.define_spec/3
   :sig: define_spec(module, tuple, definition)


   
   Defines a ``spec`` by receiving Erlang's typespec.
   
   

.. elixir:function:: Kernel.Typespec.define_type/3
   :sig: define_type(caller, kind, type)


   
   Defines a ``type``, ``typep`` or ``opaque`` by receiving Erlang's
   typespec.
   
   

.. elixir:function:: Kernel.Typespec.defines_callback?/3
   :sig: defines_callback?(module, name, arity)


   
   Returns ``true`` if the current module defines a callback. This function
   is only available for modules being compiled.
   
   

.. elixir:function:: Kernel.Typespec.defines_spec?/3
   :sig: defines_spec?(module, name, arity)


   
   Returns ``true`` if the current module defines a given spec. This
   function is only available for modules being compiled.
   
   

.. elixir:function:: Kernel.Typespec.defines_type?/3
   :sig: defines_type?(module, name, arity)


   
   Returns ``true`` if the current module defines a given type (private,
   opaque or not). This function is only available for modules being
   compiled.
   
   

.. elixir:function:: Kernel.Typespec.spec_to_ast/2
   :sig: spec_to_ast(name, arg2)


   
   Converts a spec clause back to Elixir AST.
   
   

.. elixir:function:: Kernel.Typespec.type_to_ast/1
   :sig: type_to_ast(arg1)


   
   Converts a type clause back to Elixir AST.
   
   





Macros
------

.. elixir:macro:: Kernel.Typespec.defcallback/1
   :sig: defcallback(spec)


   
   Defines a callback. This macro is responsible for handling the attribute
   ``@callback``.
   
   **Examples**
   
   ::
   
       @callback add(number, number) :: number
   
   
   

.. elixir:macro:: Kernel.Typespec.defopaque/1
   :sig: defopaque(type)


   
   Defines an opaque type. This macro is responsible for handling the
   attribute ``@opaque``.
   
   **Examples**
   
   ::
   
       @opaque my_type :: atom
   
   
   

.. elixir:macro:: Kernel.Typespec.defspec/1
   :sig: defspec(spec)


   
   Defines a spec. This macro is responsible for handling the attribute
   ``@spec``.
   
   **Examples**
   
   ::
   
       @spec add(number, number) :: number
   
   
   

.. elixir:macro:: Kernel.Typespec.deftype/1
   :sig: deftype(type)


   
   Defines a type. This macro is responsible for handling the attribute
   ``@type``.
   
   **Examples**
   
   ::
   
       @type my_type :: atom
   
   
   

.. elixir:macro:: Kernel.Typespec.deftypep/1
   :sig: deftypep(type)


   
   Defines a private type. This macro is responsible for handling the
   attribute ``@typep``.
   
   **Examples**
   
   ::
   
       @typep my_type :: atom
   
   
   





