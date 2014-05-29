Mix.Tasks.Escriptize
==============================================================

.. elixir:module:: Mix.Tasks.Escriptize

   :mtype: 

Overview
--------

Generates an escript for the project.

Command line options
~~~~~~~~~~~~~~~~~~~~

-  ``--force`` - forces compilation regardless of modification times

-  ``--no-compile`` - skips compilation to .beam files

Configuration
~~~~~~~~~~~~~

The following option must be specified in your ``mix.exs``:

-  ``:escript_main_module`` - the module to be invoked once the escript
   starts. The module must contain a function named ``main/1`` that will
   receive the command line arguments as binaries;

The remaining options can be specified to further customize the escript:

-  ``:escript_name`` - the name of the generated escript. Defaults to
   app name;

-  ``:escript_path`` - the path to write the escript to. Defaults to app
   name;

-  ``:escript_app`` - the app to start with the escript. Defaults to app
   name. Set it to ``nil`` if no application should be started.

-  ``:escript_embed_elixir`` - if ``true`` embed elixir in the escript
   file. Defaults to ``true``.

-  ``:escript_embed_extra_apps`` - embed additional Elixir applications.
   if ``:escript_embed_elixir`` is ``true``. Defaults to ``[]``.

-  ``:escript_shebang`` - shebang interpreter directive used to execute
   the escript. Defaults to "#! /usr/bin/env escript".

-  ``:escript_comment`` - comment line to follow shebang directive in
   the escript. Defaults to "%%"

-  ``:escript_emu_args`` - emulator arguments to embed in the escript
   file. Defaults to "%%!".







Summary
-------

==================== =
:elixir:func:`run/1` Callback implementation of ```Mix.Task.run/1`` <Mix.Task.html#run/1>`__ 
==================== =





Functions
---------

.. elixir:function:: Mix.Tasks.Escriptize.run/1
   :sig: run(args)


   
   Callback implementation of ```Mix.Task.run/1`` <Mix.Task.html#run/1>`__.
   
   







