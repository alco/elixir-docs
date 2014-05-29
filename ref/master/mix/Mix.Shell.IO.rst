Mix.Shell.IO
==============================================================

.. elixir:module:: Mix.Shell.IO

   :mtype: 

Overview
--------

This is Mix's default shell. It simply prints messages to stdio and
stderr.





Summary
-------

======================= =
:elixir:func:`cmd/1`    Executes the given command and prints its output to stdout as it comes 

:elixir:func:`error/1`  Writes an error message to the shell followed by new line 

:elixir:func:`info/1`   Writes a message to the shell followed by new line 

:elixir:func:`prompt/1` Writes a message shell followed by prompting the user for input. Input will be consumed until enter is pressed 

:elixir:func:`yes?/1`   Receives a message and asks the user if he wants to proceed. He must press enter or type anything that matches the a "yes" regex ``~r/^Y(es)?$/i`` 
======================= =





Functions
---------

.. elixir:function:: Mix.Shell.IO.cmd/1
   :sig: cmd(command)


   
   Executes the given command and prints its output to stdout as it comes.
   
   

.. elixir:function:: Mix.Shell.IO.error/1
   :sig: error(message)


   
   Writes an error message to the shell followed by new line.
   
   

.. elixir:function:: Mix.Shell.IO.info/1
   :sig: info(message)


   
   Writes a message to the shell followed by new line.
   
   

.. elixir:function:: Mix.Shell.IO.prompt/1
   :sig: prompt(message)


   
   Writes a message shell followed by prompting the user for input. Input
   will be consumed until enter is pressed.
   
   

.. elixir:function:: Mix.Shell.IO.yes?/1
   :sig: yes?(message)


   
   Receives a message and asks the user if he wants to proceed. He must
   press enter or type anything that matches the a "yes" regex
   ``~r/^Y(es)?$/i``.
   
   







