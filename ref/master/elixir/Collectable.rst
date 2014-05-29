Collectable
==============================================================

.. elixir:module:: Collectable

   :mtype: protocol

Overview
--------

A protocol to traverse data structures.

The :elixir:func:`Enum.into/2` function uses this protocol to insert an enumerable
into a collection:

::

    iex> Enum.into([a: 1, b: 2], %{})
    %{a: 1, b: 2}

If a collection implements both :elixir:mod:`Enumerable` and :elixir:mod:`Collectable`, both
operations can be combined with :elixir:func:`Enum.traverse/2`:

::

    iex> Enum.traverse(%{a: 1, b: 2}, fn {k, v} -> {k, v * 2} end)
    %{a: 2, b: 4}

Why Collectable?
~~~~~~~~~~~~~~~~

The :elixir:mod:`Enumerable` protocol is useful to take values out of a
collection. In order to support a wide range of values, the functions
provided by the :elixir:mod:`Enumerable` protocol do not keep shape. For example,
passing a dictionary to :elixir:func:`Enum.map/2` always returns a list.

This design is intentional. :elixir:mod:`Enumerable` was designed to support
infinite collections, resources and other structures with fixed shape.
For example, it doesn't make sense to insert values into a range, as it
has a fixed shape where just the range limits are stored.

The :elixir:mod:`Collectable` module was designed to fill the gap left by the
:elixir:mod:`Enumerable` protocol. It provides two functions: :elixir:func:`into/1` and
:elixir:func:`empty/1`.

:elixir:func:`into/1` can be seen as the opposite of :elixir:func:`Enumerable.reduce/3`. If
:elixir:mod:`Enumerable` is about taking values out, :elixir:func:`Collectable.into/1` is
about collecting those values into a structure.

:elixir:func:`empty/1` receives a collectable and returns an empty version of the
same collectable. By combining the enumerable functionality with
:elixir:func:`into/1` and :elixir:func:`empty/1`, one can, for example, implement a traversal
mechanism.





Summary
-------

====================== =
:elixir:func:`empty/1` Receives a collectable structure and returns an empty one 

:elixir:func:`into/1`  Returns a function that collects values alongside the initial accumulation value 
====================== =



Types
-----

.. elixir:type:: Collectable.command/0

   :elixir:type:`command/0` :: {:cont, term} | :done | :halt
   

.. elixir:type:: Collectable.t/0

   :elixir:type:`t/0` :: term
   





Functions
---------

.. elixir:function:: Collectable.empty/1
   :sig: empty(collectable)


   Specs:
   
 
   * empty(:elixir:type:`t/0`) :: :elixir:type:`t/0`
 

   
   Receives a collectable structure and returns an empty one.
   
   

.. elixir:function:: Collectable.into/1
   :sig: into(collectable)


   Specs:
   
 
   * into(:elixir:type:`t/0`) :: {term, (term, :elixir:type:`command/0` -> :elixir:type:`t/0` | term)}
 

   
   Returns a function that collects values alongside the initial
   accumulation value.
   
   The returned function receives a collectable and injects a given value
   into it for every ``{:cont, term}`` instruction.
   
   ``:done`` is passed when no further values will be injected, useful for
   closing resources and normalizing values. A collectable must be returned
   on ``:done``.
   
   If injection is suddenly interrupted, ``:halt`` is passed and it can
   return any value, as it won't be used.
   
   







