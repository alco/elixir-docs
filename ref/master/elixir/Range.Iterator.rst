Range.Iterator
==============================================================

.. elixir:module:: Range.Iterator

   :mtype: protocol

Overview
--------

A protocol used for iterating range elements.





Summary
-------

====================== =
:elixir:func:`count/2` Count how many items are in the range 

:elixir:func:`next/2`  Returns the function that calculates the next item 
====================== =



Types
-----

.. elixir:type:: Range.Iterator.t/0

   :elixir:type:`t/0` :: term
   





Functions
---------

.. elixir:function:: Range.Iterator.count/2
   :sig: count(first, range)


   
   Count how many items are in the range.
   
   

.. elixir:function:: Range.Iterator.next/2
   :sig: next(first, range)


   
   Returns the function that calculates the next item.
   
   







