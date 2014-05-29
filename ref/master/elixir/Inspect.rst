Inspect
==============================================================

.. elixir:module:: Inspect

   :mtype: protocol

Overview
--------

The :elixir:mod:`Inspect` protocol is responsible for converting any Elixir data
structure into an algebra document. This document is then formatted,
either in pretty printing format or a regular one.

The :elixir:func:`inspect/2` function receives the entity to be inspected followed
by the inspecting options, represented by the struct :elixir:mod:`Inspect.Opts`.

Inspection is done using the functions available in :elixir:mod:`Inspect.Algebra`.

Examples
~~~~~~~~

Many times, inspecting a structure can be implemented in function of
existing entities. For example, here is :elixir:mod:`HashSet`'s ``inspect``
implementation:

::

    defimpl Inspect, for: HashSet do
      import Inspect.Algebra

      def inspect(dict, opts) do
        concat ["#HashSet<", to_doc(HashSet.to_list(dict), opts), ">"]
      end
    end

The ``concat`` function comes from :elixir:mod:`Inspect.Algebra` and it
concatenates algebra documents together. In the example above, it is
concatenating the string ``"HashSet<"`` (all strings are valid algebra
documents that keep their formatting when pretty printed), the document
returned by :elixir:func:`Inspect.Algebra.to_doc/2` and the other string ``">"``.

Since regular strings are valid entities in an algebra document, an
implementation of inspect may simply return a string, although that will
devoid it of any pretty-printing.

Error handling
~~~~~~~~~~~~~~

In case there is an error while your structure is being inspected,
Elixir will automatically fall back to a raw representation.

You can however access the underlying error by invoking the Inspect
implementation directly. For example, to test Inspect.HashSet above, you
can invoke it as:

::

    Inspect.HashSet.inspect(HashSet.new, Inspect.Opts.new)






Summary
-------

======================== =
:elixir:func:`inspect/2` 
======================== =



Types
-----

.. elixir:type:: Inspect.t/0

   :elixir:type:`t/0` :: term
   





Functions
---------

.. elixir:function:: Inspect.inspect/2
   :sig: inspect(thing, opts)


   
   
   







