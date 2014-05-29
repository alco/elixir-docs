Tuple
==============================================================

.. elixir:module:: Tuple

   :mtype: 

Overview
--------

Functions for working with tuples.





Summary
-------

========================== =
:elixir:func:`delete_at/2` Removes an element from a tuple 

:elixir:func:`duplicate/2` Creates a new tuple 

:elixir:func:`insert_at/3` Inserts an element into a tuple 

:elixir:func:`to_list/1`   Converts a tuple to a list 
========================== =





Functions
---------

.. elixir:function:: Tuple.delete_at/2
   :sig: delete_at(tuple, index)


   Specs:
   
 
   * delete_at(tuple, non_neg_integer) :: tuple
 

   
   Removes an element from a tuple.
   
   Deletes the element at the zero-based ``index`` from ``tuple``. Raises
   an :elixir:mod:`ArgumentError` if ``index`` is greater than or equal to the length
   of ``tuple``.
   
   Inlined by the compiler.
   
   **Examples**
   
   ::
   
       iex> tuple = {:foo, :bar, :baz}
       iex> Tuple.delete_at(tuple, 0)
       {:bar, :baz}
   
   
   

.. elixir:function:: Tuple.duplicate/2
   :sig: duplicate(data, size)


   Specs:
   
 
   * duplicate(term, non_neg_integer) :: tuple
 

   
   Creates a new tuple.
   
   Creates a tuple of size ``size`` containing the given ``data`` at every
   position.
   
   Inlined by the compiler.
   
   **Examples**
   
   ::
   
       iex> Tuple.duplicate(:hello, 3)
       {:hello, :hello, :hello}
   
   
   

.. elixir:function:: Tuple.insert_at/3
   :sig: insert_at(tuple, index, term)


   Specs:
   
 
   * insert_at(tuple, non_neg_integer, term) :: tuple
 

   
   Inserts an element into a tuple.
   
   Inserts ``value`` into ``tuple`` at the given zero-based ``index``.
   Raises an :elixir:mod:`ArgumentError` if ``index`` is greater than the length of
   ``tuple``.
   
   Inlined by the compiler.
   
   **Examples**
   
   ::
   
       iex> tuple = {:bar, :baz}
       iex> Tuple.insert_at(tuple, 0, :foo)
       {:foo, :bar, :baz}
   
   
   

.. elixir:function:: Tuple.to_list/1
   :sig: to_list(tuple)


   Specs:
   
 
   * to_list(tuple) :: []
 

   
   Converts a tuple to a list.
   
   Inlined by the compiler.
   
   







