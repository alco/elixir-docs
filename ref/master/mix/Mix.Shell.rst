Mix.Shell
==============================================================

.. elixir:module:: Mix.Shell

   :mtype: behaviour

Overview
--------

Defines Mix.Shell contract.





Summary
-------

============================ =
:elixir:func:`cmd/2`         An implementation of the command callback that is shared across different shells 

:elixir:func:`output_app?/0` Returns if we should output application name to shell. Calling this function automatically toggles its value to false 
============================ =





Functions
---------

.. elixir:function:: Mix.Shell.cmd/2
   :sig: cmd(command, callback)


   
   An implementation of the command callback that is shared across
   different shells.
   
   

.. elixir:function:: Mix.Shell.output_app?/0
   :sig: output_app?()


   
   Returns if we should output application name to shell. Calling this
   function automatically toggles its value to false.
   
   







Callbacks
---------

.. elixir:callback:: Mix.Shell.cmd/1
   :sig: cmd/1


   Specs:
   
 
   * cmd(command :: :elixir:type:`String.t/0`) :: integer
 

   
   Executes the given command and returns its exit status.
   
   

.. elixir:callback:: Mix.Shell.error/1
   :sig: error/1


   Specs:
   
 
   * error(message :: :elixir:type:`String.t/0`) :: any
 

   
   Warns about the given error message.
   
   

.. elixir:callback:: Mix.Shell.info/1
   :sig: info/1


   Specs:
   
 
   * info(message :: :elixir:type:`String.t/0`) :: any
 

   
   Informs the given message.
   
   

.. elixir:callback:: Mix.Shell.prompt/1
   :sig: prompt/1


   Specs:
   
 
   * prompt(message :: :elixir:type:`String.t/0`) :: :elixir:type:`String.t/0`
 

   
   Prompts the user for input.
   
   

.. elixir:callback:: Mix.Shell.yes?/1
   :sig: yes?/1


   Specs:
   
 
   * yes?(message :: :elixir:type:`String.t/0`) :: boolean
 

   
   Asks the user for confirmation.
   
   



