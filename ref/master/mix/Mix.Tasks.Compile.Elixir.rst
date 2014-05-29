Mix.Tasks.Compile.Elixir
==============================================================

.. elixir:module:: Mix.Tasks.Compile.Elixir

   :mtype: 

Overview
--------

Compiles Elixir source files.

Elixir is smart enough to recompile only files that changed and their
dependencies. This means if ``lib/a.ex`` is invoking a function defined
over ``lib/b.ex``, whenever ``lib/b.ex`` changes, ``lib/a.ex`` is also
recompiled.

Note it is important to recompile a file dependencies because often
there are compilation time dependencies in between them.

Command line options
~~~~~~~~~~~~~~~~~~~~

-  ``--force`` - forces compilation regardless of modification times;
-  ``--no-docs`` - Do not attach documentation to compiled modules;
-  ``--no-debug-info`` - Do not attach debug info to compiled modules;
-  ``--ignore-module-conflict``
-  ``--warnings-as-errors`` - Treat warnings as errors and return a
   non-zero exit code

Configuration
~~~~~~~~~~~~~

-  ``:elixirc_paths`` - directories to find source files. Defaults to
   ``["lib"]``, can be configured as:

-  ``:elixirc_options`` - compilation options that apply to Elixir's
   compiler, they are: ``:ignore_module_conflict``, ``:docs`` and
   ``:debug_info``. By default, uses the same behaviour as Elixir;







Summary
-------

============================== =
:elixir:func:`files_to_path/5` Compiles stale Elixir files 

:elixir:func:`manifests/0`     Returns Elixir manifests 

:elixir:func:`run/1`           Runs this task 
============================== =





Functions
---------

.. elixir:function:: Mix.Tasks.Compile.Elixir.files_to_path/5
   :sig: files_to_path(manifest, force, all, path, on_start)


   
   Compiles stale Elixir files.
   
   It expects a manifest file, a flag if compilation should be forced or
   not, all source files available (including the ones that are not stale)
   and a path where compiled files will be written to. All paths are
   required to be relative to the current working directory.
   
   The manifest is written down with information including dependencies in
   between modules, which helps it recompile only the modules that have
   changed at runtime.
   
   

.. elixir:function:: Mix.Tasks.Compile.Elixir.manifests/0
   :sig: manifests()


   
   Returns Elixir manifests.
   
   

.. elixir:function:: Mix.Tasks.Compile.Elixir.run/1
   :sig: run(args)


   
   Runs this task.
   
   







