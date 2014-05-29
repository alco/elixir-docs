Mix.Tasks.Compile.Protocols
==============================================================

.. elixir:module:: Mix.Tasks.Compile.Protocols

   :mtype: 

Overview
--------

Consolidates all protocols in all paths.

This module consolidates all protocols in the code path and output the
new binary files to the given directory (defaults to "consolidated").

A new directory will be created with the consolidated protocol versions.
Simply add it to your codepath to make use of it:

::

    mix run -pa _build/dev/consolidated

You can verify a protocol is consolidated by checking its attributes:

::

    elixir -pa _build/dev/consolidated -S       mix run -e "IO.puts Protocol.consolidated?(Enumerable)"






Summary
-------

==================== =
:elixir:func:`run/1` Callback implementation of :elixir:func:`Mix.Task.run/1` 
==================== =





Functions
---------

.. elixir:function:: Mix.Tasks.Compile.Protocols.run/1
   :sig: run(args)


   
   Callback implementation of :elixir:func:`Mix.Task.run/1`.
   
   







