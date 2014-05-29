Mix.Tasks.Compile
==============================================================

.. elixir:module:: Mix.Tasks.Compile

   :mtype: 

Overview
--------

A meta task that compiles source files.

It simply runs the compilers registered in your project. At the end of
compilation it ensures load paths are set.

Configuration
~~~~~~~~~~~~~

-  ``:compilers`` - compilers to run, defaults to:

   [:leex, :yeec, :erlang, :elixir, :app]

Command line options
~~~~~~~~~~~~~~~~~~~~

-  ``--list`` - List all enabled compilers

-  ``--no-deps-check`` - Skips checking of dependencies

-  ``--force`` - Forces compilation







Summary
-------

========================== =
:elixir:func:`manifests/0` Returns manifests for all compilers 

:elixir:func:`run/1`       Callback implementation of :elixir:func:`Mix.Task.run/1` 
========================== =





Functions
---------

.. elixir:function:: Mix.Tasks.Compile.manifests/0
   :sig: manifests()


   
   Returns manifests for all compilers.
   
   

.. elixir:function:: Mix.Tasks.Compile.run/1
   :sig: run(args)


   
   Callback implementation of :elixir:func:`Mix.Task.run/1`.
   
   







