Mix.Tasks.Archive
==============================================================

.. elixir:module:: Mix.Tasks.Archive

   :mtype: 

Overview
--------

Packages the current project (though not its dependencies) into a zip
file according to the specification of the `Erlang Archive
Format <http://www.erlang.org/doc/man/code.html>`__.

Archives are meant to bundle small projects, usually installed locally.

The file will be created in the current directory (which is expected to
be the project root), unless an argument -o is provided with the file
name.

Command line options
~~~~~~~~~~~~~~~~~~~~

-  ``-o`` - specify output file name. If there is a mix.exs, defaults to
   app-vsn.ez

-  ``-i`` - specify the input directory to archive. If there is a
   mix.exs, defaults to the current application build

-  ``--no-compile`` - skip compilation. Only applies to projects.







Summary
-------

==================== =
:elixir:func:`run/1` Callback implementation of :elixir:func:`Mix.Task.run/1` 
==================== =





Functions
---------

.. elixir:function:: Mix.Tasks.Archive.run/1
   :sig: run(args)


   
   Callback implementation of :elixir:func:`Mix.Task.run/1`.
   
   







