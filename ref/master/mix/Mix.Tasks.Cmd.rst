Mix.Tasks.Cmd
==============================================================

.. elixir:module:: Mix.Tasks.Cmd

   :mtype: 

Overview
--------

Executes the given command.

Useful in umbrella applications to execute a command on each child app:

::

    mix cmd echo pwd

Aborts when the first command exits with status different than zero.





Summary
-------

==================== =
:elixir:func:`run/1` Callback implementation of :elixir:func:`Mix.Task.run/1` 
==================== =





Functions
---------

.. elixir:function:: Mix.Tasks.Cmd.run/1
   :sig: run(args)


   
   Callback implementation of :elixir:func:`Mix.Task.run/1`.
   
   







