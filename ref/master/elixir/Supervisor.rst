Supervisor
==============================================================

.. elixir:module:: Supervisor

   :mtype: 

Overview
--------

A behaviour module for implementing supevision functionality.

A supervisor is a process which supervises other processes called child
processes. Supervisors are used to build an hierarchical process
structure called a supervision tree, a nice way to structure
fault-tolerant applications.

A supervisor implemented using this module will have a standard set of
interface functions and include functionality for tracing and error
reporting. It will also fit into an supervision tree.

Example
~~~~~~~

In order to define a supervisor, we need to first define a child process
that is going to be supervised. In order to do so, we will define a
GenServer that represents a stack:

::

    defmodule Stack do
      use GenServer

      def start_link(state) do
        GenServer.start_link(__MODULE__, state, [name: :sup_stack])
      end

      def handle_call(:pop, _from, [h|t]) do
        {:reply, h, t}
      end

      def handle_cast({:push, h}, _from, t) do
        {:noreply, [h|t]}
      end
    end

We can now define our supervisor and start it as follows:

::

    # Import helpers for defining supervisors
    import Supervisor.Spec

    # We are going to supervise the Stack server which will
    # be started with a single argument [:hello]
    children = [
      worker(Stack, [[:hello]])
    ]

    # Start the supervisor with our one child
    {:ok, pid} = Supervisor.start_link(children, strategy: :one_for_one)

Notice that when starting the GenServer, we have registered it with name
``:sup_stack``, which allows us to call it directly and get what is on
the stack:

::

    GenServer.call(:sup_stack, :pop)
    #=> :hello

    GenServer.cast(:sup_stack, {:push, :world})
    #=> :ok

    GenServer.call(:sup_stack, :pop)
    #=> :world

However, there is a bug in our stack server. If we call ``:pop`` and the
stack is empty, it is going to crash because no clause matches. Let's
try it:

::

    GenServer.call(:sup_stack, :pop)
    =ERROR REPORT====

Luckily, since the server is being supervised by a supervisor, the
supervisor will automatically start a new one, with the default stack of
``[:hello]`` like before:

::

    GenServer.call(:sup_stack, :pop) == :hello

Supervisors support different strategies; in the example above, we have
chosen ``:one_for_one``. Furthermore, each supervisor can have many
workers and supervisors as children, each of them with their specific
configuration, shutdown values, and restart strategies.

Continue reading this moduledoc to learn more about supervision
strategies and then follow to the :elixir:mod:`Supervisor.Spec` module
documentation to learn about the specification for workers and
supervisors.

Module-based supervisors
~~~~~~~~~~~~~~~~~~~~~~~~

In the example above, a supervisor was dynamically created by passing
the supervision structure to :elixir:func:`start_link/2`. However, supervisors can
also be created by explicitly defining a supevision module:

::

    defmodule MyApp.Supervisor do
      use Supervisor

      def start_link do
        Supervisor.start_link(__MODULE__, [])
      end

      def init([]) do
        import Supervisor.Spec

        children = [
          worker(Stack, [[:hello]])
        ]

        supervisor(children, strategy: :one_for_one)
      end
    end

You may want to use a module-based supervisor if:

-  You need to do some particular action on supervisor initialization,
   like setting up a ETS table;

-  You want to perform partial hot-code swapping of the tree. For
   example, if you add or remove a children, the module-based
   supervision will add and remove the new children directly, while the
   dynamic supervision requires the whole tree to be restarted in order
   to perform such swaps;

Strategies
~~~~~~~~~~

-  ``:one_for_one`` - If a child process terminates, only that process
   is restarted;

-  ``:one_for_all`` - If a child process terminates, all other child
   processes are terminated and then all child processes (including the
   terminated one) are restarted;

-  ``:rest_for_one`` - If a child process terminates, the "rest" of the
   child processes, i.e. the child processes after the terminated one in
   start order, are terminated. Then the terminated child process and
   the rest of the child processes are restarted;

-  ``:simple_one_for_one`` - Similar to ``:one_for_one`` but suits
   better when dynamically attaching children. This strategy requires
   the supervisor specification to contain only one children. Many
   functions in this module behave slightly differently when this
   strategy is used;

Name Registration
~~~~~~~~~~~~~~~~~

A supervisor is bound to the same name registration rules as a
:elixir:mod:`GenServer`. Read more about it in the :elixir:mod:`GenServer` docs.





Summary
-------

================================ =
:elixir:func:`count_children/1`  Returns a map containing count values for the supervisor 

:elixir:func:`delete_child/2`    Deletes the child specification identified by ``child_id`` 

:elixir:func:`restart_child/2`   Restarts a child process identified by ``child_id`` 

:elixir:func:`start_child/2`     Dynamically adds and starts a child specification to the supervisor 

:elixir:func:`start_link/2`      Starts a supervisor with the given children 

:elixir:func:`start_link/3`      Starts a supervisor module with the given ``arg`` 

:elixir:func:`terminate_child/2` Terminates the given pid or child id 

:elixir:func:`which_children/1`  Returns a list with information about all children 
================================ =



Types
-----

.. elixir:type:: Supervisor.on_start/0

   :elixir:type:`on_start/0` :: {:ok, pid} | :ignore | {:error, {:already_started, pid} | {:shutdown, term} | term}
   

   Return values of ``start_link`` functions
   

.. elixir:type:: Supervisor.on_start_child/0

   :elixir:type:`on_start_child/0` :: {:ok, :elixir:type:`child/0`} | {:ok, :elixir:type:`child/0`, info :: term} | {:error, {:already_started, :elixir:type:`child/0`} | :already_present | term}
   

   Return values of ``start_child`` functions
   

.. elixir:type:: Supervisor.child/0

   :elixir:type:`child/0` :: pid | :undefined
   

.. elixir:type:: Supervisor.name/0

   :elixir:type:`name/0` :: atom | {:global, term} | {:via, module, term}
   

   The Supervisor name
   

.. elixir:type:: Supervisor.options/0

   :elixir:type:`options/0` :: [name: :elixir:type:`name/0`, strategy: :elixir:type:`Supervisor.Spec.strategy/0`, max_restarts: non_neg_integer, max_seconds: non_neg_integer]
   

   Options used by the ``start*`` functions
   

.. elixir:type:: Supervisor.supervisor/0

   :elixir:type:`supervisor/0` :: pid | :elixir:type:`name/0` | {atom, node}
   

   The supervisor reference
   





Functions
---------

.. elixir:function:: Supervisor.count_children/1
   :sig: count_children(supervisor)


   Specs:
   
 
   * count_children(:elixir:type:`supervisor/0`) :: [specs: non_neg_integer, active: non_neg_integer, supervisors: non_neg_integer, workers: non_neg_integer]
 

   
   Returns a map containing count values for the supervisor.
   
   The map contains the following keys:
   
   -  ``:specs`` - the total count of children, dead or alive;
   
   -  ``:active`` - the count of all actively running child processes
      managed by this supervisor;
   
   -  ``:supervisors`` - the count of all supervisors whether or not the
      child process is still alive;
   
   -  ``:workers`` - the count of all workers, whether or not the child
      process is still alive;
   
   
   
   

.. elixir:function:: Supervisor.delete_child/2
   :sig: delete_child(supervisor, child_id)


   Specs:
   
 
   * (delete_child(:elixir:type:`supervisor/0`, :elixir:type:`Supervisor.Spec.child_id/0`) :: :ok | {:error, error}) when error: :not_found | :simple_one_for_one | :running | :restarting
 

   
   Deletes the child specification identified by ``child_id``.
   
   The corresponding child process must not be running, use
   :elixir:func:`terminate_child/2` to terminate it.
   
   If successful, the function returns ``:ok``. This function may error
   with an appropriate error tuple if the ``child_id`` is not found, or if
   the current process is running or being restarted.
   
   This operation is not supported by ``simple_one_for_one`` supervisors.
   
   

.. elixir:function:: Supervisor.restart_child/2
   :sig: restart_child(supervisor, child_id)


   Specs:
   
 
   * (restart_child(:elixir:type:`supervisor/0`, :elixir:type:`Supervisor.Spec.child_id/0`) :: {:ok, :elixir:type:`child/0`} | {:ok, :elixir:type:`child/0`, term} | {:error, error}) when error: :not_found | :simple_one_for_one | :running | :restarting | term
 

   
   Restarts a child process identified by ``child_id``.
   
   The child specification must exist and the corresponding child process
   must not be running.
   
   Note that for temporary children, the child specification is
   automatically deleted when the child terminates, and thus it is not
   possible to restart such children.
   
   If the child process start function returns ``{:ok, child}`` or
   ``{:ok, child, info}``, the pid is added to the supervisor and the
   function returns the same value.
   
   If the child process start function returns ``:ignore``, the pid remains
   set to ``:undefined`` and the function returns ``{:ok, :undefined}``.
   
   This function may error with an appropriate error tuple if the
   ``child_id`` is not found, or if the current process is running or being
   restarted.
   
   If the child process start function returns an error tuple or an
   erroneous value, or if it fails, the function returns
   ``{:error, error}``.
   
   This operation is not supported by ``simple_one_for_one`` supervisors.
   
   

.. elixir:function:: Supervisor.start_child/2
   :sig: start_child(supervisor, child_spec_or_args)


   Specs:
   
 
   * start_child(:elixir:type:`supervisor/0`, :elixir:type:`Supervisor.Spec.spec/0` | [term]) :: :elixir:type:`on_start_child/0`
 

   
   Dynamically adds and starts a child specification to the supervisor.
   
   ``child_spec`` should be a valid child specification (unless the
   supervisor is a ``:simple_one_for_one`` supervisor, see below). The
   child process will be started as defined in the child specification.
   
   In the case of ``:simple_one_for_one``, the child specification defined
   in the supervisor will be used and instead of a ``child_spec``, an
   arbitrary list of terms is expected. The child process will then be
   started by appending the given list to the existing function arguments
   in the child specification.
   
   If there already exists a child specification with the specified id,
   ``child_spec`` is discarded and the function returns an error with
   ``:already_started`` or ``:already_present`` if the corresponding child
   process is running or not.
   
   If the child process start function returns ``{:ok, child}`` or
   ``{:ok, child, info}``, the child specification and pid is added to the
   supervisor and the function returns the same value.
   
   If the child process start function returns
   ``:ignore, the child specification is added to the supervisor, the pid is set to undefined and the function returns``\ {:ok,
   :undefined}\`.
   
   If the child process start function returns an error tuple or an
   erroneous value, or if it fails, the child specification is discarded
   and the function returns ``{:error, error}`` where ``error`` is a term
   containing information about the error and child specification.
   
   

.. elixir:function:: Supervisor.start_link/2
   :sig: start_link(children, options)


   Specs:
   
 
   * start_link([tuple], :elixir:type:`options/0`) :: :elixir:type:`on_start/0`
 

   
   Starts a supervisor with the given children.
   
   A strategy is required to be given as an option. Furthermore, the
   ``:max_restarts`` and ``:max_seconds`` value can be configured as
   described in :elixir:func:`Supervisor.Spec.supervise/2` docs.
   
   The options can also be used to register a supervisor name. the
   supported values are described under the ``Name Registration`` section
   in the :elixir:mod:`GenServer` module docs.
   
   If the supervisor and its child processes are successfully created (i.e.
   if the start function of all child processes returns ``{:ok, child}``,
   ``{:ok, child, info}``, or ``:ignore``) the function returns
   ``{:ok, pid}``, where ``pid`` is the pid of the supervisor. If there
   already exists a process with the specified name, the function returns
   ``{:error, {:already_started, pid}}``, where pid is the pid of that
   process.
   
   If any of the child process start functions fail or return an error
   tuple or an erroneous value, the supervisor will first terminate all
   already started child processes with reason ``:shutdown`` and then
   terminate itself and return ``{:error, {:shutdown, reason}}``.
   
   

.. elixir:function:: Supervisor.start_link/3
   :sig: start_link(module, arg, options \\ [])


   Specs:
   
 
   * start_link(module, term, :elixir:type:`options/0`) :: :elixir:type:`on_start/0`
 

   
   Starts a supervisor module with the given ``arg``.
   
   To start the supervisor, the ``init/1`` callback will be invoked in the
   given module. The ``init/1`` callback must return a supervision
   specification which can be created with the help of :elixir:mod:`Supervisor.Spec`
   module.
   
   If the ``init/1`` callback returns ``:ignore``, this function returns
   ``:ignore`` as well and the supervisor terminates with reason
   ``:normal``. If it fails or returns an incorrect value, this function
   returns ``{:error, term}`` where ``term`` is a term with information
   about the error, and the supervisor terminates with reason ``term``.
   
   The ``:name`` option can also be given in order to register a supervisor
   name, the supported values are described under the ``Name Registration``
   section in the :elixir:mod:`GenServer` module docs.
   
   Other failure conditions are specified in :elixir:func:`start_link/2` docs.
   
   

.. elixir:function:: Supervisor.terminate_child/2
   :sig: terminate_child(supervisor, pid_or_child_id)


   Specs:
   
 
   * (terminate_child(:elixir:type:`supervisor/0`, pid | :elixir:type:`Supervisor.Spec.child_id/0`) :: :ok | {:error, error}) when error: :not_found | :simple_one_for_one
 

   
   Terminates the given pid or child id.
   
   If the supervisor is not a ``simple_one_for_one``, the child id is
   expected and the process, if there is one, is terminated; the child
   specification is kept unless the child is temporary.
   
   In case of a ``simple_one_for_one`` supervisor, a pid is expected. If
   the child specification identifier is given instead of a ``pid``, the
   function will return ``{:error, :simple_one_for_one}``.
   
   A non-temporary child process may later be restarted by the supervisor.
   The child process can also be restarted explicitly by calling
   :elixir:func:`restart_child/2`. Use :elixir:func:`delete_child/2` to remove the child
   specification.
   
   If successful, the function returns ``:ok``. If there is no child
   specification or pid, the function returns ``{:error, :not_found}``.
   
   

.. elixir:function:: Supervisor.which_children/1
   :sig: which_children(supervisor)


   Specs:
   
 
   * which_children(:elixir:type:`supervisor/0`) :: [{:elixir:type:`Supervisor.Spec.child_id/0` | :undefined, :elixir:type:`child/0` | :restarting, :elixir:type:`Supervisor.Spec.worker/0`, :elixir:type:`Supervisor.Spec.modules/0`}]
 

   
   Returns a list with information about all children.
   
   Note that calling this function when supervising a large number of
   children under low memory conditions can cause an out of memory
   exception.
   
   This function returns a list of tuples containing:
   
   -  ``id`` - as defined in the child specification or ``:undefined`` in
      the case of a ``simple_one_for_one`` supervisor;
   
   -  ``child`` - the pid of the corresponding child process, the atom
      ``:restarting`` if the process is about to be restarted, or
      ``:undefined`` if there is no such process;
   
   -  ``type`` - ``:worker`` or ``:supervisor`` as defined in the child
      specification;
   
   -  ``modules`` – as defined in the child specification;
   
   
   
   







