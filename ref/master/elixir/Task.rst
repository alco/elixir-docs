Task
==============================================================

.. elixir:module:: Task

   :mtype: 

Overview
--------

Conveniences for spawning and awaiting for tasks.

Tasks are processes that meant to execute one particular action
throughout their life-cycle, often with little explicit communication
with other processes. The most common use case for tasks is to compute a
value asynchronously:

::

    task = Task.async(fn -> do_some_work() end)
    res  = do_some_other_work()
    res + Task.await(task)

Tasks spawned with async can be awaited on by its caller process (and
only its caller) as shown in the example above. They are implemented by
spawning a process that sends a message to the caller once the given
computation is performed.

Besides ```async/1`` <#async/1>`__ and ``await/1``, tasks can also be
used as part of supervision trees and dynamically spawned in remote
nodes. We will explore all three scenarios next.

async and await
~~~~~~~~~~~~~~~

The most common way to spawn a task is with
```Task.async/1`` <Task.html#async/1>`__. A new process will be created
and this process is linked and monitored by the caller. However, the
processes are unlinked right before the task finishes, allowing the
proper error to be triggered only on ``await/1``.

This implies three things:

1) In case the caller crashes, the task will be killed and its
   computation will abort;

2) In case the task crashes due to an error, the parent will crash only
   on ``await/1``;

3) In case the task crashes because a linked process caused it to crash,
   the parent will crash immediately;

Supervised tasks
~~~~~~~~~~~~~~~~

It is also possible to spawn a task inside a supervision tree with
```start_link/1`` <#start_link/1>`__ and
```start_link/3`` <#start_link/3>`__:

::

    Task.start_link(fn -> IO.puts "ok" end)

Such can be mounted in your supervision tree as:

::

    import Supervisor.Spec

    children = [
      worker(Task, [fn -> IO.puts "ok" end])
    ]

Since such tasks are supervised and not directly linked to the caller,
they cannot be awaited on. For such reason, differently from
```async/1`` <#async/1>`__, ```start_link/1`` <#start_link/1>`__ returns
``{:ok, pid}`` (which is the result expected by supervision trees).

Such tasks are useful as workers that run during your application
life-cycle and rarely communicate with other workers. For example, a
worker that pushes data to another server or a worker that consumes
events from an event manager and writes it to a log file.

Supervision trees
~~~~~~~~~~~~~~~~~

The ```Task.Supervisor`` <Task.Supervisor.html>`__ module allows
developers to start supervisors that dynamically supervise tasks:

::

    {:ok, pid} = Task.Supervisor.start_link()
    Task.Supervisor.async(pid, fn -> do_work() end)

```Task.Supervisor`` <Task.Supervisor.html>`__ also makes it possible to
spawn tasks in remote nodes as long as the supervisor is registered
locally or globally:

::

    # In the remote node
    Task.Supervisor.start_link(name: :tasks_sup)

    # On the client
    Task.Supervisor.async({:tasks_sup, :remote@local}, fn -> do_work() end)

```Task.Supervisor`` <Task.Supervisor.html>`__ is more often started in
your supervision tree as:

::

    import Supervisor.Spec

    children = [
      supervisor(Task.Supervisor, [[name: :tasks_sup]])
    ]

Check ```Task.Supervisor`` <Task.Supervisor.html>`__ for other
operations supported by the Task supervisor.





Summary
-------

=========================== =
:elixir:func:`__struct__/0` The Task struct 

:elixir:func:`async/1`      Starts a task that can be awaited on 

:elixir:func:`async/3`      Starts a task that can be awaited on 

:elixir:func:`await/2`      Awaits for a task reply 

:elixir:func:`find/2`       Receives a group of tasks and a message and finds a task that matches the given message 

:elixir:func:`start_link/1` Starts a task as part of a supervision tree 

:elixir:func:`start_link/3` Starts a task as part of a supervision tree 
=========================== =



Types
-----

.. elixir:type:: Task.t/0

   :elixir:type:`t/0` :: %Task{pid: term, ref: term}
   





Functions
---------

.. elixir:function:: Task.__struct__/0
   :sig: __struct__()


   Specs:
   
 
   * __struct__ :: :elixir:type:`t/0`
 

   
   The Task struct.
   
   It contains two fields:
   
   -  ``:pid`` - the proces reference of the task process. It may be a pid
      or a tuple containing the process and node names;
   
   -  ``:ref`` - the task monitor reference;
   
   
   
   

.. elixir:function:: Task.async/1
   :sig: async(fun)


   Specs:
   
 
   * async((... -> any)) :: :elixir:type:`t/0`
 

   
   Starts a task that can be awaited on.
   
   This function spawns a process that is linked and monitored to the
   caller process. A ```Task`` <Task.html>`__ struct is returned containing
   the relevant information.
   
   **Task's message format**
   
   The reply sent by the task will be in the format ``{ref, msg}``, where
   ``ref`` is the monitoring reference hold by the task.
   
   

.. elixir:function:: Task.async/3
   :sig: async(mod, fun, args)


   Specs:
   
 
   * async(module, atom, [term]) :: :elixir:type:`t/0`
 

   
   Starts a task that can be awaited on.
   
   Similar to ```async/1`` <#async/1>`__, but the task is specified by the
   given module, function and arguments.
   
   

.. elixir:function:: Task.await/2
   :sig: await(task, timeout \\ 5000)


   Specs:
   
 
   * await(:elixir:type:`t/0`, timeout) :: term | no_return
 

   
   Awaits for a task reply.
   
   A timeout, in miliseconds, can be given with default value of ``5000``.
   In case the task process dies, this function will exit with the same
   reason as the task.
   
   

.. elixir:function:: Task.find/2
   :sig: find(tasks, msg)


   Specs:
   
 
   * find([:elixir:type:`t/0`], any) :: {term, :elixir:type:`t/0`} | nil | no_return
 

   
   Receives a group of tasks and a message and finds a task that matches
   the given message.
   
   This function returns a tuple with the task and the returned value in
   case the message matches a task that exited with success, it raises in
   case the found task failed or nil if no task was found.
   
   This function is useful in situations where multiple tasks are spawned
   and their results are collected just later on. For example, a GenServer
   can spawn tasks, store the tasks in a list and later use
   ```Task.find/2`` <Task.html#find/2>`__ to see if upcoming messages are
   from any of the tasks.
   
   

.. elixir:function:: Task.start_link/1
   :sig: start_link(fun)


   Specs:
   
 
   * start_link((... -> any)) :: {:ok, pid}
 

   
   Starts a task as part of a supervision tree.
   
   

.. elixir:function:: Task.start_link/3
   :sig: start_link(mod, fun, args)


   Specs:
   
 
   * start_link(module, atom, [term]) :: {:ok, pid}
 

   
   Starts a task as part of a supervision tree.
   
   







