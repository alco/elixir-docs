Mix.Tasks.Compile.Yecc
==============================================================

.. elixir:module:: Mix.Tasks.Compile.Yecc

   :mtype: 

Overview
--------

Compile Yecc source files.

When this task runs, it will check the modification time of every file,
and if it has changed, the file will be compiled. Files will be compiled
in the same source directory with a .erl extension. You can force
compilation regardless of modification times by passing the ``--force``
option.

Command line options
~~~~~~~~~~~~~~~~~~~~

-  ``--force`` - forces compilation regardless of modification times;

Configuration
~~~~~~~~~~~~~

-  ``:erlc_paths`` - directories to find source files. Defaults to
   ``["src"]``, can be configured as:

``[erlc_paths: ["src", "other"]]``

-  ``:yecc_options`` - compilation options that apply to Yecc's
   compiler. There are many other available options here:
   http://www.erlang.org/doc/man/yecc.html#file-1






Summary
-------

========================== =
:elixir:func:`manifests/0` Returns Yecc manifests 

:elixir:func:`run/1`       Runs this task 
========================== =





Functions
---------

.. elixir:function:: Mix.Tasks.Compile.Yecc.manifests/0
   :sig: manifests()


   
   Returns Yecc manifests.
   
   

.. elixir:function:: Mix.Tasks.Compile.Yecc.run/1
   :sig: run(args)


   
   Runs this task.
   
   







