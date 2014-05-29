Range
==============================================================

.. elixir:module:: Range

   :mtype: 

Overview
--------

Defines a Range.

A Range are represented internally as a struct. However, the most common
form of creating and matching on ranges is via the ``../2`` macro,
auto-imported from Kernel:

::

    iex> range = 1..3
    1..3
    iex> first .. last = range
    iex> first
    1
    iex> last
    3






Summary
-------

======================= =
:elixir:func:`new/2`    Creates a new range 

:elixir:func:`range?/1` Returns true if the given argument is a range 
======================= =



Types
-----

.. elixir:type:: Range.t/0

   :elixir:type:`t/0` :: %Range{first: term, last: term}
   

.. elixir:type:: Range.t/2

   :elixir:type:`t/2` :: %Range{first: first, last: last}
   





Functions
---------

.. elixir:function:: Range.new/2
   :sig: new(first, last)


   
   Creates a new range.
   
   

.. elixir:function:: Range.range?/1
   :sig: range?(range)


   
   Returns true if the given argument is a range.
   
   **Examples**
   
   ::
   
       iex> Range.range?(1..3)
       true
   
       iex> Range.range?(0)
       false
   
   
   







