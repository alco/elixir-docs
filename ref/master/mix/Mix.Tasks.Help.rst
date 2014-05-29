Mix.Tasks.Help
==============================================================

.. elixir:module:: Mix.Tasks.Help

   :mtype: 

Overview
--------

Lists all tasks or prints the documentation for a given task.

Arguments
~~~~~~~~~

::

    mix help      - prints all tasks and their shortdoc
    mix help TASK - prints full docs for the given task

Colors
~~~~~~

When possible, ``mix help`` is going to use coloring for formatting
guides. The formatting can be customized by configuring the Mix
application either inside your project (in ``config/config.exs``) or by
using the local config (in ``~/.mix/config.exs``).

For example, to disable, one may:

::

    [mix: [colors: [enabled: false]]]

The available color options are:

-  ``:enabled`` - show ANSI formatting (defaults to IO.ANSI.terminal?)
-  ``:doc_code`` — the attributes for code blocks (cyan, bright)
-  ``:doc_inline_code`` - inline code (cyan)
-  ``:doc_headings`` - h1 and h2 (yellow, bright)
-  ``:doc_title`` — the overall heading for the output
   (reverse,yellow,bright)
-  ``:doc_bold`` - (bright)
-  ``:doc_underline`` - (underline)






Summary
-------

==================== =
:elixir:func:`run/1` Callback implementation of :elixir:func:`Mix.Task.run/1` 
==================== =





Functions
---------

.. elixir:function:: Mix.Tasks.Help.run/1
   :sig: run(arg1)


   
   Callback implementation of :elixir:func:`Mix.Task.run/1`.
   
   







