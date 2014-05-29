Supervisor.Spec
==============================================================

.. elixir:module:: Supervisor.Spec

   :mtype: 

Overview
--------

Convenience functions for defining a supervision specification.

Example
~~~~~~~

By using the functions in this module one can define a supervisor and
start it with :elixir:func:`Supervisor.start_link/2`:

::

    import Supervisor.Spec

    children = [
      worker(MyWorker, [arg1, arg2, arg3]),
      supervisor(MySupervisor, [arg1])
    ]

    Supervisor.start_link(children, strategy: :one_for_one)

In many situations, it may be handy to define supervisors backed by a
module:

::

    defmodule MySupervisor do
      use Supervisor

      def start_link(arg) do
        Supervisor.start_link(__MODULE__, arg)
      end

      def init(arg) do
        children = [
          worker(MyWorker, [arg], restart: :temporary)
        ]

        supervise(children, strategy: :simple_one_for_one)
      end
    end

Notice in this case we don't have to explicitly import
:elixir:mod:`Supervisor.Spec` as ``use Supervisor`` automatically does so.

Explicit supervisors as above are required when there is a need to:

1. partialy change the supervision tree during hot-code swaps;

2. define supervisors inside other supervisors;

3. perform actions inside the supervision ``init/1`` callback.

For example, you may want to start an ETS table that is linked to the
supervisor (i.e. if the supervision tree needs to be restarted, the ETS
table must be restarted too);

Supervisor and worker options
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In the example above, we have defined workers and supervisors and each
accepts the following options:

-  ``:id`` - a name used to identify the child specification internally
   by the supervisor. Defaults to the given module name;

-  ``:function`` - the function to invoke on the child to start it;

-  ``:restart`` - defines when the child process should restart;

-  ``:shutdown`` - defines how a child process should be terminated;

-  ``:modules`` - it should be a list with one element ``[module]``,
   where module is the name of the callback module only if the child
   process is a :elixir:mod:`Supervisor` or :elixir:mod:`GenServer` If the child process is
   a :elixir:mod:`GenEvent`, modules should be ``:dynamic``;

Restart values
^^^^^^^^^^^^^^

The following restart values are supported:

-  ``:permanent`` - the child process is always restarted;

-  ``:temporary`` - the child process is never restarted (not even when
   the supervisor's strategy is ``:rest_for_one`` or ``:one_for_all``);

-  ``:transient`` - the child process is restarted only if it terminates
   abnormally, i.e. with another exit reason than ``:normal``,
   ``:shutdown`` or ``{:shutdown, term}``;

Shutdown values
^^^^^^^^^^^^^^^

The following shutdown values are supported:

-  ``:brutal_kill`` - the child process is unconditionally terminated
   using ``exit(child, :kill)``;

-  ``:infinity`` - if the child process is a supervisor, it is a
   mechanism to give the subtree enough time to shutdown. It can also be
   used with workers with care;

-  Finally, it can also be any integer meaning that the supervisor tells
   the child process to terminate by calling
   ``Process.exit(child, :shutdown)`` and then waits for an exit signal
   back. If no exit signal is received within the specified time (in
   miliseconds), the child process is unconditionally terminated using
   ``Process.exit(child, :kill)``;







Summary
-------

=========================== =
:elixir:func:`supervise/2`  Receives a list of children (workers or supervisors) to supervise and a set of options 

:elixir:func:`supervisor/3` Defines the given ``module`` as a supervisor which will be started with the given arguments 

:elixir:func:`worker/3`     Defines the given ``module`` as a worker which will be started with the given arguments 
=========================== =



Types
-----

.. elixir:type:: Supervisor.Spec.strategy/0

   :elixir:type:`strategy/0` :: :simple_one_for_one | :one_for_one | :one_for_all | :rest_for_one
   

   Supported strategies
   

.. elixir:type:: Supervisor.Spec.restart/0

   :elixir:type:`restart/0` :: :permanent | :transient | :temporary
   

   Supported restart values
   

.. elixir:type:: Supervisor.Spec.shutdown/0

   :elixir:type:`shutdown/0` :: :brutal_kill | :infinity | non_neg_integer
   

   Supported shutdown values
   

.. elixir:type:: Supervisor.Spec.worker/0

   :elixir:type:`worker/0` :: :worker | :supervisor
   

   Supported worker values
   

.. elixir:type:: Supervisor.Spec.modules/0

   :elixir:type:`modules/0` :: :dynamic | [module]
   

   Supported module values
   

.. elixir:type:: Supervisor.Spec.child_id/0

   :elixir:type:`child_id/0` :: term
   

   Supported id values
   

.. elixir:type:: Supervisor.Spec.spec/0

   :elixir:type:`spec/0` :: {:elixir:type:`child_id/0`, start_fun :: {module, atom, [term]}, :elixir:type:`restart/0`, :elixir:type:`shutdown/0`, :elixir:type:`worker/0`, :elixir:type:`modules/0`}
   

   The supervisor specification
   





Functions
---------

.. elixir:function:: Supervisor.Spec.supervise/2
   :sig: supervise(children, options)


   Specs:
   
 
   * supervise([:elixir:type:`spec/0`], strategy: :elixir:type:`strategy/0`, max_restarts: non_neg_integer, max_seconds: non_neg_integer) :: {:ok, tuple}
 

   
   Receives a list of children (workers or supervisors) to supervise and a
   set of options.
   
   Returns a tuple containing the supervisor specification.
   
   **Examples**
   
   ::
   
       supervise children, strategy: :one_for_one
   
   **Options**
   
   -  ``:strategy`` - the restart strategy option. It can be either
      ``:one_for_one``, ``:rest_for_one``, ``:one_for_all``, or
      ``:simple_one_for_one``. You can learn more about strategies in the
      :elixir:mod:`Supervisor` module docs;
   
   -  ``:max_restarts`` - the maximum amount of restarts allowed in a time
      frame. Defaults to 5;
   
   -  ``:max_seconds`` - the time frame in which ``:max_restarts`` applies.
      Defaults to 5;
   
   The ``:strategy`` option is required and by default maximum 5 restarts
   are allowed within 5 seconds. Please check the :elixir:mod:`Supervisor` module for
   a complete description of the available strategies.
   
   

.. elixir:function:: Supervisor.Spec.supervisor/3
   :sig: supervisor(module, args, options \\ [])


   Specs:
   
 
   * supervisor(module, [term], restart: :elixir:type:`restart/0`, shutdown: :elixir:type:`shutdown/0`, id: term, function: atom, modules: :elixir:type:`modules/0`) :: :elixir:type:`spec/0`
 

   
   Defines the given ``module`` as a supervisor which will be started with
   the given arguments.
   
   ::
   
       supervisor ExUnit.Runner, [], restart: :permanent
   
   By default, the function ``start_link`` is invoked on the given module.
   Overall, the default values for the options are:
   
   ::
   
       [id: module,
        function: :start_link,
        restart: :permanent,
        shutdown: :infinity,
        modules: [module]]
   
   Check :elixir:mod:`Supervisor.Spec` module docs for more information on the
   options.
   
   

.. elixir:function:: Supervisor.Spec.worker/3
   :sig: worker(module, args, options \\ [])


   Specs:
   
 
   * worker(module, [term], restart: :elixir:type:`restart/0`, shutdown: :elixir:type:`shutdown/0`, id: term, function: atom, modules: :elixir:type:`modules/0`) :: :elixir:type:`spec/0`
 

   
   Defines the given ``module`` as a worker which will be started with the
   given arguments.
   
   ::
   
       worker ExUnit.Runner, [], restart: :permanent
   
   By default, the function ``start_link`` is invoked on the given module.
   Overall, the default values for the options are:
   
   ::
   
       [id: module,
        function: :start_link,
        restart: :permanent,
        shutdown: 5000,
        modules: [module]]
   
   Check :elixir:mod:`Supervisor.Spec` module docs for more information on the
   options.
   
   







