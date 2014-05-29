Float
==============================================================

.. elixir:module:: Float

   :mtype: 

Overview
--------

Functions for working with floating point numbers.





Summary
-------

============================= =
:elixir:func:`ceil/1`         Rounds a float to the largest integer greater than or equal to ``num`` 

:elixir:func:`floor/1`        Rounds a float to the largest integer less than or equal to ``num`` 

:elixir:func:`parse/1`        Parses a binary into a float 

:elixir:func:`round/2`        Rounds a floating point value to an arbitrary number of fractional digits (between 0 and 15) 

:elixir:func:`to_char_list/1` Returns a char list which corresponds to the text representation of the given float 

:elixir:func:`to_char_list/2` Returns a list which corresponds to the text representation of ``float`` 

:elixir:func:`to_string/1`    Returns a binary which corresponds to the text representation of ``some_float`` 

:elixir:func:`to_string/2`    Returns a binary which corresponds to the text representation of ``float`` 
============================= =





Functions
---------

.. elixir:function:: Float.ceil/1
   :sig: ceil(num)


   Specs:
   
 
   * ceil(float | integer) :: integer
 

   
   Rounds a float to the largest integer greater than or equal to ``num``.
   
   **Examples**
   
   ::
   
       iex> Float.ceil(34)
       34
   
       iex> Float.ceil(34.25)
       35
   
       iex> Float.ceil(-56.5)
       -56
   
   
   

.. elixir:function:: Float.floor/1
   :sig: floor(num)


   Specs:
   
 
   * floor(float | integer) :: integer
 

   
   Rounds a float to the largest integer less than or equal to ``num``.
   
   **Examples**
   
   ::
   
       iex> Float.floor(34)
       34
   
       iex> Float.floor(34.25)
       34
   
       iex> Float.floor(-56.5)
       -57
   
   
   

.. elixir:function:: Float.parse/1
   :sig: parse(binary)


   Specs:
   
 
   * parse(binary) :: {float, binary} | :error
 

   
   Parses a binary into a float.
   
   If successful, returns a tuple of the form
   ``{float, remainder_of_binary}``. Otherwise ``:error``.
   
   **Examples**
   
   ::
   
       iex> Float.parse("34")
       {34.0,""}
   
       iex> Float.parse("34.25")
       {34.25,""}
   
       iex> Float.parse("56.5xyz")
       {56.5,"xyz"}
   
       iex> Float.parse("pi")
       :error
   
   
   

.. elixir:function:: Float.round/2
   :sig: round(number, precision)


   Specs:
   
 
   * round(float, integer) :: float
 

   
   Rounds a floating point value to an arbitrary number of fractional
   digits (between 0 and 15).
   
   **Examples**
   
   ::
   
       iex> Float.round(5.5674, 3)
       5.567
   
       iex> Float.round(5.5675, 3)
       5.568
   
       iex> Float.round(-5.5674, 3)
       -5.567
   
       iex> Float.round(-5.5675, 3)
       -5.568
   
   
   

.. elixir:function:: Float.to_char_list/1
   :sig: to_char_list(number)


   Specs:
   
 
   * to_char_list(float) :: char_list
 

   
   Returns a char list which corresponds to the text representation of the
   given float.
   
   Inlined by the compiler.
   
   **Examples**
   
   ::
   
       iex> Float.to_char_list(7.0)
       '7.00000000000000000000e+00'
   
   
   

.. elixir:function:: Float.to_char_list/2
   :sig: to_char_list(float, options)


   Specs:
   
 
   * to_char_list(float, []) :: char_list
 

   
   Returns a list which corresponds to the text representation of
   ``float``.
   
   **Options**
   
   -  ``:decimals`` — number of decimal points to show
   -  ``:scientific`` — number of decimal points to show, in scientific
      format
   -  ``:compact`` — when true, use the most compact representation
      (ignored with the ``scientific`` option)
   
   **Examples**
   
   ::
   
       iex> Float.to_char_list 7.1, [decimals: 2, compact: true]
       '7.1'
   
   
   

.. elixir:function:: Float.to_string/1
   :sig: to_string(some_float)


   Specs:
   
 
   * to_string(float) :: :elixir:type:`String.t/0`
 

   
   Returns a binary which corresponds to the text representation of
   ``some_float``.
   
   Inlined by the compiler.
   
   **Examples**
   
   ::
   
       iex> Float.to_string(7.0)
       "7.00000000000000000000e+00"
   
   
   

.. elixir:function:: Float.to_string/2
   :sig: to_string(float, options)


   Specs:
   
 
   * to_string(float, []) :: :elixir:type:`String.t/0`
 

   
   Returns a binary which corresponds to the text representation of
   ``float``.
   
   **Options**
   
   -  ``:decimals`` — number of decimal points to show
   -  ``:scientific`` — number of decimal points to show, in scientific
      format
   -  ``:compact`` — when true, use the most compact representation
      (ignored with the ``scientific`` option)
   
   **Examples**
   
   ::
   
       iex> Float.to_string 7.1, [decimals: 2, compact: true]
       "7.1"
   
   
   







