Kernel
==============================================================

.. elixir:module:: Kernel

   :mtype: 

Overview
--------

:elixir:mod:`Kernel` provides the default macros and functions Elixir imports into
your environment. These macros and functions can be skipped or
cherry-picked via the ``import`` macro. For instance, if you want to
tell Elixir not to import the ``if`` macro, you can do:

::

    import Kernel, except: [if: 2]

Elixir also has special forms that are always imported and cannot be
skipped. These are described in :elixir:mod:`Kernel.SpecialForms`.

Some of the functions described in this module are inlined by the Elixir
compiler into their Erlang counterparts in the ``:erlang`` module. Those
functions are called BIFs (builtin internal functions) in Erlang-land
and they exhibit interesting properties, as some of them are allowed in
guards and others are used for compiler optimizations.

Most of the inlined functions can be seen in effect when capturing the
function:

::

    iex> &Kernel.is_atom/1
    &:erlang.is_atom/1

Those functions will be explicitly marked in their docs as "inlined by
the compiler".





Summary
-------

=================================== =
:elixir:macro:`!/1`                 Receives any argument and returns ``true`` if it is ``false`` or ``nil``. Returns ``false`` otherwise. Not allowed in guard clauses 

:elixir:func:`!=/2`                 Returns ``true`` if the two items are not equal 

:elixir:func:`!==/2`                Returns ``true`` if the two items do not match 

:elixir:macro:`&&/2`                Provides a short-circuit operator that evaluates and returns the second expression only if the first one evaluates to true (i.e. it is not nil nor false). Returns the first expression otherwise 

:elixir:func:`*/2`                  Arithmetic multiplication 

:elixir:func:`++/2`                 Concatenates two lists 

:elixir:func:`+/1`                  Arithmetic unary plus 

:elixir:func:`+/2`                  Arithmetic plus 

:elixir:func:`--/2`                 Removes the first occurrence of an item on the left for each item on the right 

:elixir:func:`-/1`                  Arithmetic unary minus 

:elixir:func:`-/2`                  Arithmetic minus 

:elixir:macro:`../2`                Returns a range with the specified start and end. Includes both ends 

:elixir:func:`//2`                  Arithmetic division 

:elixir:func:`</2`                  Returns ``true`` if left is less than right 

:elixir:func:`<=/2`                 Returns ``true`` if left is less than or equal to right 

:elixir:macro:`<>/2`                Concatenates two binaries 

:elixir:func:`==/2`                 Returns ``true`` if the two items are equal 

:elixir:func:`===/2`                Returns ``true`` if the two items are match 

:elixir:func:`=~/2`                 Matches the term on the left against the regular expression or string on the right. Returns true if ``left`` matches ``right`` (if it's a regular expression) or contains ``right`` (if it's a string) 

:elixir:func:`>/2`                  Returns ``true`` if left is more than right 

:elixir:func:`>=/2`                 Returns ``true`` if left is more than or equal to right 

:elixir:macro:`@/1`                 Read and write attributes of th current module 

:elixir:func:`abs/1`                Returns an integer or float which is the arithmetical absolute value of ``number`` 

:elixir:macro:`alias!/1`            When used inside quoting, marks that the alias should not be hygienezed. This means the alias will be expanded when the macro is expanded 

:elixir:macro:`and/2`               Boolean and. Requires only the first argument to be a boolean since it short-circuits 

:elixir:func:`apply/2`              Invokes the given ``fun`` with the array of arguments ``args`` 

:elixir:func:`apply/3`              Invokes the given ``fun`` from ``module`` with the array of arguments ``args`` 

:elixir:func:`binary_part/3`        Extracts the part of the binary starting at ``start`` with length ``length``. Binaries are zero-indexed 

:elixir:macro:`binding/0`           Returns the binding as a keyword list where the variable name is the key and the variable value is the value 

:elixir:macro:`binding/1`           Receives a list of atoms at compilation time and returns the binding of the given variables as a keyword list where the variable name is the key and the variable value is the value 

:elixir:macro:`binding/2`           Receives a list of atoms at compilation time and returns the binding of the given variables in the given context as a keyword list where the variable name is the key and the variable value is the value 

:elixir:func:`bit_size/1`           Returns an integer which is the size in bits of ``bitstring`` 

:elixir:func:`byte_size/1`          Returns the number of bytes needed to contain ``bitstring`` 

:elixir:macro:`cond/1`              Evaluates the expression corresponding to the first clause that evaluates to true. Raises an error if all conditions evaluate to to nil or false 

:elixir:macro:`def/2`               Defines a function with the given name and contents 

:elixir:macro:`defdelegate/2`       Defines the given functions in the current module that will delegate to the given ``target``. Functions defined with ``defdelegate`` are public and are allowed to be invoked from external. If you find yourself wishing to define a delegation as private, you should likely use import instead 

:elixir:macro:`defexception/1`      Defines an exception 

:elixir:macro:`defimpl/3`           Defines an implementation for the given protocol. See :elixir:func:`defprotocol/2` for examples 

:elixir:macro:`defmacro/2`          Defines a macro with the given name and contents 

:elixir:macro:`defmacrop/2`         Defines a macro that is private. Private macros are only accessible from the same module in which they are defined 

:elixir:macro:`defmodule/2`         Defines a module given by name with the given contents 

:elixir:macro:`defoverridable/1`    Makes the given functions in the current module overridable. An overridable function is lazily defined, allowing a developer to customize it 

:elixir:macro:`defp/2`              Defines a function that is private. Private functions are only accessible from within the module in which they are defined 

:elixir:macro:`defprotocol/2`       Defines a protocol 

:elixir:macro:`defstruct/1`         Defines a struct for the current module 

:elixir:macro:`destructure/2`       Allows you to destructure two lists, assigning each term in the right to the matching term in the left. Unlike pattern matching via ``=``, if the sizes of the left and right lists don't match, destructuring simply stops instead of raising an error 

:elixir:func:`div/2`                Performs an integer division 

:elixir:func:`elem/2`               Get the element at the zero-based ``index`` in ``tuple`` 

:elixir:func:`exit/1`               Stops the execution of the calling process with the given reason 

:elixir:func:`function_exported?/3` Returns true if the ``module`` is loaded and contains a public ``function`` with the given ``arity``, otherwise false 

:elixir:func:`hd/1`                 Returns the head of a list, raises ``badarg`` if the list is empty 

:elixir:macro:`if/2`                Provides an ``if`` macro. This macro expects the first argument to be a condition and the rest are keyword arguments 

:elixir:macro:`in/2`                Checks if the element on the left side is member of the collection on the right side 

:elixir:func:`inspect/2`            Inspect the given argument according to the :elixir:mod:`Inspect` protocol. The second argument is a keywords list with options to control inspection 

:elixir:func:`is_atom/1`            Returns ``true`` if ``term`` is an atom; otherwise returns ``false`` 

:elixir:func:`is_binary/1`          Returns ``true`` if ``term`` is a binary; otherwise returns ``false`` 

:elixir:func:`is_bitstring/1`       Returns ``true`` if ``term`` is a bitstring (including a binary); otherwise returns ``false`` 

:elixir:func:`is_boolean/1`         Returns ``true`` if ``term`` is either the atom ``true`` or the atom ``false`` (i.e. a boolean); otherwise returns false 

:elixir:func:`is_float/1`           Returns ``true`` if ``term`` is a floating point number; otherwise returns ``false`` 

:elixir:func:`is_function/1`        Returns ``true`` if ``term`` is a function; otherwise returns ``false`` 

:elixir:func:`is_function/2`        Returns ``true`` if ``term`` is a function that can be applied with ``arity`` number of arguments; otherwise returns ``false`` 

:elixir:func:`is_integer/1`         Returns ``true`` if ``term`` is an integer; otherwise returns ``false`` 

:elixir:func:`is_list/1`            Returns ``true`` if ``term`` is a list with zero or more elements; otherwise returns ``false`` 

:elixir:func:`is_map/1`             Returns ``true`` if ``term`` is a map; otherwise returns ``false`` 

:elixir:func:`is_number/1`          Returns ``true`` if ``term`` is either an integer or a floating point number; otherwise returns ``false`` 

:elixir:func:`is_pid/1`             Returns ``true`` if ``term`` is a pid (process identifier); otherwise returns ``false`` 

:elixir:func:`is_port/1`            Returns ``true`` if ``term`` is a port identifier; otherwise returns ``false`` 

:elixir:func:`is_reference/1`       Returns ``true`` if ``term`` is a reference; otherwise returns ``false`` 

:elixir:func:`is_tuple/1`           Returns ``true`` if ``term`` is a tuple; otherwise returns ``false`` 

:elixir:func:`length/1`             Returns the length of ``list`` 

:elixir:func:`macro_exported?/3`    Returns true if the ``module`` is loaded and contains a public ``macro`` with the given ``arity``, otherwise false 

:elixir:func:`make_ref/0`           Returns an almost unique reference 

:elixir:func:`map_size/1`           Returns the size of a map 

:elixir:macro:`match?/2`            A convenient macro that checks if the right side matches the left side. The left side is allowed to be a match pattern 

:elixir:func:`max/2`                Return the biggest of the two given terms according to Erlang's term ordering. If the terms compare equal, the first one is returned 

:elixir:func:`min/2`                Return the smallest of the two given terms according to Erlang's term ordering. If the terms compare equal, the first one is returned 

:elixir:macro:`nil?/1`              Checks if the given argument is nil or not. Allowed in guard clauses 

:elixir:func:`node/0`               Returns an atom representing the name of the local node. If the node is not alive, ``:nonode@nohost`` is returned instead 

:elixir:func:`node/1`               Returns the node where the given argument is located. The argument can be a pid, a reference, or a port. If the local node is not alive, ``nonode@nohost`` is returned 

:elixir:func:`not/1`                Boolean not. Argument must be a boolean 

:elixir:macro:`or/2`                Boolean or. Requires only the first argument to be a boolean since it short-circuits 

:elixir:func:`put_elem/3`           Sets the element in ``tuple`` at the zero-based ``index`` to the given ``value`` 

:elixir:macro:`raise/1`             Raises an exception 

:elixir:macro:`raise/2`             Raises an exception 

:elixir:func:`rem/2`                Calculates the remainder of an integer division 

:elixir:macro:`reraise/2`           Raises an exception preserving a previous stacktrace 

:elixir:macro:`reraise/3`           Raises an exception preserving a previous stacktrace 

:elixir:func:`round/1`              Returns an integer by rounding the given number 

:elixir:func:`self/0`               Returns the pid (process identifier) of the calling process 

:elixir:func:`send/2`               Sends a message to the given ``dest`` and returns the message 

:elixir:macro:`sigil_C/2`           Handles the sigil ~C. It simply returns a char list without escaping characters and without interpolations 

:elixir:macro:`sigil_R/2`           Handles the sigil ~R. It returns a Regex pattern without escaping nor interpreting interpolations 

:elixir:macro:`sigil_S/2`           Handles the sigil ~S. It simply returns a string without escaping characters and without interpolations 

:elixir:macro:`sigil_W/2`           Handles the sigil ~W. It returns a list of "words" split by whitespace without escaping nor interpreting interpolations 

:elixir:macro:`sigil_c/2`           Handles the sigil ~c. It returns a char list as if it were a single quoted string, unescaping characters and replacing interpolations 

:elixir:macro:`sigil_r/2`           Handles the sigil ~r. It returns a Regex pattern 

:elixir:macro:`sigil_s/2`           Handles the sigil ~s. It returns a string as if it was double quoted string, unescaping characters and replacing interpolations 

:elixir:macro:`sigil_w/2`           Handles the sigil ~w. It returns a list of "words" split by whitespace 

:elixir:func:`size/1`               Returns the size of the given argument, which must be a tuple or a binary 

:elixir:func:`spawn/1`              Spawns the given function and returns its pid 

:elixir:func:`spawn/3`              Spawns the given module and function passing the given args and returns its pid 

:elixir:func:`spawn_link/1`         Spawns the given function, links it to the current process and returns its pid 

:elixir:func:`spawn_link/3`         Spawns the given module and function passing the given args, links it to the current process and returns its pid 

:elixir:func:`spawn_monitor/1`      Spawns the given function, monitors it and returns its pid and monitoring reference 

:elixir:func:`spawn_monitor/3`      Spawns the given module and function passing the given args, monitors it and returns its pid and monitoring reference 

:elixir:func:`struct/2`             Creates and updates structs 

:elixir:func:`throw/1`              A non-local return from a function. Check :elixir:func:`Kernel.SpecialForms.try/1` for more information 

:elixir:func:`tl/1`                 Returns the tail of a list. Raises :elixir:mod:`ArgumentError` if the list is empty 

:elixir:macro:`to_char_list/1`      Convert the argument to a list according to the List.Chars protocol 

:elixir:macro:`to_string/1`         Converts the argument to a string according to the String.Chars protocol. This is the function invoked when there is string interpolation 

:elixir:func:`trunc/1`              Returns an integer by truncating the given number 

:elixir:func:`tuple_size/1`         Returns the size of a tuple 

:elixir:macro:`unless/2`            Evaluates and returns the do-block passed in as a second argument unless clause evaluates to true. Returns nil otherwise. See also ``if`` 

:elixir:macro:`use/2`               ``use`` is a simple mechanism for using a given module into the current context 

:elixir:macro:`var!/2`              When used inside quoting, marks that the variable should not be hygienized. The argument can be either a variable unquoted or an atom representing the variable name 

:elixir:func:`xor/2`                Boolean exclusive-or. Arguments must be booleans. Returns ``true`` if and only if both arguments are different 

:elixir:macro:`|>/2`                ``|>`` is the pipe operator 

:elixir:macro:`||/2`                Provides a short-circuit operator that evaluates and returns the second expression only if the first one does not evaluate to true (i.e. it is either nil or false). Returns the first expression otherwise 
=================================== =





Functions
---------

.. elixir:function:: Kernel.!=/2
   :sig: left != right


   Specs:
   
 
   * term != term :: boolean
 

   
   Returns ``true`` if the two items are not equal.
   
   This operator considers 1 and 1.0 to be equal. For match comparison, use
   ``!==`` instead.
   
   All terms in Elixir can be compared with each other.
   
   Allowed in guard tests. Inlined by the compiler.
   
   **Examples**
   
   ::
   
       iex> 1 != 2
       true
   
       iex> 1 != 1.0
       false
   
   
   

.. elixir:function:: Kernel.!==/2
   :sig: left !== right


   Specs:
   
 
   * term !== term :: boolean
 

   
   Returns ``true`` if the two items do not match.
   
   All terms in Elixir can be compared with each other.
   
   Allowed in guard tests. Inlined by the compiler.
   
   **Examples**
   
   ::
   
       iex> 1 !== 2
       true
   
       iex> 1 !== 1.0
       true
   
   
   

.. elixir:function:: Kernel.*/2
   :sig: left * right


   Specs:
   
 
   * number * number :: number
 

   
   Arithmetic multiplication.
   
   Allowed in guard tests. Inlined by the compiler.
   
   **Examples**
   
   ::
   
       iex> 1 * 2
       2
   
   
   

.. elixir:function:: Kernel.+/1
   :sig: +value


   Specs:
   
 
   * +number :: number
 

   
   Arithmetic unary plus.
   
   Allowed in guard tests. Inlined by the compiler.
   
   **Examples**
   
   ::
   
       iex> +1
       1
   
   
   

.. elixir:function:: Kernel.+/2
   :sig: left + right


   Specs:
   
 
   * number + number :: number
 

   
   Arithmetic plus.
   
   Allowed in guard tests. Inlined by the compiler.
   
   **Examples**
   
   ::
   
       iex> 1 + 2
       3
   
   
   

.. elixir:function:: Kernel.++/2
   :sig: left ++ right


   Specs:
   
 
   * [] ++ term :: maybe_improper_list
 

   
   Concatenates two lists.
   
   Allowed in guard tests. Inlined by the compiler.
   
   **Examples**
   
   ::
   
       iex> [1] ++ [2, 3]
       [1,2,3]
   
       iex> 'foo' ++ 'bar'
       'foobar'
   
   
   

.. elixir:function:: Kernel.-/1
   :sig: -value


   Specs:
   
 
   * -number :: number
 

   
   Arithmetic unary minus.
   
   Allowed in guard tests. Inlined by the compiler.
   
   **Examples**
   
   ::
   
       iex> -2
       -2
   
   
   

.. elixir:function:: Kernel.-/2
   :sig: left - right


   Specs:
   
 
   * number - number :: number
 

   
   Arithmetic minus.
   
   Allowed in guard tests. Inlined by the compiler.
   
   **Examples**
   
   ::
   
       iex> 1 - 2
       -1
   
   
   

.. elixir:function:: Kernel.--/2
   :sig: left -- right


   Specs:
   
 
   * [] -- [] :: []
 

   
   Removes the first occurrence of an item on the left for each item on the
   right.
   
   Allowed in guard tests. Inlined by the compiler.
   
   **Examples**
   
   ::
   
       iex> [1, 2, 3] -- [1, 2]
       [3]
   
       iex> [1, 2, 3, 2, 1] -- [1, 2, 2]
       [3,1]
   
   
   

.. elixir:function:: Kernel.//2
   :sig: left / right


   Specs:
   
 
   * number / number :: float
 

   
   Arithmetic division.
   
   The result is always a float. Use ``div`` and ``rem`` if you want a
   natural division or the remainder.
   
   Allowed in guard tests. Inlined by the compiler.
   
   **Examples**
   
   ::
   
       iex> 1 / 2
       0.5
   
       iex> 2 / 1
       2.0
   
   
   

.. elixir:function:: Kernel.</2
   :sig: left < right


   Specs:
   
 
   * term < term :: boolean
 

   
   Returns ``true`` if left is less than right.
   
   All terms in Elixir can be compared with each other.
   
   Allowed in guard tests. Inlined by the compiler.
   
   **Examples**
   
   ::
   
       iex> 1 < 2
       true
   
   
   

.. elixir:function:: Kernel.<=/2
   :sig: left <= right


   Specs:
   
 
   * term <= term :: boolean
 

   
   Returns ``true`` if left is less than or equal to right.
   
   All terms in Elixir can be compared with each other.
   
   Allowed in guard tests. Inlined by the compiler.
   
   **Examples**
   
   ::
   
       iex> 1 <= 2
       true
   
   
   

.. elixir:function:: Kernel.==/2
   :sig: left == right


   Specs:
   
 
   * term == term :: boolean
 

   
   Returns ``true`` if the two items are equal.
   
   This operator considers 1 and 1.0 to be equal. For match semantics, use
   ``===`` instead.
   
   All terms in Elixir can be compared with each other.
   
   Allowed in guard tests. Inlined by the compiler.
   
   **Examples**
   
   ::
   
       iex> 1 == 2
       false
   
       iex> 1 == 1.0
       true
   
   
   

.. elixir:function:: Kernel.===/2
   :sig: left === right


   Specs:
   
 
   * term === term :: boolean
 

   
   Returns ``true`` if the two items are match.
   
   This operator gives the same semantics as the one existing in pattern
   matching, i.e., ``1`` and ``1.0`` are equal, but they do not match.
   
   All terms in Elixir can be compared with each other.
   
   Allowed in guard tests. Inlined by the compiler.
   
   **Examples**
   
   ::
   
       iex> 1 === 2
       false
   
       iex> 1 === 1.0
       false
   
   
   

.. elixir:function:: Kernel.=~/2
   :sig: left =~ right


   
   Matches the term on the left against the regular expression or string on
   the right. Returns true if ``left`` matches ``right`` (if it's a regular
   expression) or contains ``right`` (if it's a string).
   
   **Examples**
   
   ::
   
       iex> "abcd" =~ ~r/c(d)/
       true
   
       iex> "abcd" =~ ~r/e/
       false
   
       iex> "abcd" =~ "bc"
       true
   
       iex> "abcd" =~ "ad"
       false
   
   
   

.. elixir:function:: Kernel.>/2
   :sig: left > right


   Specs:
   
 
   * term > term :: boolean
 

   
   Returns ``true`` if left is more than right.
   
   All terms in Elixir can be compared with each other.
   
   Allowed in guard tests. Inlined by the compiler.
   
   **Examples**
   
   ::
   
       iex> 1 > 2
       false
   
   
   

.. elixir:function:: Kernel.>=/2
   :sig: left >= right


   Specs:
   
 
   * term >= term :: boolean
 

   
   Returns ``true`` if left is more than or equal to right.
   
   All terms in Elixir can be compared with each other.
   
   Allowed in guard tests. Inlined by the compiler.
   
   **Examples**
   
   ::
   
       iex> 1 >= 2
       false
   
   
   

.. elixir:function:: Kernel.abs/1
   :sig: abs(number)


   Specs:
   
 
   * abs(number) :: number
 

   
   Returns an integer or float which is the arithmetical absolute value of
   ``number``.
   
   Allowed in guard tests. Inlined by the compiler.
   
   **Examples**
   
   ::
   
       iex> abs(-3.33)
       3.33
   
       iex> abs(-3)
       3
   
   
   

.. elixir:function:: Kernel.apply/2
   :sig: apply(fun, args)


   Specs:
   
 
   * apply((... -> any), [any]) :: any
 

   
   Invokes the given ``fun`` with the array of arguments ``args``.
   
   Inlined by the compiler.
   
   **Examples**
   
   ::
   
       iex> apply(fn x -> x * 2 end, [2])
       4
   
   
   

.. elixir:function:: Kernel.apply/3
   :sig: apply(module, fun, args)


   Specs:
   
 
   * apply(module, atom, [any]) :: any
 

   
   Invokes the given ``fun`` from ``module`` with the array of arguments
   ``args``.
   
   Inlined by the compiler.
   
   **Examples**
   
   ::
   
       iex> apply(Enum, :reverse, [[1, 2, 3]])
       [3,2,1]
   
   
   

.. elixir:function:: Kernel.binary_part/3
   :sig: binary_part(binary, start, length)


   Specs:
   
 
   * binary_part(binary, pos_integer, integer) :: binary
 

   
   Extracts the part of the binary starting at ``start`` with length
   ``length``. Binaries are zero-indexed.
   
   If start or length references in any way outside the binary, an
   :elixir:mod:`ArgumentError` exception is raised.
   
   Allowed in guard tests. Inlined by the compiler.
   
   **Examples**
   
   ::
   
       iex> binary_part("foo", 1, 2)
       "oo"
   
   A negative length can be used to extract bytes at the end of a binary:
   
   ::
   
       iex> binary_part("foo", 3, -1)
       "o"
   
   
   

.. elixir:function:: Kernel.bit_size/1
   :sig: bit_size(bitstring)


   Specs:
   
 
   * bit_size(bitstring) :: non_neg_integer
 

   
   Returns an integer which is the size in bits of ``bitstring``.
   
   Allowed in guard tests. Inlined by the compiler.
   
   **Examples**
   
   ::
   
       iex> bit_size(<<433::16, 3::3>>)
       19
   
       iex> bit_size(<<1, 2, 3>>)
       24
   
   
   

.. elixir:function:: Kernel.byte_size/1
   :sig: byte_size(bitstring)


   Specs:
   
 
   * byte_size(bitstring) :: non_neg_integer
 

   
   Returns the number of bytes needed to contain ``bitstring``.
   
   That is, if the number of bits in ``bitstring`` is not divisible by 8,
   the resulting number of bytes will be rounded up. This operation happens
   in constant time.
   
   Allowed in guard tests. Inlined by the compiler.
   
   **Examples**
   
   ::
   
       iex> byte_size(<<433::16, 3::3>>)
       3
   
       iex> byte_size(<<1, 2, 3>>)
       3
   
   
   

.. elixir:function:: Kernel.div/2
   :sig: div(left, right)


   Specs:
   
 
   * div(integer, integer) :: integer
 

   
   Performs an integer division.
   
   Raises an error if one of the arguments is not an integer.
   
   Allowed in guard tests. Inlined by the compiler.
   
   **Examples**
   
   ::
   
       iex> div(5, 2)
       2
   
   
   

.. elixir:function:: Kernel.elem/2
   :sig: elem(tuple, index)


   Specs:
   
 
   * elem(tuple, non_neg_integer) :: term
 

   
   Get the element at the zero-based ``index`` in ``tuple``.
   
   Allowed in guard tests. Inlined by the compiler.
   
   **Example**
   
   ::
   
       iex> tuple = {:foo, :bar, 3}
       iex> elem(tuple, 1)
       :bar
   
   
   

.. elixir:function:: Kernel.exit/1
   :sig: exit(reason)


   Specs:
   
 
   * exit(term) :: no_return
 

   
   Stops the execution of the calling process with the given reason.
   
   Since evaluating this function causes the process to terminate, it has
   no return value.
   
   Inlined by the compiler.
   
   **Examples**
   
   ::
   
       exit(:normal)
       exit(:seems_bad)
   
   
   

.. elixir:function:: Kernel.function_exported?/3
   :sig: function_exported?(module, function, arity)


   Specs:
   
 
   * function_exported?(atom | tuple, atom, integer) :: boolean
 

   
   Returns true if the ``module`` is loaded and contains a public
   ``function`` with the given ``arity``, otherwise false.
   
   Notice that this function does not load the module in case it is not
   loaded. Check :elixir:func:`Code.ensure_loaded/1` for more information.
   
   

.. elixir:function:: Kernel.hd/1
   :sig: hd(list)


   Specs:
   
 
   * hd([]) :: term
 

   
   Returns the head of a list, raises ``badarg`` if the list is empty.
   
   Inlined by the compiler.
   
   

.. elixir:function:: Kernel.inspect/2
   :sig: inspect(arg, opts \\ [])


   Specs:
   
 
   * inspect(:elixir:type:`Inspect.t/0`, :elixir:type:`Keyword.t/0`) :: :elixir:type:`String.t/0`
 

   
   Inspect the given argument according to the :elixir:mod:`Inspect` protocol. The
   second argument is a keywords list with options to control inspection.
   
   **Options**
   
   :elixir:func:`inspect/2` accepts a list of options that are internally translated
   to an :elixir:mod:`Inspect.Opts` struct. Check the docs for :elixir:mod:`Inspect.Opts` to
   see the supported options.
   
   **Examples**
   
   ::
   
       iex> inspect(:foo)
       ":foo"
   
       iex> inspect [1, 2, 3, 4, 5], limit: 3
       "[1, 2, 3, ...]"
   
       iex> inspect("josé" <> <<0>>)
       "<<106, 111, 115, 195, 169, 0>>"
   
       iex> inspect("josé" <> <<0>>, binaries: :as_strings)
       "\"josé\\000\""
   
       iex> inspect("josé", binaries: :as_binaries)
       "<<106, 111, 115, 195, 169>>"
   
   Note that the inspect protocol does not necessarily return a valid
   representation of an Elixir term. In such cases, the inspected result
   must start with ``#``. For example, inspecting a function will return:
   
   ::
   
       inspect fn a, b -> a + b end
       #=> #Function<...>
   
   
   

.. elixir:function:: Kernel.is_atom/1
   :sig: is_atom(term)


   Specs:
   
 
   * is_atom(term) :: boolean
 

   
   Returns ``true`` if ``term`` is an atom; otherwise returns ``false``.
   
   Allowed in guard tests. Inlined by the compiler.
   
   

.. elixir:function:: Kernel.is_binary/1
   :sig: is_binary(term)


   Specs:
   
 
   * is_binary(term) :: boolean
 

   
   Returns ``true`` if ``term`` is a binary; otherwise returns ``false``.
   
   A binary always contains a complete number of bytes.
   
   Allowed in guard tests. Inlined by the compiler.
   
   

.. elixir:function:: Kernel.is_bitstring/1
   :sig: is_bitstring(term)


   Specs:
   
 
   * is_bitstring(term) :: boolean
 

   
   Returns ``true`` if ``term`` is a bitstring (including a binary);
   otherwise returns ``false``.
   
   Allowed in guard tests. Inlined by the compiler.
   
   

.. elixir:function:: Kernel.is_boolean/1
   :sig: is_boolean(term)


   Specs:
   
 
   * is_boolean(term) :: boolean
 

   
   Returns ``true`` if ``term`` is either the atom ``true`` or the atom
   ``false`` (i.e. a boolean); otherwise returns false.
   
   Allowed in guard tests. Inlined by the compiler.
   
   

.. elixir:function:: Kernel.is_float/1
   :sig: is_float(term)


   Specs:
   
 
   * is_float(term) :: boolean
 

   
   Returns ``true`` if ``term`` is a floating point number; otherwise
   returns ``false``.
   
   Allowed in guard tests. Inlined by the compiler.
   
   

.. elixir:function:: Kernel.is_function/1
   :sig: is_function(term)


   Specs:
   
 
   * is_function(term) :: boolean
 

   
   Returns ``true`` if ``term`` is a function; otherwise returns ``false``.
   
   Allowed in guard tests. Inlined by the compiler.
   
   

.. elixir:function:: Kernel.is_function/2
   :sig: is_function(term, arity)


   Specs:
   
 
   * is_function(term, non_neg_integer) :: boolean
 

   
   Returns ``true`` if ``term`` is a function that can be applied with
   ``arity`` number of arguments; otherwise returns ``false``.
   
   Allowed in guard tests. Inlined by the compiler.
   
   

.. elixir:function:: Kernel.is_integer/1
   :sig: is_integer(term)


   Specs:
   
 
   * is_integer(term) :: boolean
 

   
   Returns ``true`` if ``term`` is an integer; otherwise returns ``false``.
   
   Allowed in guard tests. Inlined by the compiler.
   
   

.. elixir:function:: Kernel.is_list/1
   :sig: is_list(term)


   Specs:
   
 
   * is_list(term) :: boolean
 

   
   Returns ``true`` if ``term`` is a list with zero or more elements;
   otherwise returns ``false``.
   
   Allowed in guard tests. Inlined by the compiler.
   
   

.. elixir:function:: Kernel.is_map/1
   :sig: is_map(term)


   Specs:
   
 
   * is_map(term) :: boolean
 

   
   Returns ``true`` if ``term`` is a map; otherwise returns ``false``.
   
   Allowed in guard tests. Inlined by the compiler.
   
   

.. elixir:function:: Kernel.is_number/1
   :sig: is_number(term)


   Specs:
   
 
   * is_number(term) :: boolean
 

   
   Returns ``true`` if ``term`` is either an integer or a floating point
   number; otherwise returns ``false``.
   
   Allowed in guard tests. Inlined by the compiler.
   
   

.. elixir:function:: Kernel.is_pid/1
   :sig: is_pid(term)


   Specs:
   
 
   * is_pid(term) :: boolean
 

   
   Returns ``true`` if ``term`` is a pid (process identifier); otherwise
   returns ``false``.
   
   Allowed in guard tests. Inlined by the compiler.
   
   

.. elixir:function:: Kernel.is_port/1
   :sig: is_port(term)


   Specs:
   
 
   * is_port(term) :: boolean
 

   
   Returns ``true`` if ``term`` is a port identifier; otherwise returns
   ``false``.
   
   Allowed in guard tests. Inlined by the compiler.
   
   

.. elixir:function:: Kernel.is_reference/1
   :sig: is_reference(term)


   Specs:
   
 
   * is_reference(term) :: boolean
 

   
   Returns ``true`` if ``term`` is a reference; otherwise returns
   ``false``.
   
   Allowed in guard tests. Inlined by the compiler.
   
   

.. elixir:function:: Kernel.is_tuple/1
   :sig: is_tuple(term)


   Specs:
   
 
   * is_tuple(term) :: boolean
 

   
   Returns ``true`` if ``term`` is a tuple; otherwise returns ``false``.
   
   Allowed in guard tests. Inlined by the compiler.
   
   

.. elixir:function:: Kernel.length/1
   :sig: length(list)


   Specs:
   
 
   * length([]) :: non_neg_integer
 

   
   Returns the length of ``list``.
   
   Allowed in guard tests. Inlined by the compiler.
   
   **Examples**
   
   ::
   
       iex> length([1, 2, 3, 4, 5, 6, 7, 8, 9])
       9
   
   
   

.. elixir:function:: Kernel.macro_exported?/3
   :sig: macro_exported?(module, macro, arity)


   Specs:
   
 
   * macro_exported?(atom, atom, integer) :: boolean
 

   
   Returns true if the ``module`` is loaded and contains a public ``macro``
   with the given ``arity``, otherwise false.
   
   Notice that this function does not load the module in case it is not
   loaded. Check :elixir:func:`Code.ensure_loaded/1` for more information.
   
   

.. elixir:function:: Kernel.make_ref/0
   :sig: make_ref()


   Specs:
   
 
   * make_ref :: reference
 

   
   Returns an almost unique reference.
   
   The returned reference will re-occur after approximately 2^82 calls;
   therefore it is unique enough for practical purposes.
   
   Inlined by the compiler.
   
   **Examples**
   
   ::
   
       make_ref() #=> #Reference<0.0.0.135>
   
   
   

.. elixir:function:: Kernel.map_size/1
   :sig: map_size(map)


   Specs:
   
 
   * map_size(%{}) :: non_neg_integer
 

   
   Returns the size of a map.
   
   This operation happens in constant time.
   
   Allowed in guard tests. Inlined by the compiler.
   
   

.. elixir:function:: Kernel.max/2
   :sig: max(first, second)


   Specs:
   
 
   * max(term, term) :: term
 

   
   Return the biggest of the two given terms according to Erlang's term
   ordering. If the terms compare equal, the first one is returned.
   
   Inlined by the compiler.
   
   **Examples**
   
   ::
   
       iex> max(1, 2)
       2
   
   
   

.. elixir:function:: Kernel.min/2
   :sig: min(first, second)


   Specs:
   
 
   * min(term, term) :: term
 

   
   Return the smallest of the two given terms according to Erlang's term
   ordering. If the terms compare equal, the first one is returned.
   
   Inlined by the compiler.
   
   **Examples**
   
   ::
   
       iex> min(1, 2)
       1
   
   
   

.. elixir:function:: Kernel.node/0
   :sig: node()


   Specs:
   
 
   * node :: node
 

   
   Returns an atom representing the name of the local node. If the node is
   not alive, ``:nonode@nohost`` is returned instead.
   
   Allowed in guard tests. Inlined by the compiler.
   
   

.. elixir:function:: Kernel.node/1
   :sig: node(arg)


   Specs:
   
 
   * node(pid | reference | port) :: node
 

   
   Returns the node where the given argument is located. The argument can
   be a pid, a reference, or a port. If the local node is not alive,
   ``nonode@nohost`` is returned.
   
   Allowed in guard tests. Inlined by the compiler.
   
   

.. elixir:function:: Kernel.not/1
   :sig: not arg


   Specs:
   
 
   * not boolean :: boolean
 

   
   Boolean not. Argument must be a boolean.
   
   Allowed in guard tests. Inlined by the compiler.
   
   **Examples**
   
   ::
   
       iex> not false
       true
   
   
   

.. elixir:function:: Kernel.put_elem/3
   :sig: put_elem(tuple, index, value)


   Specs:
   
 
   * put_elem(tuple, non_neg_integer, term) :: tuple
 

   
   Sets the element in ``tuple`` at the zero-based ``index`` to the given
   ``value``.
   
   Inlined by the compiler.
   
   **Example**
   
   ::
   
       iex> tuple = {:foo, :bar, 3}
       iex> put_elem(tuple, 0, :baz)
       {:baz, :bar, 3}
   
   
   

.. elixir:function:: Kernel.rem/2
   :sig: rem(left, right)


   Specs:
   
 
   * rem(integer, integer) :: integer
 

   
   Calculates the remainder of an integer division.
   
   Raises an error if one of the arguments is not an integer.
   
   Allowed in guard tests. Inlined by the compiler.
   
   **Examples**
   
   ::
   
       iex> rem(5, 2)
       1
   
   
   

.. elixir:function:: Kernel.round/1
   :sig: round(number)


   Specs:
   
 
   * round(number) :: integer
 

   
   Returns an integer by rounding the given number.
   
   Allowed in guard tests. Inlined by the compiler.
   
   **Examples**
   
   ::
   
       iex> round(5.5)
       6
   
   
   

.. elixir:function:: Kernel.self/0
   :sig: self()


   Specs:
   
 
   * self :: pid
 

   
   Returns the pid (process identifier) of the calling process.
   
   Allowed in guard clauses. Inlined by the compiler.
   
   

.. elixir:function:: Kernel.send/2
   :sig: send(dest, msg)


   Specs:
   
 
   * (send(dest :: pid | port | atom | {atom, node}, msg) :: msg) when msg: any
 

   
   Sends a message to the given ``dest`` and returns the message.
   
   ``dest`` may be a remote or local pid, a (local) port, a locally
   registered name, or a tuple ``{registered_name, node}`` for a registered
   name at another node.
   
   Inlined by the compiler.
   
   **Examples**
   
   ::
   
       iex> send self(), :hello
       :hello
   
   
   

.. elixir:function:: Kernel.size/1
   :sig: size(arg)


   Specs:
   
 
   * size(tuple | binary) :: non_neg_integer
 

   
   Returns the size of the given argument, which must be a tuple or a
   binary.
   
   Prefer using :elixir:func:`tuple_size/1` or :elixir:func:`byte_size/1` instead.
   
   Allowed in guard tests. Inlined by the compiler.
   
   

.. elixir:function:: Kernel.spawn/1
   :sig: spawn(fun)


   Specs:
   
 
   * spawn((() -> any)) :: pid
 

   
   Spawns the given function and returns its pid.
   
   Check the modules :elixir:mod:`Process` and :elixir:mod:`Node` for other functions to handle
   processes, including spawning functions in nodes.
   
   Inlined by the compiler.
   
   **Examples**
   
   ::
   
       current = Kernel.self
       child   = spawn(fn -> send current, {Kernel.self, 1 + 2} end)
   
       receive do
         {^child, 3} -> IO.puts "Received 3 back"
       end
   
   
   

.. elixir:function:: Kernel.spawn/3
   :sig: spawn(module, fun, args)


   Specs:
   
 
   * spawn(module, atom, []) :: pid
 

   
   Spawns the given module and function passing the given args and returns
   its pid.
   
   Check the modules :elixir:mod:`Process` and :elixir:mod:`Node` for other functions to handle
   processes, including spawning functions in nodes.
   
   Inlined by the compiler.
   
   **Examples**
   
   ::
   
       spawn(SomeModule, :function, [1, 2, 3])
   
   
   

.. elixir:function:: Kernel.spawn_link/1
   :sig: spawn_link(fun)


   Specs:
   
 
   * spawn_link((() -> any)) :: pid
 

   
   Spawns the given function, links it to the current process and returns
   its pid.
   
   Check the modules :elixir:mod:`Process` and :elixir:mod:`Node` for other functions to handle
   processes, including spawning functions in nodes.
   
   Inlined by the compiler.
   
   **Examples**
   
   ::
   
       current = Kernel.self
       child   = spawn_link(fn -> send current, {Kernel.self, 1 + 2} end)
   
       receive do
         {^child, 3} -> IO.puts "Received 3 back"
       end
   
   
   

.. elixir:function:: Kernel.spawn_link/3
   :sig: spawn_link(module, fun, args)


   Specs:
   
 
   * spawn_link(module, atom, []) :: pid
 

   
   Spawns the given module and function passing the given args, links it to
   the current process and returns its pid.
   
   Check the modules :elixir:mod:`Process` and :elixir:mod:`Node` for other functions to handle
   processes, including spawning functions in nodes.
   
   Inlined by the compiler.
   
   **Examples**
   
   ::
   
       spawn_link(SomeModule, :function, [1, 2, 3])
   
   
   

.. elixir:function:: Kernel.spawn_monitor/1
   :sig: spawn_monitor(fun)


   Specs:
   
 
   * spawn_monitor((() -> any)) :: {pid, reference}
 

   
   Spawns the given function, monitors it and returns its pid and
   monitoring reference.
   
   Check the modules :elixir:mod:`Process` and :elixir:mod:`Node` for other functions to handle
   processes, including spawning functions in nodes.
   
   Inlined by the compiler.
   
   **Examples**
   
   ::
   
       current = Kernel.self
       spawn_monitor(fn -> send current, {Kernel.self, 1 + 2} end)
   
   
   

.. elixir:function:: Kernel.spawn_monitor/3
   :sig: spawn_monitor(module, fun, args)


   Specs:
   
 
   * spawn_monitor(module, atom, []) :: {pid, reference}
 

   
   Spawns the given module and function passing the given args, monitors it
   and returns its pid and monitoring reference.
   
   Check the modules :elixir:mod:`Process` and :elixir:mod:`Node` for other functions to handle
   processes, including spawning functions in nodes.
   
   Inlined by the compiler.
   
   **Examples**
   
   ::
   
       spawn_monitor(SomeModule, :function, [1, 2, 3])
   
   
   

.. elixir:function:: Kernel.struct/2
   :sig: struct(struct, kv \\ [])


   Specs:
   
 
   * struct(module | %{}, :elixir:type:`Enum.t/0`) :: %{}
 

   
   Creates and updates structs.
   
   The struct argument may be an atom (which defines ``defstruct``) or a
   struct itself. The second argument is any Enumerable that emits two-item
   tuples (key-value) during enumeration.
   
   If one of the keys in the Enumerable does not exist in the struct, they
   are automatically discarded.
   
   This function is useful for dynamically creating and updating structs.
   
   **Example**
   
   ::
   
       defmodule User do
         defstruct name: "jose"
       end
   
       struct(User)
       #=> %User{name: "jose"}
   
       opts = [name: "eric"]
       user = struct(User, opts)
       #=> %User{name: "eric"}
   
       struct(user, unknown: "value")
       #=> %User{name: "eric"}
   
   
   

.. elixir:function:: Kernel.throw/1
   :sig: throw(term)


   Specs:
   
 
   * throw(term) :: no_return
 

   
   A non-local return from a function. Check :elixir:func:`Kernel.SpecialForms.try/1`
   for more information.
   
   Inlined by the compiler.
   
   

.. elixir:function:: Kernel.tl/1
   :sig: tl(list)


   Specs:
   
 
   * tl(maybe_improper_list) :: maybe_improper_list
 

   
   Returns the tail of a list. Raises :elixir:mod:`ArgumentError` if the list is
   empty.
   
   Allowed in guard tests. Inlined by the compiler.
   
   

.. elixir:function:: Kernel.trunc/1
   :sig: trunc(number)


   Specs:
   
 
   * trunc(number) :: integer
 

   
   Returns an integer by truncating the given number.
   
   Allowed in guard tests. Inlined by the compiler.
   
   **Examples**
   
   ::
   
       iex> trunc(5.5)
       5
   
   
   

.. elixir:function:: Kernel.tuple_size/1
   :sig: tuple_size(tuple)


   Specs:
   
 
   * tuple_size(tuple) :: non_neg_integer
 

   
   Returns the size of a tuple.
   
   This operation happens in constant time.
   
   Allowed in guard tests. Inlined by the compiler.
   
   

.. elixir:function:: Kernel.xor/2
   :sig: left xor right


   Specs:
   
 
   * boolean xor boolean :: boolean
 

   
   Boolean exclusive-or. Arguments must be booleans. Returns ``true`` if
   and only if both arguments are different.
   
   Allowed in guard tests. Inlined by the compiler.
   
   **Examples**
   
   ::
   
       iex> true xor false
       true
   
       iex> true xor true
       false
   
   
   





Macros
------

.. elixir:macro:: Kernel.!/1
   :sig: !arg


   
   Receives any argument and returns ``true`` if it is ``false`` or
   ``nil``. Returns ``false`` otherwise. Not allowed in guard clauses.
   
   **Examples**
   
   ::
   
       iex> !Enum.empty?([])
       false
   
       iex> !List.first([])
       true
   
   
   

.. elixir:macro:: Kernel.&&/2
   :sig: left && right


   
   Provides a short-circuit operator that evaluates and returns the second
   expression only if the first one evaluates to true (i.e. it is not nil
   nor false). Returns the first expression otherwise.
   
   **Examples**
   
   ::
   
       iex> Enum.empty?([]) && Enum.empty?([])
       true
   
       iex> List.first([]) && true
       nil
   
       iex> Enum.empty?([]) && List.first([1])
       1
   
       iex> false && throw(:bad)
       false
   
   Notice that, unlike Erlang's ``and`` operator, this operator accepts any
   expression as an argument, not only booleans, however it is not allowed
   in guards.
   
   

.. elixir:macro:: Kernel.../2
   :sig: first .. last


   
   Returns a range with the specified start and end. Includes both ends.
   
   **Examples**
   
   ::
   
       iex> 0 in 1..3
       false
   
       iex> 1 in 1..3
       true
   
       iex> 2 in 1..3
       true
   
       iex> 3 in 1..3
       true
   
   
   

.. elixir:macro:: Kernel.<>/2
   :sig: left <> right


   
   Concatenates two binaries.
   
   **Examples**
   
   ::
   
       iex> "foo" <> "bar"
       "foobar"
   
   The ``<>`` operator can also be used in guard clauses as long as the
   first part is a literal binary:
   
   ::
   
       iex> "foo" <> x = "foobar"
       iex> x
       "bar"
   
   
   

.. elixir:macro:: Kernel.@/1
   :sig: @expr


   
   Read and write attributes of th current module.
   
   The canonical example for attributes is annotating that a module
   implements the OTP behaviour called ``gen_server``:
   
   ::
   
       defmodule MyServer do
         @behaviour :gen_server
         # ... callbacks ...
       end
   
   By default Elixir supports all Erlang module attributes, but any
   developer can also add custom attributes:
   
   ::
   
       defmodule MyServer do
         @my_data 13
         IO.inspect @my_data #=> 13
       end
   
   Unlike Erlang, such attributes are not stored in the module by default
   since it is common in Elixir to use such attributes to store temporary
   data. A developer can configure an attribute to behave closer to Erlang
   by calling :elixir:func:`Module.register_attribute/3`.
   
   Finally, notice that attributes can also be read inside functions:
   
   ::
   
       defmodule MyServer do
         @my_data 11
         def first_data, do: @my_data
         @my_data 13
         def second_data, do: @my_data
       end
   
       MyServer.first_data #=> 11
       MyServer.second_data #=> 13
   
   It is important to note that reading an attribute takes a snapshot of
   its current value. In other words, the value is read at compilation time
   and not at runtime. Check the module :elixir:mod:`Module` for other functions to
   manipulate module attributes.
   
   

.. elixir:macro:: Kernel.alias!/1
   :sig: alias!(alias)


   
   When used inside quoting, marks that the alias should not be hygienezed.
   This means the alias will be expanded when the macro is expanded.
   
   Check :elixir:func:`Kernel.SpecialForms.quote/2` for more information.
   
   

.. elixir:macro:: Kernel.and/2
   :sig: left and right


   
   Boolean and. Requires only the first argument to be a boolean since it
   short-circuits.
   
   Allowed in guard tests.
   
   **Examples**
   
   ::
   
       iex> true and false
       false
   
   
   

.. elixir:macro:: Kernel.binding/0
   :sig: binding()


   
   Returns the binding as a keyword list where the variable name is the key
   and the variable value is the value.
   
   **Examples**
   
   ::
   
       iex> x = 1
       iex> binding()
       [x: 1]
       iex> x = 2
       iex> binding()
       [x: 2]
   
   
   

.. elixir:macro:: Kernel.binding/1
   :sig: binding(list)


   
   Receives a list of atoms at compilation time and returns the binding of
   the given variables as a keyword list where the variable name is the key
   and the variable value is the value.
   
   In case a variable in the list does not exist in the binding, it is not
   included in the returned result.
   
   **Examples**
   
   ::
   
       iex> x = 1
       iex> binding([:x, :y])
       [x: 1]
   
   
   

.. elixir:macro:: Kernel.binding/2
   :sig: binding(list, context)


   
   Receives a list of atoms at compilation time and returns the binding of
   the given variables in the given context as a keyword list where the
   variable name is the key and the variable value is the value.
   
   In case a variable in the list does not exist in the binding, it is not
   included in the returned result.
   
   **Examples**
   
   ::
   
       iex> var!(x, :foo) = 1
       iex> binding([:x, :y])
       []
       iex> binding([:x, :y], :foo)
       [x: 1]
   
   
   

.. elixir:macro:: Kernel.cond/1
   :sig: cond(list1)


   
   Evaluates the expression corresponding to the first clause that
   evaluates to true. Raises an error if all conditions evaluate to to nil
   or false.
   
   **Examples**
   
   ::
   
       cond do
         1 + 1 == 1 ->
           "This will never match"
         2 * 2 != 4 ->
           "Nor this"
         true ->
           "This will"
       end
   
   
   

.. elixir:macro:: Kernel.def/2
   :sig: def(call, expr \\ nil)


   
   Defines a function with the given name and contents.
   
   **Examples**
   
   ::
   
       defmodule Foo do
         def bar, do: :baz
       end
   
       Foo.bar #=> :baz
   
   A function that expects arguments can be defined as follow:
   
   ::
   
       defmodule Foo do
         def sum(a, b) do
           a + b
         end
       end
   
   In the example above, we defined a function ``sum`` that receives two
   arguments and sums them.
   
   

.. elixir:macro:: Kernel.defdelegate/2
   :sig: defdelegate(funs, opts)


   
   Defines the given functions in the current module that will delegate to
   the given ``target``. Functions defined with ``defdelegate`` are public
   and are allowed to be invoked from external. If you find yourself
   wishing to define a delegation as private, you should likely use import
   instead.
   
   Delegation only works with functions, delegating to macros is not
   supported.
   
   **Options**
   
   -  ``:to`` - The expression to delegate to. Any expression is allowed
      and its results will be calculated on runtime;
   
   -  ``:as`` - The function to call on the target given in ``:to``. This
      parameter is optional and defaults to the name being delegated.
   
   -  ``:append_first`` - If true, when delegated, first argument passed to
      the delegate will be relocated to the end of the arguments when
      dispatched to the target. The motivation behind this is because
      Elixir normalizes the "handle" as a first argument and some Erlang
      modules expect it as last argument.
   
   **Examples**
   
   ::
   
       defmodule MyList do
         defdelegate reverse(list), to: :lists
         defdelegate [reverse(list), map(callback, list)], to: :lists
         defdelegate other_reverse(list), to: :lists, as: :reverse
       end
   
       MyList.reverse([1, 2, 3])
       #=> [3,2,1]
   
       MyList.other_reverse([1, 2, 3])
       #=> [3,2,1]
   
   
   

.. elixir:macro:: Kernel.defexception/1
   :sig: defexception(fields)


   
   Defines an exception.
   
   Exceptions are structs backed by a module that implements the Exception
   behaviour. The Exception behaviour requires two functions to be
   implemented:
   
   -  ``exception/1`` - that receives the arguments given to :elixir:func:`raise/2`
      and returns the exception struct. The default implementation accepts
      a set of keyword arguments that is merged into the struct;
   
   -  ``message/1`` - receives the exception struct and must return its
      message. Most commonly exceptions have a message field which by
      default is accessed by this function. However, if your exception does
      not have a message field, this function must be explicitly
      implemented;
   
   Since exceptions are structs, all the API supported by :elixir:func:`defstruct/1`
   is also available in :elixir:func:`defexception/1`.
   
   **Raising exceptions**
   
   The most common way to raise an exception is via the :elixir:func:`raise/2`
   function:
   
   ::
   
       defmodule MyAppError do
         defexception [:message]
       end
   
       raise MyAppError,
         message: "did not get what was expected, got: #{inspect value}"
   
   In many cases it is more convenient to pass the expected value to
   ``raise`` and generate the message in the ``exception/1`` callback:
   
   ::
   
       defmodule MyAppError do
         defexception [:message]
   
         def exception(value) do
           msg = "did not get what was expected, got: #{inspect value}"
           %MyAppError{message: msg}
         end
       end
   
       raise MyAppError, value
   
   The example above is the preferred mechanism for customizing exception
   messages.
   
   

.. elixir:macro:: Kernel.defimpl/3
   :sig: defimpl(name, opts, do_block \\ [])


   
   Defines an implementation for the given protocol. See :elixir:func:`defprotocol/2`
   for examples.
   
   Inside an implementation, the name of the protocol can be accessed via
   ``@protocol`` and the current target as ``@for``.
   
   

.. elixir:macro:: Kernel.defmacro/2
   :sig: defmacro(call, expr \\ nil)


   
   Defines a macro with the given name and contents.
   
   **Examples**
   
   ::
   
       defmodule MyLogic do
         defmacro unless(expr, opts) do
           quote do
             if !unquote(expr), unquote(opts)
           end
         end
       end
   
       require MyLogic
       MyLogic.unless false do
         IO.puts "It works"
       end
   
   
   

.. elixir:macro:: Kernel.defmacrop/2
   :sig: defmacrop(call, expr \\ nil)


   
   Defines a macro that is private. Private macros are only accessible from
   the same module in which they are defined.
   
   Check :elixir:func:`defmacro/2` for more information
   
   

.. elixir:macro:: Kernel.defmodule/2
   :sig: defmodule(alias, list2)


   
   Defines a module given by name with the given contents.
   
   It returns the module name, the module binary and the block contents
   result.
   
   **Examples**
   
   ::
   
       iex> defmodule Foo do
       ...>   def bar, do: :baz
       ...> end
       iex> Foo.bar
       :baz
   
   **Nesting**
   
   Nesting a module inside another module affects its name:
   
   ::
   
       defmodule Foo do
         defmodule Bar do
         end
       end
   
   In the example above, two modules ``Foo`` and ``Foo.Bar`` are created.
   When nesting, Elixir automatically creates an alias, allowing the second
   module ``Foo.Bar`` to be accessed as ``Bar`` in the same lexical scope.
   
   This means that, if the module ``Bar`` is moved to another file, the
   references to ``Bar`` needs to be updated or an alias needs to be
   explicitly set with the help of :elixir:func:`Kernel.SpecialForms.alias/2`.
   
   **Dynamic names**
   
   Elixir module names can be dynamically generated. This is very useful
   for macros. For instance, one could write:
   
   ::
   
       defmodule String.to_atom("Foo#{1}") do
         # contents ...
       end
   
   Elixir will accept any module name as long as the expression returns an
   atom. Note that, when a dynamic name is used, Elixir won't nest the name
   under the current module nor automatically set up an alias.
   
   

.. elixir:macro:: Kernel.defoverridable/1
   :sig: defoverridable(tuples)


   
   Makes the given functions in the current module overridable. An
   overridable function is lazily defined, allowing a developer to
   customize it.
   
   **Example**
   
   ::
   
       defmodule DefaultMod do
         defmacro __using__(_opts) do
           quote do
             def test(x, y) do
               x + y
             end
   
             defoverridable [test: 2]
           end
         end
       end
   
       defmodule InheritMod do
         use DefaultMod
   
         def test(x, y) do
           x * y + super(x, y)
         end
       end
   
   As seen as in the example ``super`` can be used to call the default
   implementation.
   
   

.. elixir:macro:: Kernel.defp/2
   :sig: defp(call, expr \\ nil)


   
   Defines a function that is private. Private functions are only
   accessible from within the module in which they are defined.
   
   Check :elixir:func:`def/2` for more information
   
   **Examples**
   
   ::
   
       defmodule Foo do
         def bar do
           sum(1, 2)
         end
   
         defp sum(a, b), do: a + b
       end
   
   In the example above, ``sum`` is private and accessing it through
   ``Foo.sum`` will raise an error.
   
   

.. elixir:macro:: Kernel.defprotocol/2
   :sig: defprotocol(name, list2)


   
   Defines a protocol.
   
   A protocol specifies an API that should be defined by its
   implementations.
   
   **Examples**
   
   In Elixir, only ``false`` and ``nil`` are considered falsy values.
   Everything else evaluates to true in ``if`` clauses. Depending on the
   application, it may be important to specify a ``blank?`` protocol that
   returns a boolean for other data types that should be considered
   ``blank?``. For instance, an empty list or an empty binary could be
   considered blanks.
   
   We could implement this protocol as follow:
   
   ::
   
       defprotocol Blank do
         @doc "Returns true if data is considered blank/empty"
         def blank?(data)
       end
   
   Now that the protocol is defined, we can implement it. We need to
   implement the protocol for each Elixir type. For example:
   
   ::
   
       # Integers are never blank
       defimpl Blank, for: Integer do
         def blank?(number), do: false
       end
   
       # Just empty list is blank
       defimpl Blank, for: List do
         def blank?([]), do: true
         def blank?(_),  do: false
       end
   
       # Just the atoms false and nil are blank
       defimpl Blank, for: Atom do
         def blank?(false), do: true
         def blank?(nil),   do: true
         def blank?(_),     do: false
       end
   
   And we would have to define the implementation for all types. The
   supported types available are:
   
   -  Structs (see below)
   -  Tuple
   -  Atom
   -  List
   -  BitString
   -  Integer
   -  Float
   -  Function
   -  PID
   -  Map
   -  Port
   -  Reference
   -  Any (see below)
   
   **Protocols + Structs**
   
   The real benefit of protocols comes when mixed with structs. For
   instance, Elixir ships with many data types implemented as structs, like
   :elixir:mod:`HashDict` and :elixir:mod:`HashSet`. We can implement the ``Blank`` protocol
   for those types as well:
   
   ::
   
       defimpl Blank, for: [HashDict, HashSet] do
         def blank?(enum_like), do: Enum.empty?(enum_like)
       end
   
   If a protocol is not found for a given type, it will fallback to
   ``Any``.
   
   **Fallback to any**
   
   In some cases, it may be convenient to provide a default implementation
   for all types. This can be achieved by setting ``@fallback_to_any`` to
   ``true`` in the protocol definition:
   
   ::
   
       defprotocol Blank do
         @fallback_to_any true
         def blank?(data)
       end
   
   Which can now be implemented as:
   
   ::
   
       defimpl Blank, for: Any do
         def blank?(_), do: true
       end
   
   One may wonder why such fallback is not true by default.
   
   It is two-fold: first, the majority of protocols cannot implement an
   action in a generic way for all types. In fact, providing a default
   implementation may be harmful, because users may rely on the default
   implementation instead of providing a specialized one.
   
   Second, falling back to ``Any`` adds an extra lookup to all types, which
   is unnecessary overhead unless an implementation for Any is required.
   
   **Types**
   
   Defining a protocol automatically defines a type named ``t``, which can
   be used as:
   
   ::
   
       @spec present?(Blank.t) :: boolean
       def present?(blank) do
         not Blank.blank?(blank)
       end
   
   The ``@spec`` above expresses that all types allowed to implement the
   given protocol are valid argument types for the given function.
   
   **Reflection**
   
   Any protocol module contains three extra functions:
   
   -  ``__protocol__/1`` - returns the protocol name when :name is given,
      and a keyword list with the protocol functions when :functions is
      given;
   
   -  ``impl_for/1`` - receives a structure and returns the module that
      implements the protocol for the structure, nil otherwise;
   
   -  ``impl_for!/1`` - same as above but raises an error if an
      implementation is not found
   
   **Consolidation**
   
   In order to cope with code loading in development, protocols in Elixir
   provide a slow implementation of protocol dispatching specific to
   development.
   
   In order to speed up dispatching in production environments, where all
   implementations are known up-front, Elixir provides a feature called
   protocol consolidation. For this reason, all protocols are compiled with
   ``debug_info`` set to true, regardless of the option set by ``elixirc``
   compiler. The debug info though may be removed after consolidation.
   
   For more information on how to apply protocol consolidation to a given
   project, please check the functions in the :elixir:mod:`Protocol` module or the
   ``mix compile.protocols`` task.
   
   

.. elixir:macro:: Kernel.defstruct/1
   :sig: defstruct(kv)


   
   Defines a struct for the current module.
   
   A struct is a tagged map that allows developers to provide default
   values for keys, tags to be used in polymorphic dispatches and compile
   time assertions.
   
   To define a struct, a developer needs to only define a function named
   ``__struct__/0`` that returns a map with the structs field. This macro
   is a convenience for defining such function, with the addition of a type
   ``t`` and deriving conveniences.
   
   For more information about structs, please check
   ``Kernel.SpecialForms.%/2``.
   
   **Examples**
   
   ::
   
       defmodule User do
         defstruct name: nil, age: nil
       end
   
   Struct fields are evaluated at definition time, which allows them to be
   dynamic. In the example below, ``10 + 11`` will be evaluated at
   compilation time and the age field will be stored with value ``21``:
   
   ::
   
       defmodule User do
         defstruct name: nil, age: 10 + 11
       end
   
   **Deriving**
   
   Alhought structs are maps, by default structs do not implement any of
   the protocols implemented for maps. For example, if you attempt to use
   the access protocol with the User struct, it will lead to an error:
   
   ::
   
       %User{}[:age]
       ** (Protocol.UndefinedError) protocol Access not implemented for %User{...}
   
   However, ``defstruct/2`` allows implementation for protocols to derived
   by defining a ``@derive`` attribute as a list before ``defstruct/2`` is
   invoked:
   
   ::
   
       defmodule User do
         @derive [Access]
         defstruct name: nil, age: 10 + 11
       end
   
       %User{}[:age] #=> 21
   
   For each protocol given to ``@derive``, Elixir will assert there is an
   implementation of that protocol for maps and check if the map
   implementation defines a ``__deriving__/2`` callback. If so, the
   callback is invoked, otherwise an implementation that simply points to
   the map one is automatically derived.
   
   **Types**
   
   ``defstruct`` automatically generates a type ``t`` unless one exists.
   The following definition:
   
   ::
   
       defmodule User do
         defstruct name: "José" :: String.t,
                   age: 25 :: integer
       end
   
   Generates a type as follows:
   
   ::
   
       @type t :: %User{name: String.t, age: integer}
   
   In case a struct does not declare a field type, it defaults to ``term``.
   
   

.. elixir:macro:: Kernel.destructure/2
   :sig: destructure(left, right)


   
   Allows you to destructure two lists, assigning each term in the right to
   the matching term in the left. Unlike pattern matching via ``=``, if the
   sizes of the left and right lists don't match, destructuring simply
   stops instead of raising an error.
   
   **Examples**
   
   ::
   
       iex> destructure([x, y, z], [1, 2, 3, 4, 5])
       iex> {x, y, z}
       {1, 2, 3}
   
   Notice in the example above, even though the right size has more entries
   than the left, destructuring works fine. If the right size is smaller,
   the remaining items are simply assigned to nil:
   
   ::
   
       iex> destructure([x, y, z], [1])
       iex> {x, y, z}
       {1, nil, nil}
   
   The left side supports any expression you would use on the left side of
   a match:
   
   ::
   
       x = 1
       destructure([^x, y, z], [1, 2, 3])
   
   The example above will only work if x matches the first value from the
   right side. Otherwise, it will raise a CaseClauseError.
   
   

.. elixir:macro:: Kernel.if/2
   :sig: if(condition, clauses)


   
   Provides an ``if`` macro. This macro expects the first argument to be a
   condition and the rest are keyword arguments.
   
   **One-liner examples**
   
   ::
   
       if(foo, do: bar)
   
   In the example above, ``bar`` will be returned if ``foo`` evaluates to
   ``true`` (i.e. it is neither ``false`` nor ``nil``). Otherwise, ``nil``
   will be returned.
   
   An ``else`` option can be given to specify the opposite:
   
   ::
   
       if(foo, do: bar, else: baz)
   
   **Blocks examples**
   
   Elixir also allows you to pass a block to the ``if`` macro. The first
   example above would be translated to:
   
   ::
   
       if foo do
         bar
       end
   
   Notice that ``do/end`` becomes delimiters. The second example would then
   translate to:
   
   ::
   
       if foo do
         bar
       else
         baz
       end
   
   If you want to compare more than two clauses, you can use the :elixir:func:`cond/1`
   macro.
   
   

.. elixir:macro:: Kernel.in/2
   :sig: left in right


   
   Checks if the element on the left side is member of the collection on
   the right side.
   
   **Examples**
   
   ::
   
       iex> x = 1
       iex> x in [1, 2, 3]
       true
   
   This macro simply translates the expression above to:
   
   ::
   
       Enum.member?([1,2,3], x)
   
   **Guards**
   
   The ``in`` operator can be used on guard clauses as long as the right
   side is a range or a list. Elixir will then expand the operator to a
   valid guard expression. For example:
   
   ::
   
       when x in [1,2,3]
   
   Translates to:
   
   ::
   
       when x === 1 or x === 2 or x === 3
   
   When using ranges:
   
   ::
   
       when x in 1..3
   
   Translates to:
   
   ::
   
       when x >= 1 and x <= 3
   
   
   

.. elixir:macro:: Kernel.match?/2
   :sig: match?(pattern, expr)


   
   A convenient macro that checks if the right side matches the left side.
   The left side is allowed to be a match pattern.
   
   **Examples**
   
   ::
   
       iex> match?(1, 1)
       true
   
       iex> match?(1, 2)
       false
   
       iex> match?({1, _}, {1, 2})
       true
   
   Match can also be used to filter or find a value in an enumerable:
   
   ::
   
       list = [{:a, 1}, {:b, 2}, {:a, 3}]
       Enum.filter list, &match?({:a, _}, &1)
   
   Guard clauses can also be given to the match:
   
   ::
   
       list = [{:a, 1}, {:b, 2}, {:a, 3}]
       Enum.filter list, &match?({:a, x} when x < 2, &1)
   
   However, variables assigned in the match will not be available outside
   of the function call:
   
   ::
   
       iex> match?(x, 1)
       true
   
       iex> binding([:x]) == []
       true
   
   
   

.. elixir:macro:: Kernel.nil?/1
   :sig: nil?(x)


   
   Checks if the given argument is nil or not. Allowed in guard clauses.
   
   **Examples**
   
   ::
   
       iex> nil?(1)
       false
   
       iex> nil?(nil)
       true
   
   
   

.. elixir:macro:: Kernel.or/2
   :sig: left or right


   
   Boolean or. Requires only the first argument to be a boolean since it
   short-circuits.
   
   Allowed in guard tests.
   
   **Examples**
   
   ::
   
       iex> true or false
       true
   
   
   

.. elixir:macro:: Kernel.raise/1
   :sig: raise(msg)


   
   Raises an exception.
   
   If the argument is a binary, it raises :elixir:mod:`RuntimeError` using the given
   argument as message.
   
   If an atom, it will become a call to ``raise(atom, [])``.
   
   If anything else, it will just raise the given exception.
   
   **Examples**
   
   ::
   
       raise "Given values do not match"
   
       try do
         1 + :foo
       rescue
         x in [ArithmeticError] ->
           IO.puts "that was expected"
           raise x
       end
   
   
   

.. elixir:macro:: Kernel.raise/2
   :sig: raise(exception, attrs)


   
   Raises an exception.
   
   Calls ``.exception`` on the given argument passing the attributes in
   order to retrieve the appropriate exception structure.
   
   Any module defined via :elixir:func:`defexception/1` automatically implements
   ``exception(attrs)`` callback expected by :elixir:func:`raise/2`.
   
   **Examples**
   
   ::
   
       iex> raise(ArgumentError, message: "Sample")
       ** (ArgumentError) Sample
   
   
   

.. elixir:macro:: Kernel.reraise/2
   :sig: reraise(msg, stacktrace)


   
   Raises an exception preserving a previous stacktrace.
   
   Works like :elixir:func:`raise/1` but does not generate a new stacktrace.
   
   Notice that ``System.stacktrace`` returns the stacktrace of the last
   exception. That said, it is common to assign the stacktrace as the first
   expression inside a ``rescue`` clause as any other exception potentially
   raised (and rescued) in between the rescue clause and the raise call may
   change the ``System.stacktrace`` value.
   
   **Examples**
   
   ::
   
       try do
         raise "Oops"
       rescue
         exception ->
           stacktrace = System.stacktrace
           if Exception.message(exception) == "Oops" do
             reraise exception, stacktrace
           end
       end
   
   
   

.. elixir:macro:: Kernel.reraise/3
   :sig: reraise(exception, attrs, stacktrace)


   
   Raises an exception preserving a previous stacktrace.
   
   Works like :elixir:func:`raise/2` but does not generate a new stacktrace.
   
   See :elixir:func:`reraise/2` for more details.
   
   **Examples**
   
   ::
   
       try do
         raise "Oops"
       rescue
         exception ->
           stacktrace = System.stacktrace
           reraise WrapperError, [exception: exception], stacktrace
       end
   
   
   

.. elixir:macro:: Kernel.sigil_C/2
   :sig: sigil_C(arg1, list2)


   
   Handles the sigil ~C. It simply returns a char list without escaping
   characters and without interpolations.
   
   **Examples**
   
   ::
   
       iex> ~C(foo)
       'foo'
   
       iex> ~C(f#{o}o)
       'f\#{o}o'
   
   
   

.. elixir:macro:: Kernel.sigil_R/2
   :sig: sigil_R(arg1, options)


   
   Handles the sigil ~R. It returns a Regex pattern without escaping nor
   interpreting interpolations.
   
   **Examples**
   
   ::
   
       iex> Regex.match?(~R(f#{1,3}o), "f#o")
       true
   
   
   

.. elixir:macro:: Kernel.sigil_S/2
   :sig: sigil_S(string, list2)


   
   Handles the sigil ~S. It simply returns a string without escaping
   characters and without interpolations.
   
   **Examples**
   
   ::
   
       iex> ~S(foo)
       "foo"
   
       iex> ~S(f#{o}o)
       "f\#{o}o"
   
   
   

.. elixir:macro:: Kernel.sigil_W/2
   :sig: sigil_W(arg1, modifiers)


   
   Handles the sigil ~W. It returns a list of "words" split by whitespace
   without escaping nor interpreting interpolations.
   
   **Modifiers**
   
   -  ``s``: strings (default)
   -  ``a``: atoms
   -  ``c``: char lists
   
   **Examples**
   
   ::
   
       iex> ~W(foo #{bar} baz)
       ["foo", "\#{bar}", "baz"]
   
   
   

.. elixir:macro:: Kernel.sigil_c/2
   :sig: sigil_c(arg1, list2)


   
   Handles the sigil ~c. It returns a char list as if it were a single
   quoted string, unescaping characters and replacing interpolations.
   
   **Examples**
   
   ::
   
       iex> ~c(foo)
       'foo'
   
       iex> ~c(f#{:o}o)
       'foo'
   
   
   

.. elixir:macro:: Kernel.sigil_r/2
   :sig: sigil_r(arg1, options)


   
   Handles the sigil ~r. It returns a Regex pattern.
   
   **Examples**
   
   ::
   
       iex> Regex.match?(~r(foo), "foo")
       true
   
   
   

.. elixir:macro:: Kernel.sigil_s/2
   :sig: sigil_s(arg1, list2)


   
   Handles the sigil ~s. It returns a string as if it was double quoted
   string, unescaping characters and replacing interpolations.
   
   **Examples**
   
   ::
   
       iex> ~s(foo)
       "foo"
   
       iex> ~s(f#{:o}o)
       "foo"
   
   
   

.. elixir:macro:: Kernel.sigil_w/2
   :sig: sigil_w(arg1, modifiers)


   
   Handles the sigil ~w. It returns a list of "words" split by whitespace.
   
   **Modifiers**
   
   -  ``s``: strings (default)
   -  ``a``: atoms
   -  ``c``: char lists
   
   **Examples**
   
   ::
   
       iex> ~w(foo #{:bar} baz)
       ["foo", "bar", "baz"]
   
       iex> ~w(--source test/enum_test.exs)
       ["--source", "test/enum_test.exs"]
   
       iex> ~w(foo bar baz)a
       [:foo, :bar, :baz]
   
   
   

.. elixir:macro:: Kernel.to_char_list/1
   :sig: to_char_list(arg)


   
   Convert the argument to a list according to the List.Chars protocol.
   
   **Examples**
   
   ::
   
       iex> to_char_list(:foo)
       'foo'
   
   
   

.. elixir:macro:: Kernel.to_string/1
   :sig: to_string(arg)


   
   Converts the argument to a string according to the String.Chars
   protocol. This is the function invoked when there is string
   interpolation.
   
   **Examples**
   
   ::
   
       iex> to_string(:foo)
       "foo"
   
   
   

.. elixir:macro:: Kernel.unless/2
   :sig: unless(clause, options)


   
   Evaluates and returns the do-block passed in as a second argument unless
   clause evaluates to true. Returns nil otherwise. See also ``if``.
   
   **Examples**
   
   ::
   
       iex> unless(Enum.empty?([]), do: "Hello")
       nil
   
       iex> unless(Enum.empty?([1,2,3]), do: "Hello")
       "Hello"
   
   
   

.. elixir:macro:: Kernel.use/2
   :sig: use(module, opts \\ [])


   
   ``use`` is a simple mechanism for using a given module into the current
   context.
   
   **Examples**
   
   For example, in order to write tests using the ExUnit framework, a
   developer should use the ``ExUnit.Case`` module:
   
   ::
   
       defmodule AssertionTest do
         use ExUnit.Case, async: true
   
         test "always pass" do
           assert true
         end
       end
   
   By calling ``use``, a hook called ``__using__`` will be invoked in
   ``ExUnit.Case`` which will then do the proper setup.
   
   Simply put, ``use`` is simply a translation to:
   
   ::
   
       defmodule AssertionTest do
         require ExUnit.Case
         ExUnit.Case.__using__([async: true])
   
         test "always pass" do
           assert true
         end
       end
   
   
   

.. elixir:macro:: Kernel.var!/2
   :sig: var!(var, context \\ nil)


   
   When used inside quoting, marks that the variable should not be
   hygienized. The argument can be either a variable unquoted or an atom
   representing the variable name.
   
   Check :elixir:func:`Kernel.SpecialForms.quote/2` for more information.
   
   

.. elixir:macro:: Kernel.|>/2
   :sig: left \|> right


   
   ``|>`` is the pipe operator.
   
   This operator introduces the expression on the left as the first
   argument to the function call on the right.
   
   **Examples**
   
   ::
   
       iex> [1, [2], 3] |> List.flatten()
       [1, 2, 3]
   
   The example above is the same as calling ``List.flatten([1, [2], 3])``,
   i.e. the argument on the left side of ``|>`` is introduced as the first
   argument of the function call on the right side.
   
   This pattern is mostly useful when there is a desire to execute a bunch
   of operations, resembling a pipeline:
   
   ::
   
       iex> [1, [2], 3] |> List.flatten |> Enum.map(fn x -> x * 2 end)
       [2, 4, 6]
   
   The example above will pass the list to :elixir:func:`List.flatten/1`, then get the
   flattened list and pass to :elixir:func:`Enum.map/2`, which will multiply each
   entry in the list per two.
   
   In other words, the expression above simply translates to:
   
   ::
   
       Enum.map(List.flatten([1, [2], 3]), fn x -> x * 2 end)
   
   Beware of operator precedence when using the pipe operator. For example,
   the following expression:
   
   ::
   
       String.graphemes "Hello" |> Enum.reverse
   
   Translates to:
   
   ::
   
       String.graphemes("Hello" |> Enum.reverse)
   
   Which will result in an error as Enumerable protocol is not defined for
   binaries. Adding explicit parenthesis resolves the ambiguity:
   
   ::
   
       String.graphemes("Hello") |> Enum.reverse
   
   Or, even better:
   
   ::
   
       "Hello" |> String.graphemes |> Enum.reverse
   
   
   

.. elixir:macro:: Kernel.||/2
   :sig: left \|\| right


   
   Provides a short-circuit operator that evaluates and returns the second
   expression only if the first one does not evaluate to true (i.e. it is
   either nil or false). Returns the first expression otherwise.
   
   **Examples**
   
   ::
   
       iex> Enum.empty?([1]) || Enum.empty?([1])
       false
   
       iex> List.first([]) || true
       true
   
       iex> Enum.empty?([1]) || 1
       1
   
       iex> Enum.empty?([]) || throw(:bad)
       true
   
   Notice that, unlike Erlang's ``or`` operator, this operator accepts any
   expression as an argument, not only booleans, however it is not allowed
   in guards.
   
   





