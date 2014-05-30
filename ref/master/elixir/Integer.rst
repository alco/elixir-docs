Integer
==============================================================

.. elixir:module:: Integer

   :mtype: 

Overview
--------

Functions for working with integers.





Summary
-------

============================= =
:elixir:func:`even?/1`        Determines if an integer is even 

:elixir:func:`odd?/1`         Determines if an integer is odd 

:elixir:func:`parse/1`        Converts a binary to an integer 

:elixir:func:`to_char_list/1` Returns a char list which corresponds to the text representation of the given integer 

:elixir:func:`to_char_list/2` Returns a char list which corresponds to the text representation of the given integer in the given case 

:elixir:func:`to_string/1`    Returns a binary which corresponds to the text representation of ``some_integer`` 

:elixir:func:`to_string/2`    Returns a binary which corresponds to the text representation of ``some_integer`` in base ``base`` 
============================= =





Functions
---------

.. elixir:function:: Integer.parse/1
   :sig: parse(bin)


   Specs:
   
 
   * parse(binary) :: {integer, binary} | :error
 

   
   Converts a binary to an integer.
   
   If successful, returns a tuple of the form
   ``{integer, remainder_of_binary}``. Otherwise ``:error``.
   
   **Examples**
   
   ::
   
       iex> Integer.parse("34")
       {34,""}
   
       iex> Integer.parse("34.5")
       {34,".5"}
   
       iex> Integer.parse("three")
       :error
   
   
   

.. elixir:function:: Integer.to_char_list/1
   :sig: to_char_list(number)


   Specs:
   
 
   * to_char_list(integer) :: []
 

   
   Returns a char list which corresponds to the text representation of the
   given integer.
   
   Inlined by the compiler.
   
   **Examples**
   
   ::
   
       iex> Integer.to_char_list(7)
       '7'
   
   
   

.. elixir:function:: Integer.to_char_list/2
   :sig: to_char_list(number, base)


   Specs:
   
 
   * to_char_list(integer, pos_integer) :: []
 

   
   Returns a char list which corresponds to the text representation of the
   given integer in the given case.
   
   Inlined by the compiler.
   
   **Examples**
   
   ::
   
       iex> Integer.to_char_list(1023, 16)
       '3FF'
   
   
   

.. elixir:function:: Integer.to_string/1
   :sig: to_string(some_integer)


   Specs:
   
 
   * to_string(integer) :: :elixir:type:`String.t/0`
 

   
   Returns a binary which corresponds to the text representation of
   ``some_integer``.
   
   Inlined by the compiler.
   
   **Examples**
   
   ::
   
       iex> Integer.to_string(123)
       "123"
   
   
   

.. elixir:function:: Integer.to_string/2
   :sig: to_string(some_integer, base)


   Specs:
   
 
   * to_string(integer, pos_integer) :: :elixir:type:`String.t/0`
 

   
   Returns a binary which corresponds to the text representation of
   ``some_integer`` in base ``base``.
   
   Inlined by the compiler.
   
   **Examples**
   
   ::
   
       iex> Integer.to_string(100, 16)
       "64"
   
   
   





Macros
------

.. elixir:macro:: Integer.even?/1
   :sig: even?(n)


   
   Determines if an integer is even.
   
   Returns ``true`` if ``n`` is an even number, otherwise ``false``.
   Implemented as a macro so it is allowed in guard clauses.
   
   

.. elixir:macro:: Integer.odd?/1
   :sig: odd?(n)


   
   Determines if an integer is odd.
   
   Returns ``true`` if ``n`` is an odd number, otherwise ``false``.
   Implemented as a macro so it is allowed in guard clauses.
   
   





