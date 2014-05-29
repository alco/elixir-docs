String.Chars
==============================================================

.. elixir:module:: String.Chars

   :mtype: protocol

Overview
--------

The String.Chars protocol is responsible for converting a structure to a
Binary (only if applicable). The only function required to be
implemented is ``to_string`` which does the conversion.

The ``to_string`` function automatically imported by Kernel invokes this
protocol. String interpolation also invokes to\_string in its arguments.
For example, ``"foo#{bar}"`` is the same as ``"foo" <> to_string(bar)``.





Summary
-------

========================== =
:elixir:func:`to_string/1` 
========================== =



Types
-----

.. elixir:type:: String.Chars.t/0

   :elixir:type:`t/0` :: term
   





Functions
---------

.. elixir:function:: String.Chars.to_string/1
   :sig: to_string(thing)


   
   
   







