Mix.Tasks.New
==============================================================

.. elixir:module:: Mix.Tasks.New

   :mtype: 

Overview
--------

Creates a new Elixir project. It expects the path of the project as
argument.

::

    mix new PATH [--bare] [--module MODULE] [--umbrella]

A project at the given PATH will be created. The application name and
module name will be retrieved from the path, unless ``--module`` is
given.

A ``--sup`` option can be given to generate an OTP application skeleton
including a supervision tree. Normally an app is generated without a
supervisor and without the app callback.

An ``--umbrella`` option can be given to generate an umbrella project.

Examples
~~~~~~~~

::

    mix new hello_world

Is equivalent to:

::

    mix new hello_world --module HelloWorld

To generate an app with supervisor and application callback:

::

    mix new hello_world --sup






Summary
-------

==================== =
:elixir:func:`run/1` Callback implementation of ```Mix.Task.run/1`` <Mix.Task.html#run/1>`__ 
==================== =





Functions
---------

.. elixir:function:: Mix.Tasks.New.run/1
   :sig: run(argv)


   
   Callback implementation of ```Mix.Task.run/1`` <Mix.Task.html#run/1>`__.
   
   







