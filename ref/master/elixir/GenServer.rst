GenServer
==============================================================

.. elixir:module:: GenServer

   :mtype: 

Overview
--------

A behaviour module for implementing the server of a client-server
relation.

A GenServer is a process as any other Elixir process and it can be used
to keep state, execute code asynchronously and so on. The advantage of
using a generic server process (GenServer) implemented using this module
is that it will have a standard set of interface functions and include
functionality for tracing and error reporting. It will also fit into a
supervision tree.

Example
~~~~~~~

The GenServer behaviour abstracts the common client-server interaction.
Developer are only required to implement the callbacks and functionality
they are interested in.

Let's start with a code example and then explore the available
callbacks. Imagine we want a GenServer that works like a stack, allowing
us to push and pop items:

::

    defmodule Stack do
      use GenServer

      # Callbacks

      def handle_call(:pop, _from, [h|t]) do
        {:reply, h, t}
      end

      def handle_cast({:push, item}, state) do
        {:noreply, [item|state]}
      end
    end

    # Start the server
    {:ok, pid} = GenServer.start_link(Stack, [:hello])

    # This is the client
    GenServer.call(pid, :pop)
    #=> :hello

    GenServer.cast(pid, {:push, :world})
    #=> :ok

    GenServer.call(pid, :pop)
    #=> :world

We start our ``Stack`` by calling ```start_link/3`` <#start_link/3>`__,
passing the module with the server implementation and its initial
argument (a list representing the stack containing the item ``:hello``).
We can primarily interact with the server by sending two types of
messages. **call** messages expect a reply from the server (and are
therefore synchronous) while **cast** messages do not.

Every time you do a ```GenServer.call/3`` <GenServer.html#call/3>`__,
the client will send a message that must be handled by the
``handle_call/3`` callback in the GenServer. A ```cast/2`` <#cast/2>`__
message must be handled by ``handle_cast/2``.

Callbacks
~~~~~~~~~

There are 6 callbacks required to be implemented in a
```GenServer`` <GenServer.html>`__. By adding ``use GenServer`` to your
module, Elixir will automatically define all 6 callbacks for you,
leaving it up to you to implement the ones you want to customize. The
callbacks are:

-  ``init(args)`` - invoked when the server is started

It must return:

-  ``{:ok, state}``
-  ``{:ok, state, timeout}``
-  ``:ignore``
-  ``{:stop, reason}``

-  ``handle_call(msg, {from, ref}, state)`` and
   ``handle_cast(msg, state)`` - invoked to handle call (sync) and cast
   (async) messages.

It must return:

-  ``{:reply, reply, new_state}``
-  ``{:reply, reply, new_state, timeout}``
-  ``{:reply, reply, new_state, :hibernate}``
-  ``{:noreply, new_state}``
-  ``{:noreply, new_state, timeout}``
-  ``{:noreply, new_state, :hibernate}``
-  ``{:stop, reason, new_state}``
-  ``{:stop, reason, reply, new_state}``

-  ``handle_info(msg, state)`` - invoked to handle all other messages
   which are received by the process.

It must return:

-  ``{:noreply, state}``
-  ``{:noreply, state, timeout}``
-  ``{:stop, reason, state}``

-  ``terminate(reason, state)`` - called when the server is about to
   terminate, useful for cleaning up. It must return ``:ok``

-  ``code_change(old_vsn, state, extra)`` - called when the application
   code is being upgraded live (hot code swapping).

It must return:

-  ``{:ok, new_state}``
-  ``{:error, reason}``

Name Registration
~~~~~~~~~~~~~~~~~

Both ```start_link/3`` <#start_link/3>`__ and ```start/3`` <#start/3>`__
support the ```GenServer`` <GenServer.html>`__ to register a name on
start via the ``:name`` option. Registered names are also automatically
cleaned up on termination. The supported values are:

-  an atom - the GenServer is registered locally with the given name
   using ```Process.register/2`` <Process.html#register/2>`__;

-  ``{:global, term}``- the GenServer is registered globally with the
   given term using the functions in the ``:global`` module;

-  ``{:via, module, term}`` - the GenServer is registered with the given
   mechanism and name. The ``:via`` option expects a module name to
   control the registration mechanism alongside a name which can be any
   term;

For example, we could start and register our Stack server locally as
follows:

::

    # Start the server and register it locally with name MyStack
    {:ok, _} = GenServer.start_link(Stack, [:hello], name: MyStack)

    # Now messages can be sent directly to MyStack
    GenServer.call(MyStack, :pop) #=> :hello

Once the server is started, the remaining functions in this module
(```call/3`` <#call/3>`__, ```cast/2`` <#cast/2>`__, and friends) will
also accept an atom, or any ``:global`` or ``:via`` tuples. In general,
the following formats are supported:

-  a ``pid``
-  an ``atom`` if the server is locally registered
-  ``{atom, node}`` if the server is locally registered at another node
-  ``{:global, term}`` if the server is globally registered
-  ``{:via, module, name}`` if the server is registered through an
   alternative registry

Client / Server APIs
~~~~~~~~~~~~~~~~~~~~

Although in the example above we have used
```GenServer.start_link/3`` <GenServer.html#start_link/3>`__ and friends
to directly start and communicate with the server, most of the time we
don't call the ```GenServer`` <GenServer.html>`__ functions directly.
Instead, we wrap the calls in new functions representing the public API
of the server.

Here is a better implementation of our Stack module:

::

    defmodule Stack do
      use GenServer

      # Client

      def start_link(default) do
        GenServer.start_link(__MODULE__, default)
      end

      def push(pid, item) do
        GenServer.cast(pid, {:push, item})
      end

      def pop(pid) do
        GenServer.call(pid, :pop)
      end

      # Server (callbacks)

      def handle_call(:pop, _from, [h|t]) do
        {:reply, h, t}
      end

      def handle_call(request, from, state) do
        # Call the default implementation from GenServer
        super(request, from, state)
      end

      def handle_cast({:push, item}, state) do
        {:noreply, [item|state]}
      end

      def handle_cast(request, state) do
        super(request, state)
      end
    end

In practice, it is common to have both server and client functions in
the same module. If the server and/or client implementations are growing
complex, you may want to have them in different modules.

Learn more
~~~~~~~~~~

If you wish to find out more about gen servers, Elixir getting started
guides provide a tutorial-like introduction. The documentation and links
in Erlang can also provide extra insight.

-  http://elixir-lang.org/getting\_started/mix/1.html
-  http://www.erlang.org/doc/man/gen\_server.html
-  http://www.erlang.org/doc/design\_principles/gen\_server\_concepts.html
-  http://learnyousomeerlang.com/clients-and-servers






Summary
-------

=========================== =
:elixir:func:`abcast/3`     Casts all servers locally registered as ``name`` at the specified nodes 

:elixir:func:`call/3`       Makes a synchronous call to the ``server`` and waits for its reply 

:elixir:func:`cast/2`       Sends an asynchronous request to the ``server`` 

:elixir:func:`multi_call/4` Calls all servers locally registered as ``name`` at the specified ``nodes`` 

:elixir:func:`reply/2`      Replies to a client 

:elixir:func:`start/3`      Starts a ```GenServer`` <GenServer.html>`__ process without links (outside of a supervision tree) 

:elixir:func:`start_link/3` Starts a ```GenServer`` <GenServer.html>`__ process linked to the current process 
=========================== =



Types
-----

.. elixir:type:: GenServer.on_start/0

   :elixir:type:`on_start/0` :: {:ok, pid} | :ignore | {:error, {:already_started, pid} | term}
   

   Return values of ``start*`` functions
   

.. elixir:type:: GenServer.name/0

   :elixir:type:`name/0` :: atom | {:global, term} | {:via, module, term}
   

   The GenServer name
   

.. elixir:type:: GenServer.options/0

   :elixir:type:`options/0` :: [debug: :elixir:type:`debug/0`, name: :elixir:type:`name/0`, timeout: timeout, spawn_opt: :elixir:type:`Process.spawn_opt/0`]
   

   Options used by the ``start*`` functions
   

.. elixir:type:: GenServer.debug/0

   :elixir:type:`debug/0` :: [:trace | :log | :statistics | {:log_to_file, :elixir:type:`Path.t/0`}]
   

   debug options supported by the ``start*`` functions
   

.. elixir:type:: GenServer.server/0

   :elixir:type:`server/0` :: pid | :elixir:type:`name/0` | {atom, node}
   

   The server reference
   





Functions
---------

.. elixir:function:: GenServer.abcast/3
   :sig: abcast(nodes \\ nodes(), name, request)


   Specs:
   
 
   * abcast([node], name :: atom, term) :: :abcast
 

   
   Casts all servers locally registered as ``name`` at the specified nodes.
   
   The function returns immediately and ignores nodes that do not exist, or
   where the server name does not exist.
   
   See ```multi_call/4`` <#multi_call/4>`__ for more information.
   
   

.. elixir:function:: GenServer.call/3
   :sig: call(server, request, timeout \\ 5000)


   Specs:
   
 
   * call(:elixir:type:`server/0`, term, timeout) :: term
 

   
   Makes a synchronous call to the ``server`` and waits for its reply.
   
   The client sends the given ``request`` to the server and waits until a
   reply arrives or a timeout occurs. ``handle_call/3`` will be called on
   the server to handle the request.
   
   The server can be any of the values described in the
   ``Name Registration`` section of the module documentation.
   
   **Timeouts**
   
   The ``timeout`` is an integer greater than zero which specifies how many
   milliseconds to wait for a reply, or the atom ``:infinity`` to wait
   indefinitely. The default value is 5000. If no reply is received within
   the specified time, the function call fails. If the caller catches the
   failure and continues running, and the server is just late with the
   reply, it may arrive at any time later into the caller's message queue.
   The caller must in this case be prepared for this and discard any such
   garbage messages that are two element tuples with a reference as the
   first element.
   
   

.. elixir:function:: GenServer.cast/2
   :sig: cast(server, request)


   Specs:
   
 
   * cast(:elixir:type:`server/0`, term) :: :ok
 

   
   Sends an asynchronous request to the ``server``.
   
   This function returns ``:ok`` immediately, regardless of whether the
   destination node or server does exists. ``handle_cast/2`` will be called
   on the server to handle the request.
   
   

.. elixir:function:: GenServer.multi_call/4
   :sig: multi_call(nodes \\ nodes(), name, request, timeout \\ :infinity)


   Specs:
   
 
   * multi_call([node], name :: atom, term, timeout) :: {replies :: [{node, term}], bad_nodes :: [node]}
 

   
   Calls all servers locally registered as ``name`` at the specified
   ``nodes``.
   
   The ``request`` is first sent to every node and then we wait for the
   replies. This function returns a tuple containing the node and its reply
   as first element and all bad nodes as second element. The bad nodes is a
   list of nodes that either did not exist, or where a server with the
   given ``name`` did not exist or did not reply.
   
   Nodes is a list of node names to which the request is sent. The default
   value is the list of all known nodes.
   
   To avoid that late answers (after the timeout) pollute the caller's
   message queue, a middleman process is used to do the actual calls. Late
   answers will then be discarded when they arrive to a terminated process.
   
   

.. elixir:function:: GenServer.reply/2
   :sig: reply(client, reply)


   Specs:
   
 
   * reply({pid, reference}, term) :: :ok
 

   
   Replies to a client.
   
   This function can be used by a server to explicitly send a reply to a
   client that called ```call/3`` <#call/3>`__ or
   ```multi_call/4`` <#multi_call/4>`__. When the reply cannot be defined
   in the return value of ``handle_call/3``.
   
   The ``client`` must be the ``from`` argument (the second argument)
   received in ``handle_call/3`` callbacks. Reply is an arbitrary term
   which will be given back to the client as the return value of the call.
   
   This function always returns ``:ok``.
   
   

.. elixir:function:: GenServer.start/3
   :sig: start(module, args, options \\ [])


   Specs:
   
 
   * start(module, any, :elixir:type:`options/0`) :: :elixir:type:`on_start/0`
 

   
   Starts a ```GenServer`` <GenServer.html>`__ process without links
   (outside of a supervision tree).
   
   See ```start_link/3`` <#start_link/3>`__ for more information.
   
   

.. elixir:function:: GenServer.start_link/3
   :sig: start_link(module, args, options \\ [])


   Specs:
   
 
   * start_link(module, any, :elixir:type:`options/0`) :: :elixir:type:`on_start/0`
 

   
   Starts a ```GenServer`` <GenServer.html>`__ process linked to the
   current process.
   
   This is often used to start the ```GenServer`` <GenServer.html>`__ as
   part of a supervision tree.
   
   Once the server is started, it calls the ``init/1`` function in the
   given ``module`` passing the given ``args`` to initialize it. To ensure
   a synchronized start-up procedure, this function does not return until
   ``init/1`` has returned.
   
   **Options**
   
   The ``:name`` option is used for name registration as described in the
   module documentation. If the option ``:timeout`` option is present, the
   server is allowed to spend the given milliseconds initializing or it
   will be terminated and the start function will return
   ``{:error, :timeout}``.
   
   If the ``:debug`` option is present, the corresponding function in the
   ```:sys`` module <http://www.erlang.org/doc/man/sys.html>`__ will be
   invoked.
   
   If the ``:spawn_opt`` option is present, its value will be passed as
   options to the underlying process as in
   ```Process.spawn/4`` <Process.html#spawn/4>`__.
   
   **Return values**
   
   If the server is successfully created and initialized, the function
   returns ``{:ok, pid}``, where pid is the pid of the server. If there
   already exists a process with the specified server name, the function
   returns ``{:error, {:already_started, pid}}`` with the pid of that
   process.
   
   If the ``init/1`` callback fails with ``reason``, the function returns
   ``{:error, reason}``. Otherwise, if it returns ``{:stop, reason}`` or
   ``:ignore``, the process is terminated and the function returns
   ``{:error, reason}`` or ``:ignore``, respectively.
   
   







