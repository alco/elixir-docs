Access
==============================================================

.. elixir:module:: Access

   :mtype: protocol

Overview
--------

The Access protocol is the underlying protocol invoked when the brackets
syntax is used. For instance, ``foo[bar]`` is translated to
``access foo, bar`` which, by default, invokes the ``Access.access``
protocol.

This protocol is implemented by default for Lists, Maps and dictionary
like types:

::

    iex> keywords = [a: 1, b: 2]
    iex> keywords[:a]
    1

    iex> map = %{a: 1, b: 2}
    iex> map[:a]
    1

    iex> star_ratings = %{1.0 => "★", 1.5 => "★☆", 2.0 => "★★"}
    iex> star_ratings[1.5]
    "★☆"

The key access must be implemented using the ``===`` operator. This
protocol is limited and is implemented only for the following built-in
types: keywords, maps and functions.





Summary
-------

==================== =
:elixir:func:`get/2` Receives the element being accessed and the access item 
==================== =



Types
-----

.. elixir:type:: Access.t/0

   :elixir:type:`t/0` :: term
   





Functions
---------

.. elixir:function:: Access.get/2
   :sig: get(container, key)


   
   Receives the element being accessed and the access item.
   
   







