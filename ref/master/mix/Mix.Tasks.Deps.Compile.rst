Mix.Tasks.Deps.Compile
==============================================================

.. elixir:module:: Mix.Tasks.Deps.Compile

   :mtype: 

Overview
--------

Compile dependencies.

By default, compile all dependencies. A list of dependencies can be
given to force the compilation of specific dependencies.

By default, attempt to detect if the project contains one of the
following files:

-  ``mix.exs`` - if so, invokes ``mix compile``
-  ``rebar.config`` - if so, invokes ``rebar compile``
-  ``Makefile`` - if so, invokes ``make``

The compilation can be customized by passing a ``compile`` option in the
dependency:

::

    {:some_dependency, "0.1.0", git: "...", compile: "command to compile"}

Command line options
~~~~~~~~~~~~~~~~~~~~

-  ``--quiet`` - do not output verbose messages






Summary
-------

==================== =
:elixir:func:`run/1` Callback implementation of :elixir:func:`Mix.Task.run/1` 
==================== =





Functions
---------

.. elixir:function:: Mix.Tasks.Deps.Compile.run/1
   :sig: run(args)


   
   Callback implementation of :elixir:func:`Mix.Task.run/1`.
   
   







