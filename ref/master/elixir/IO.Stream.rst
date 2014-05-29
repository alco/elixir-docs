IO.Stream
==============================================================

.. elixir:module:: IO.Stream

   :mtype: 

Overview
--------

Defines a :elixir:mod:`IO.Stream` struct returned by :elixir:func:`IO.stream/2` and
:elixir:func:`IO.binstream/2`.

The following fields are public:

-  ``device`` - the IO device
-  ``raw`` - a boolean indicating if bin functions should be used
-  ``line_or_bytes`` - if reading should read lines or a given amount of
   bytes








Types
-----

.. elixir:type:: IO.Stream.t/0

   :elixir:type:`t/0` :: %IO.Stream{device: term, raw: term, line_or_bytes: term}
   









