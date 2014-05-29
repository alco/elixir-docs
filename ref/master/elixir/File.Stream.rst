File.Stream
==============================================================

.. elixir:module:: File.Stream

   :mtype: 

Overview
--------

Defines a :elixir:mod:`File.Stream` struct returned by ``File.stream!/2``.

The following fields are public:

-  ``path`` - the file path
-  ``modes`` - the file modes
-  ``raw`` - a boolean indicating if bin functions should be used
-  ``line_or_bytes`` - if reading should read lines or a given amount of
   bytes








Types
-----

.. elixir:type:: File.Stream.t/0

   :elixir:type:`t/0` :: %File.Stream{path: term, modes: term, line_or_bytes: term, raw: term}
   









