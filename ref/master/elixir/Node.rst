Node
==============================================================

.. elixir:module:: Node

   :mtype: 

Overview
--------

Functions related to VM nodes.

Some of the functions in this module are inlined by the compiler,
similar to functions in the :elixir:mod:`Kernel` module and they are explicitly
marked in their docs as "inlined by the compiler". For more information
about inlined functions, check out the :elixir:mod:`Kernel` module.





Summary
-------

=========================== =
:elixir:func:`alive?/0`     Returns ``true`` if the local node is alive 

:elixir:func:`connect/1`    Establishes a connection to ``node`` 

:elixir:func:`disconnect/1` Forces the disconnection of a node 

:elixir:func:`get_cookie/0` Returns the magic cookie of the local node 

:elixir:func:`list/0`       Returns a list of all visible nodes in the system, excluding the local node 

:elixir:func:`list/1`       Returns a list of nodes according to argument given 

:elixir:func:`monitor/2`    Monitors the status of the node 

:elixir:func:`monitor/3`    Behaves as :elixir:func:`monitor/2` except that it allows an extra option to be given, namely ``:allow_passive_connect`` 

:elixir:func:`ping/1`       Tries to set up a connection to node 

:elixir:func:`self/0`       Returns the current node 

:elixir:func:`set_cookie/2` Sets the magic cookie of ``node`` to the atom ``cookie`` 

:elixir:func:`spawn/2`      Returns the pid of a new process started by the application of ``fun`` on ``node``. If ``node`` does not exist, a useless pid is returned 

:elixir:func:`spawn/3`      Returns the pid of a new process started by the application of ``fun`` on ``node`` 

:elixir:func:`spawn/4`      Returns the pid of a new process started by the application of ``module.function(args)`` on ``node`` 

:elixir:func:`spawn/5`      Returns the pid of a new process started by the application of ``module.function(args)`` on ``node`` 

:elixir:func:`spawn_link/2` Returns the pid of a new linked process started by the application of ``fun`` on ``node`` 

:elixir:func:`spawn_link/4` Returns the pid of a new linked process started by the application of ``module.function(args)`` on ``node`` 
=========================== =



Types
-----

.. elixir:type:: Node.t/0

   :elixir:type:`t/0` :: node
   





Functions
---------

.. elixir:function:: Node.alive?/0
   :sig: alive?()


   Specs:
   
 
   * alive? :: boolean
 

   
   Returns ``true`` if the local node is alive.
   
   That is, if the node can be part of a distributed system.
   
   

.. elixir:function:: Node.connect/1
   :sig: connect(node)


   Specs:
   
 
   * connect(:elixir:type:`t/0`) :: boolean | :ignored
 

   
   Establishes a connection to ``node``.
   
   Returns ``true`` if successful, ``false`` if not, and the atom
   ``:ignored`` if the local node is not alive.
   
   See http://erlang.org/doc/man/net\_kernel.html#connect\_node-1 for more
   info.
   
   

.. elixir:function:: Node.disconnect/1
   :sig: disconnect(node)


   Specs:
   
 
   * disconnect(:elixir:type:`t/0`) :: boolean | :ignored
 

   
   Forces the disconnection of a node.
   
   This will appear to the ``node`` as if the local node has crashed. This
   function is mainly used in the Erlang network authentication protocols.
   Returns ``true`` if disconnection succeeds, otherwise ``false``. If the
   local node is not alive, the function returns ``:ignored``.
   
   See http://www.erlang.org/doc/man/erlang.html#disconnect\_node-1 for
   more info.
   
   

.. elixir:function:: Node.get_cookie/0
   :sig: get_cookie()


   
   Returns the magic cookie of the local node.
   
   Returns the cookie if the node is alive, otherwise ``:nocookie``.
   
   

.. elixir:function:: Node.list/0
   :sig: list()


   Specs:
   
 
   * list :: [:elixir:type:`t/0`]
 

   
   Returns a list of all visible nodes in the system, excluding the local
   node.
   
   Same as ``list(:visible)``.
   
   

.. elixir:function:: Node.list/1
   :sig: list(args)


   Specs:
   
 
   * list(state | [state]) :: [:elixir:type:`t/0`]
 

   
   Returns a list of nodes according to argument given.
   
   The result returned when the argument is a list, is the list of nodes
   satisfying the disjunction(s) of the list elements.
   
   See http://www.erlang.org/doc/man/erlang.html#nodes-1 for more info.
   
   

.. elixir:function:: Node.monitor/2
   :sig: monitor(node, flag)


   Specs:
   
 
   * monitor(:elixir:type:`t/0`, boolean) :: true
 

   
   Monitors the status of the node.
   
   If ``flag`` is ``true``, monitoring is turned on. If ``flag`` is
   ``false``, monitoring is turned off.
   
   See http://www.erlang.org/doc/man/erlang.html#monitor\_node-2 for more
   info.
   
   

.. elixir:function:: Node.monitor/3
   :sig: monitor(node, flag, options)


   Specs:
   
 
   * monitor(:elixir:type:`t/0`, boolean, [:allow_passive_connect]) :: true
 

   
   Behaves as :elixir:func:`monitor/2` except that it allows an extra option to be
   given, namely ``:allow_passive_connect``.
   
   See http://www.erlang.org/doc/man/erlang.html#monitor\_node-3 for more
   info.
   
   

.. elixir:function:: Node.ping/1
   :sig: ping(node)


   Specs:
   
 
   * ping(:elixir:type:`t/0`) :: :pong | :pang
 

   
   Tries to set up a connection to node.
   
   Returns ``:pang`` if it fails, or ``:pong`` if it is successful.
   
   **Examples**
   
   ::
   
       iex> Node.ping(:unknown_node)
       :pang
   
   
   

.. elixir:function:: Node.self/0
   :sig: self()


   Specs:
   
 
   * self :: :elixir:type:`t/0`
 

   
   Returns the current node.
   
   It returns the same as the built-in ``node()``.
   
   

.. elixir:function:: Node.set_cookie/2
   :sig: set_cookie(node \\ Node.self(), cookie)


   
   Sets the magic cookie of ``node`` to the atom ``cookie``.
   
   The default node is ``Node.self``, the local node. If ``node`` is the
   local node, the function also sets the cookie of all other unknown nodes
   to ``cookie``.
   
   This function will raise :elixir:mod:`FunctionClauseError` if the given ``node``
   is not alive.
   
   

.. elixir:function:: Node.spawn/2
   :sig: spawn(node, fun)


   Specs:
   
 
   * spawn(:elixir:type:`t/0`, (() -> any)) :: pid
 

   
   Returns the pid of a new process started by the application of ``fun``
   on ``node``. If ``node`` does not exist, a useless pid is returned.
   
   Check http://www.erlang.org/doc/man/erlang.html#spawn-2 for the list of
   available options.
   
   Inlined by the compiler.
   
   

.. elixir:function:: Node.spawn/3
   :sig: spawn(node, fun, opts)


   Specs:
   
 
   * spawn(:elixir:type:`t/0`, (() -> any), :elixir:type:`Process.spawn_opts/0`) :: pid | {pid, reference}
 

   
   Returns the pid of a new process started by the application of ``fun``
   on ``node``.
   
   If ``node`` does not exist, a useless pid is returned. Check
   http://www.erlang.org/doc/man/erlang.html#spawn\_opt-3 for the list of
   available options.
   
   Inlined by the compiler.
   
   

.. elixir:function:: Node.spawn/4
   :sig: spawn(node, module, fun, args)


   Specs:
   
 
   * spawn(:elixir:type:`t/0`, module, atom, [any]) :: pid
 

   
   Returns the pid of a new process started by the application of
   ``module.function(args)`` on ``node``.
   
   If ``node`` does not exist, a useless pid is returned. Check
   http://www.erlang.org/doc/man/erlang.html#spawn-4 for the list of
   available options.
   
   Inlined by the compiler.
   
   

.. elixir:function:: Node.spawn/5
   :sig: spawn(node, module, fun, args, opts)


   Specs:
   
 
   * spawn(:elixir:type:`t/0`, module, atom, [any], :elixir:type:`Process.spawn_opts/0`) :: pid | {pid, reference}
 

   
   Returns the pid of a new process started by the application of
   ``module.function(args)`` on ``node``.
   
   If ``node`` does not exist, a useless pid is returned. Check
   http://www.erlang.org/doc/man/erlang.html#spawn\_opt-5 for the list of
   available options.
   
   Inlined by the compiler.
   
   

.. elixir:function:: Node.spawn_link/2
   :sig: spawn_link(node, fun)


   Specs:
   
 
   * spawn_link(:elixir:type:`t/0`, (() -> any)) :: pid
 

   
   Returns the pid of a new linked process started by the application of
   ``fun`` on ``node``.
   
   A link is created between the calling process and the new process,
   atomically. If ``node`` does not exist, a useless pid is returned (and
   due to the link, an exit signal with exit reason ``:noconnection`` will
   be received).
   
   Inlined by the compiler.
   
   

.. elixir:function:: Node.spawn_link/4
   :sig: spawn_link(node, module, fun, args)


   Specs:
   
 
   * spawn_link(:elixir:type:`t/0`, module, atom, [any]) :: pid
 

   
   Returns the pid of a new linked process started by the application of
   ``module.function(args)`` on ``node``.
   
   A link is created between the calling process and the new process,
   atomically. If ``node`` does not exist, a useless pid is returned (and
   due to the link, an exit signal with exit reason ``:noconnection`` will
   be received).
   
   Inlined by the compiler.
   
   







