Agent
==============================================================

.. elixir:module:: Agent

   :mtype: 

Overview
--------

Agents are a simple abstraction around state.

Often in Elixir there is a need to share or store state that must be
accessed from different processes or by a same process in different
points in time.

The Agent module provides a basic server implementation that allows
state to be retrieved and updated via a simple API.

Examples
~~~~~~~~

For example, in the Mix tool that ships with Elixir, we need to keep a
set of all tasks executed by a given project. Since this set is shared,
we can implement it with an Agent:

::

    defmodule Mix.TasksServer do
      def start_link do
        Agent.start_link(fn -> HashSet.new end, name: __MODULE__)
      end

      @doc "Checks if the task has already executed"
      def executed?(task, project) do
        item = {task, project}
        Agent.get(__MODULE__, fn set ->
          item in set
        end)
      end

      @doc "Marks a task as executed"
      def put_task(task, project) do
        item = {task, project}
        Agent.update(__MODULE__, &Set.put(&1, item))
      end
    end

Note that agents still provide a segregation in between the client and
server APIs, as seen in GenServers. In particular, all code inside the
function passed to the agent is executed by the agent. This distinction
is important because you may want to avoid expensive operations inside
the agent, as it will effectively block the agent until the request is
fullfilled.

Consider these two examples:

::

    # Compute in the agent/server
    def get_something(agent) do
      Agent.get(agent, fn state -> do_something_expensive(state) end)
    end

    # Compute in the agent/client
    def get_something(agent) do
      Agent.get(agent, &(&1)) |> do_something_expensive()
    end

The first one blocks the agent while the second one copies all the state
to the client and executes the operation in the client. The trade-off
here is exactly if the data is small enough to be sent to the client
cheaply or large enough to require processing on the server (or at least
some initial processing).

Name Registration
~~~~~~~~~~~~~~~~~

An Agent is bound to the same name registration rules as GenServers.
Read more about it in the :elixir:mod:`GenServer` docs.

A word on distributed agents
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

It is important to consider the limitations of distributed agents.
Agents work by sending anonymous functions in between the caller and the
agent. In a distributed setup with multiple nodes, agents only work if
the caller (client) and the agent have the same version of a given
module.

This setup may exhibit issues when doing "rolling upgrades". By rolling
upgrades we mean the following situation: you wish to deploy a new
version of your software by *shutting down* some of your nodes and
replacing them by nodes running a new version of the software. In this
setup, part of your environment will have one version of a given module
and the other part another version (the newer one) of the same module;
this may cause agents to crash. That said, if you plan to run in
distributed environments, agents should likely be avoided.

Note, however, that agents work fine if you want to perform hot code
swapping, as it keeps both the old and new versions of a given module.
We detail how to do hot code swapping with agents in the next section.

Hot code swapping
~~~~~~~~~~~~~~~~~

An agent can have its code hot swapped live by simply passing a module,
function and args tuple to the update instruction. For example, imagine
you have an agent named ``:sample`` and you want to convert its inner
state from some dict structure to a map. It can be done with the
following instruction:

::

    {:update, :sample, {:advanced, {Enum, :into, [%{}]}}}

The agent's state will be added to the given list as the first argument.





Summary
-------

=============================== =
:elixir:func:`cast/2`           Performs a cast (fire and forget) operation on the agent state 

:elixir:func:`get/3`            Gets the agent value and executes the given function 

:elixir:func:`get_and_update/3` Gets and updates the agent state in one operation 

:elixir:func:`start/2`          Starts an agent process without links (outside of a supervision tree) 

:elixir:func:`start_link/2`     Starts an agent linked to the current process 

:elixir:func:`stop/2`           Stops the agent 

:elixir:func:`update/3`         Updates the agent state 
=============================== =



Types
-----

.. elixir:type:: Agent.on_start/0

   :elixir:type:`on_start/0` :: {:ok, pid} | {:error, {:already_started, pid} | term}
   

   Return values of ``start*`` functions
   

.. elixir:type:: Agent.name/0

   :elixir:type:`name/0` :: atom | {:global, term} | {:via, module, term}
   

   The agent name
   

.. elixir:type:: Agent.agent/0

   :elixir:type:`agent/0` :: pid | {atom, node} | :elixir:type:`name/0`
   

   The agent reference
   

.. elixir:type:: Agent.state/0

   :elixir:type:`state/0` :: term
   

   The agent state
   





Functions
---------

.. elixir:function:: Agent.cast/2
   :sig: cast(agent, fun)


   Specs:
   
 
   * cast(:elixir:type:`agent/0`, (:elixir:type:`state/0` -> :elixir:type:`state/0`)) :: :ok
 

   
   Performs a cast (fire and forget) operation on the agent state.
   
   The function ``fun`` is sent to the ``agent`` which invokes the function
   passing the agent state. The function must return the new state.
   
   Note that ``cast`` returns ``:ok`` immediately, regardless of whether
   the destination node or agent exists.
   
   

.. elixir:function:: Agent.get/3
   :sig: get(agent, fun, timeout \\ 5000)


   Specs:
   
 
   * (get(:elixir:type:`agent/0`, (:elixir:type:`state/0` -> a), timeout) :: a) when a: var
 

   
   Gets the agent value and executes the given function.
   
   The function ``fun`` is sent to the ``agent`` which invokes the function
   passing the agent state. The result of the function invocation is
   returned.
   
   A timeout can also be specified (it has a default value of 5000).
   
   

.. elixir:function:: Agent.get_and_update/3
   :sig: get_and_update(agent, fun, timeout \\ 5000)


   Specs:
   
 
   * (get_and_update(:elixir:type:`agent/0`, (:elixir:type:`state/0` -> {a, :elixir:type:`state/0`}), timeout) :: a) when a: var
 

   
   Gets and updates the agent state in one operation.
   
   The function ``fun`` is sent to the ``agent`` which invokes the function
   passing the agent state. The function must return a tuple with two
   elements, the first being the value to return (i.e. the get value) and
   the second one is the new state.
   
   A timeout can also be specified (it has a default value of 5000).
   
   

.. elixir:function:: Agent.start/2
   :sig: start(fun, options \\ [])


   Specs:
   
 
   * start((() -> term), :elixir:type:`GenServer.options/0`) :: :elixir:type:`on_start/0`
 

   
   Starts an agent process without links (outside of a supervision tree).
   
   See :elixir:func:`start_link/2` for more information.
   
   

.. elixir:function:: Agent.start_link/2
   :sig: start_link(fun, options \\ [])


   Specs:
   
 
   * start_link((() -> term), :elixir:type:`GenServer.options/0`) :: :elixir:type:`on_start/0`
 

   
   Starts an agent linked to the current process.
   
   This is often used to start the agent as part of a supervision tree.
   
   Once the agent is spawned, the given function is invoked and its return
   value is used as the agent state. Note that ``start_link`` does not
   return until the given function has returned.
   
   **Options**
   
   The ``:name`` option is used for registration as described in the module
   documentation.
   
   If the ``:timeout`` option is present, the agent is allowed to spend at
   most the given amount of milliseconds on initialization or it will be
   terminated and the start function will return ``{:error, :timeout}``.
   
   If the ``:debug`` option is present, the corresponding function in the
   ```:sys`` module <http://www.erlang.org/doc/man/sys.html>`__ will be
   invoked.
   
   If the ``:spawn_opt`` option is present, its value will be passed as
   options to the underlying process as in :elixir:func:`Process.spawn/4`.
   
   **Return values**
   
   If the server is successfully created and initialized, the function
   returns ``{:ok, pid}``, where pid is the pid of the server. If there
   already exists an agent with the specified name, the function returns
   ``{:error, {:already_started, pid}}`` with the pid of that process.
   
   If the given function callback fails with ``reason``, the function
   returns ``{:error, reason}``.
   
   

.. elixir:function:: Agent.stop/2
   :sig: stop(agent, timeout \\ 5000)


   Specs:
   
 
   * stop(:elixir:type:`agent/0`, timeout) :: :ok
 

   
   Stops the agent.
   
   Returns ``:ok`` if the agent is stopped within the given ``timeout``.
   
   

.. elixir:function:: Agent.update/3
   :sig: update(agent, fun, timeout \\ 5000)


   
   Updates the agent state.
   
   The function ``fun`` is sent to the ``agent`` which invokes the function
   passing the agent state. The function must return the new state.
   
   A timeout can also be specified (it has a default value of 5000). This
   function always returns ``:ok``.
   
   







