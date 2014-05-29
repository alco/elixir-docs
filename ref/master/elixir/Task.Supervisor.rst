Task.Supervisor
==============================================================

.. elixir:module:: Task.Supervisor

   :mtype: 

Overview
--------

A tasks supervisor.

This module defines a supervisor which can be used to dynamically
supervise tasks. Behind the scenes, this module is implemented as a
``:simple_one_for_one`` supervisor where the workers are temporary (i.e.
they are not restarted after they die).

The functions in this module allow tasks can be spawned and awaited from
a supervisor, similar to the functions defined in the
```Task`` <Task.html>`__ module.

Name Registration
~~~~~~~~~~~~~~~~~

A ```Task.Supervisor`` <Task.Supervisor.html>`__ is bound to the same
name registration rules as a ```GenServer`` <GenServer.html>`__. Read
more about it in the ```GenServer`` <GenServer.html>`__ docs.





Summary
-------

================================ =
:elixir:func:`async/2`           Starts a task that can be awaited on 

:elixir:func:`async/4`           Starts a task that can be awaited on 

:elixir:func:`children/1`        Returns all children pids 

:elixir:func:`start_child/2`     Starts a task as child of the given ``supervisor`` 

:elixir:func:`start_child/4`     Starts a task as child of the given ``supervisor`` 

:elixir:func:`start_link/1`      Starts a new supervisor 

:elixir:func:`terminate_child/2` Terminates the given child at pid 
================================ =





Functions
---------

.. elixir:function:: Task.Supervisor.async/2
   :sig: async(supervisor, fun)


   Specs:
   
 
   * async(:elixir:type:`Supervisor.supervisor/0`, (... -> any)) :: :elixir:type:`Task.t/0`
 

   
   Starts a task that can be awaited on.
   
   The ``supervisor`` must be a reference as defined in
   ```Task.Supervisor`` <Task.Supervisor.html>`__. For more information on
   tasks, check the ```Task`` <Task.html>`__ module.
   
   

.. elixir:function:: Task.Supervisor.async/4
   :sig: async(supervisor, module, fun, args)


   Specs:
   
 
   * async(:elixir:type:`Supervisor.supervisor/0`, module, atom, [term]) :: :elixir:type:`Task.t/0`
 

   
   Starts a task that can be awaited on.
   
   The ``supervisor`` must be a reference as defined in
   ```Task.Supervisor`` <Task.Supervisor.html>`__. For more information on
   tasks, check the ```Task`` <Task.html>`__ module.
   
   

.. elixir:function:: Task.Supervisor.children/1
   :sig: children(supervisor)


   Specs:
   
 
   * children(:elixir:type:`Supervisor.supervisor/0`) :: [pid]
 

   
   Returns all children pids.
   
   

.. elixir:function:: Task.Supervisor.start_child/2
   :sig: start_child(supervisor, fun)


   Specs:
   
 
   * start_child(:elixir:type:`Supervisor.supervisor/0`, (... -> any)) :: {:ok, pid}
 

   
   Starts a task as child of the given ``supervisor``.
   
   Note the spawned process is not linked to the caller but only to the
   supervisor. This command is useful in case the task needs to emit
   side-effects (like I/O) and does not need to report back to the caller.
   
   

.. elixir:function:: Task.Supervisor.start_child/4
   :sig: start_child(supervisor, module, fun, args)


   Specs:
   
 
   * start_child(:elixir:type:`Supervisor.supervisor/0`, module, atom, [term]) :: {:ok, pid}
 

   
   Starts a task as child of the given ``supervisor``.
   
   Similar to ```start_child/2`` <#start_child/2>`__ except the task is
   specified by the given ``module``, ``fun`` and ``args``.
   
   

.. elixir:function:: Task.Supervisor.start_link/1
   :sig: start_link(opts \\ [])


   Specs:
   
 
   * start_link(:elixir:type:`Supervisor.options/0`) :: :elixir:type:`Supervisor.on_start/0`
 

   
   Starts a new supervisor.
   
   The supported options are:
   
   -  ``:name`` - used to register a supervisor name, the supported values
      are described under the ``Name Registration`` section in the
      ```GenServer`` <GenServer.html>`__ module docs;
   
   -  ``:shutdown`` - ``:brutal_kill`` if the tasks must be killed directly
      on shutdown or an integer indicating the timeout value, defaults to
      5000 miliseconds;
   
   
   
   

.. elixir:function:: Task.Supervisor.terminate_child/2
   :sig: terminate_child(supervisor, pid)


   Specs:
   
 
   * terminate_child(:elixir:type:`Supervisor.supervisor/0`, pid) :: :ok
 

   
   Terminates the given child at pid.
   
   







