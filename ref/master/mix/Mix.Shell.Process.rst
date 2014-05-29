Mix.Shell.Process
==============================================================

.. elixir:module:: Mix.Shell.Process

   :mtype: 

Overview
--------

This is a Mix shell that uses the current process mailbox for
communication instead of IO.

When a developer calls ``info("hello")``, the following message will be
sent to the current process:

::

    {:mix_shell, :info, ["hello"]}

This is mainly useful in tests, allowing us to assert if given messages
were received or not. Since we need to guarantee a clean slate between
tests, there is also a :elixir:func:`flush/1` function responsible for flushing all
``:mix_shell`` related messages from the process inbox.





Summary
-------

======================= =
:elixir:func:`cmd/1`    Executes the given command and forwards its messages to the current process 

:elixir:func:`error/1`  Forwards the message to the current process 

:elixir:func:`flush/1`  Flush all ``:mix_shell`` and ``:mix_shell_input`` messages from the current process. If a callback is given, it is invoked for each received message 

:elixir:func:`info/1`   Forwards the message to the current process 

:elixir:func:`prompt/1` Forwards the message to the current process. It also checks the inbox for an input message matching: 

:elixir:func:`yes?/1`   Forwards the message to the current process. It also checks the inbox for an input message matching: 
======================= =





Functions
---------

.. elixir:function:: Mix.Shell.Process.cmd/1
   :sig: cmd(command)


   
   Executes the given command and forwards its messages to the current
   process.
   
   

.. elixir:function:: Mix.Shell.Process.error/1
   :sig: error(message)


   
   Forwards the message to the current process.
   
   

.. elixir:function:: Mix.Shell.Process.flush/1
   :sig: flush(callback \\ fn x -> x end)


   
   Flush all ``:mix_shell`` and ``:mix_shell_input`` messages from the
   current process. If a callback is given, it is invoked for each received
   message.
   
   **Examples**
   
   ::
   
       flush &IO.inspect(&1)
   
   
   

.. elixir:function:: Mix.Shell.Process.info/1
   :sig: info(message)


   
   Forwards the message to the current process.
   
   

.. elixir:function:: Mix.Shell.Process.prompt/1
   :sig: prompt(message)


   
   Forwards the message to the current process. It also checks the inbox
   for an input message matching:
   
   ::
   
       {:mix_shell_input, :prompt, value}
   
   If one does not exist, it will abort since there was no shell process
   inputs given. Value must be a string.
   
   

.. elixir:function:: Mix.Shell.Process.yes?/1
   :sig: yes?(message)


   
   Forwards the message to the current process. It also checks the inbox
   for an input message matching:
   
   ::
   
       {:mix_shell_input, :yes?, value}
   
   If one does not exist, it will abort since there was no shell process
   inputs given. Value must be ``true`` or ``false``.
   
   







