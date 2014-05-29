Mix.Tasks.Run
==============================================================

.. elixir:module:: Mix.Tasks.Run

   :mtype: 

Overview
--------

Runs the given file or expression in the context of the application.

Before running the code, it invokes the ``app.start`` task which
compiles and loads your project.

It is the goal of this task to provide a subset of the functionality
existent in the ``elixir`` executable, including setting up the
``System.argv``:

::

    mix run -e Hello.world
    mix run my_script.exs arg1 arg2 arg3

Many command line options need to be passed to the ``elixir`` executable
directly, which can be done as follows:

::

    elixir --sname hello -S mix run -e "My.code"

Command line options
~~~~~~~~~~~~~~~~~~~~

-  ``--eval``, ``-e`` - evaluate the given code
-  ``--require``, ``-r`` - require pattern before running the command
-  ``--parallel-require``, ``-pr`` - requires pattern in parallel
-  ``--no-compile`` - do not compile even if files require compilation
-  ``--no-deps-check`` - do not check dependencies
-  ``--no-halt`` - do not halt the system after running the command
-  ``--no-start`` - do not start applications after compilation






Summary
-------

==================== =
:elixir:func:`run/1` Callback implementation of :elixir:func:`Mix.Task.run/1` 
==================== =





Functions
---------

.. elixir:function:: Mix.Tasks.Run.run/1
   :sig: run(args)


   
   Callback implementation of :elixir:func:`Mix.Task.run/1`.
   
   







