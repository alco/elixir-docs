Mix.Tasks.Local.Install
==============================================================

.. elixir:module:: Mix.Tasks.Local.Install

   :mtype: 

Overview
--------

Install an archive locally.

If no argument is supplied but there is an archive in the root (created
with mix archive), then the archive will be installed locally. For
example:

::

    mix do archive, local.install

The argument can be an archive located at some URL:

::

    mix local.install http://example.com/foo.ez

After installed, the tasks in the archive are available locally:

::

    mix some_task

Command line options
~~~~~~~~~~~~~~~~~~~~

-  ``--force`` - forces installation without a shell prompt. Primarily
   intended for automation in build systems like make.






Summary
-------

==================== =
:elixir:func:`run/1` Callback implementation of :elixir:func:`Mix.Task.run/1` 
==================== =





Functions
---------

.. elixir:function:: Mix.Tasks.Local.Install.run/1
   :sig: run(argv)


   
   Callback implementation of :elixir:func:`Mix.Task.run/1`.
   
   







