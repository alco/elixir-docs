GenEvent
==============================================================

.. elixir:module:: GenEvent

   :mtype: 

Overview
--------

A behaviour module for implementing event handling functionality.

The event handling model consists of a generic event manager process
with an arbitrary number of event handlers which are added and deleted
dynamically.

An event manager implemented using this module will have a standard set
of interface functions and include functionality for tracing and error
reporting. It will also fit into an supervision tree.

Example
~~~~~~~

There are many use cases for event handlers. For example, a logging
system can be built using event handlers where which log message is an
event and different event handlers can be plugged to handle the log
messages. One handler may print error messages on the terminal, another
can write it to a file, while a third one can keep the messages in
memory (like a buffer) until they are read.

As an example, let's have a GenEvent that accumulates messages until
they are collected by an explicit call.

::

    defmodule LoggerHandler do
      use GenEvent

      # Callbacks

      def handle_event({:log, x}, messages) do
        {:ok, [x|messages]}
      end

      def handle_call(:messages, messages) do
        {:ok, Enum.reverse(messages), []}
      end
    end

    {:ok, pid} = GenEvent.start_link()

    GenEvent.add_handler(pid, LoggerHandler, [])
    #=> :ok

    GenEvent.notify(pid, {:log, 1})
    #=> :ok

    GenEvent.notify(pid, {:log, 2})
    #=> :ok

    GenEvent.call(pid, LoggerHandler, :messages)
    #=> [1, 2]

    GenEvent.call(pid, LoggerHandler, :messages)
    #=> []

We start a new event manager by calling ``GenEvent.start_link/0``.
Notifications can be sent to the event manager which will then invoke
``handle_event/0`` for each registered handler.

We can add new handlers with :elixir:func:`add_handler/4`. Calls can also be made
to specific handlers by using ``call/3``.

Callbacks
~~~~~~~~~

There are 6 callbacks required to be implemented in a :elixir:mod:`GenEvent`. By
adding ``use GenEvent`` to your module, Elixir will automatically define
all 6 callbacks for you, leaving it up to you to implement the ones you
want to customize. The callbacks are:

-  ``init(args)`` - invoked when the event handler is added

It must return:

-  ``{:ok, state}``
-  ``{:ok, state, :hibernate}``
-  ``{:error, reason}``

-  ``handle_event(msg, state)`` - invoked whenever an event is sent via
   :elixir:func:`notify/2` or :elixir:func:`sync_notify/2`.

It must return:

-  ``{:ok, new_state}``
-  ``{:ok, new_state, :hibernate}``
-  ``{:swap_handler, args1, new_state, handler2, args2}``
-  ``:remove_handler``

-  ``handle_call(msg, state)`` - invoked when a ``call/3`` is done to a
   specific handler.

It must return:

-  ``{:ok, reply, new_state}``
-  ``{:ok, reply, new_state, :hibernate}``
-  ``{:swap_handler, reply, args1, new_state, handler2, args2}``
-  ``{:remove_handler, reply}``

-  ``handle_info(msg, state)`` - invoked to handle all other messages
   which are received by the process. Must return the same values as
   ``handle_event/2``;

It must return:

-  ``{:noreply, state}``
-  ``{:noreply, state, timeout}``
-  ``{:stop, reason, state}``

-  ``terminate(reason, state)`` - called when the event handler is
   removed or the event manager is terminating. It can return any term.

-  ``code_change(old_vsn, state, extra)`` - called when the application
   code is being upgraded live (hot code swapping).

It must return:

-  ``{:ok, new_state}``

Name Registration
~~~~~~~~~~~~~~~~~

A GenEvent is bound to the same name registration rules as a
:elixir:mod:`GenServer`. Read more about it in the :elixir:mod:`GenServer` docs.

Streaming
~~~~~~~~~

:elixir:mod:`GenEvent`\ s can be streamed from and streamed with the help of
:elixir:func:`stream/2`. Here are some examples:

::

    stream = GenEvent.stream(pid)

    # Take the next 10 events
    Enum.take(stream, 10)

    # Print all remaining events
    for event <- stream do
      IO.inspect event
    end

A stream may also be given an id, which allows all streams with the
given id to be cancelled at any moment via :elixir:func:`cancel_streams/1`.

Learn more
~~~~~~~~~~

If you wish to find out more about gen events, Elixir getting started
guides provide a tutorial-like introduction. The documentation and links
in Erlang can also provide extra insight.

-  http://elixir-lang.org/getting\_started/mix/1.html
-  http://www.erlang.org/doc/man/gen\_event.html
-  http://learnyousomeerlang.com/event-handlers






Summary
-------

=============================== =
:elixir:func:`__struct__/0`     Defines a :elixir:mod:`GenEvent` stream 

:elixir:func:`add_handler/4`    Adds a new event handler to the event ``manager`` 

:elixir:func:`call/4`           Makes a synchronous call to the event ``handler`` installed in ``manager`` 

:elixir:func:`cancel_streams/1` Cancels all streams currently running with the given ``:id`` 

:elixir:func:`notify/2`         Sends an event notification to the event ``manager`` 

:elixir:func:`remove_handler/3` Removes an event handler from the event ``manager`` 

:elixir:func:`start/1`          Starts an event manager process without links (outside of a supervision tree) 

:elixir:func:`start_link/1`     Starts an event manager linked to the current process 

:elixir:func:`stop/1`           Terminates the event ``manager`` 

:elixir:func:`stream/2`         Returns a stream that consumes and notifies events to the ``manager`` 

:elixir:func:`swap_handler/6`   Replaces an old event handler with a new one in the event ``manager`` 

:elixir:func:`sync_notify/2`    Sends a sync event notification to the event ``manager`` 

:elixir:func:`which_handlers/1` Returns a list of all event handlers installed in the ``manager`` 
=============================== =



Types
-----

.. elixir:type:: GenEvent.on_start/0

   :elixir:type:`on_start/0` :: {:ok, pid} | {:error, {:already_started, pid}}
   

   Return values of ``start*`` functions
   

.. elixir:type:: GenEvent.name/0

   :elixir:type:`name/0` :: atom | {:global, term} | {:via, module, term}
   

   The GenEvent manager name
   

.. elixir:type:: GenEvent.options/0

   :elixir:type:`options/0` :: [{:name, :elixir:type:`name/0`}]
   

   Options used by the ``start*`` functions
   

.. elixir:type:: GenEvent.manager/0

   :elixir:type:`manager/0` :: pid | :elixir:type:`name/0` | {atom, node}
   

   The event manager reference
   

.. elixir:type:: GenEvent.handler/0

   :elixir:type:`handler/0` :: module | {module, term}
   

   Supported values for new handlers
   

.. elixir:type:: GenEvent.t/0

   :elixir:type:`t/0` :: %GenEvent{manager: term, id: term, timeout: term, duration: term}
   





Functions
---------

.. elixir:function:: GenEvent.__struct__/0
   :sig: __struct__()


   Specs:
   
 
   * __struct__ :: :elixir:type:`t/0`
 

   
   Defines a :elixir:mod:`GenEvent` stream.
   
   This is a struct returned by :elixir:func:`stream/2`. The struct is public and
   contains the following fields:
   
   -  ``:manager`` - the manager reference given to :elixir:func:`GenEvent.stream/2`
   -  ``:id`` - the event stream id for cancellation
   -  ``:timeout`` - the timeout in between events, defaults to
      ``:infinity``
   -  ``:duration`` - the duration of the subscription, defaults to
      ``:infinity``
   
   
   

.. elixir:function:: GenEvent.add_handler/4
   :sig: add_handler(manager, handler, args, options \\ [])


   Specs:
   
 
   * add_handler(:elixir:type:`manager/0`, :elixir:type:`handler/0`, term, [{:link, boolean}]) :: :ok | {:EXIT, term} | {:error, term}
 

   
   Adds a new event handler to the event ``manager``.
   
   The event manager will call the ``init/1`` callback with ``args`` to
   initiate the event handler and its internal state.
   
   If ``init/1`` returns a correct value indicating successful completion,
   the event manager adds the event handler and this function returns
   ``:ok``. If the callback fails with ``reason`` or returns
   ``{:error, reason}``, the event handler is ignored and this function
   returns ``{:EXIT, reason}`` or ``{:error, reason}``, respectively.
   
   **Linked handlers**
   
   When adding a handler, a ``:link`` option with value ``true`` can be
   given. This means the event handler and the calling process are now
   linked.
   
   If the calling process later terminates with ``reason``, the event
   manager will delete the event handler by calling the ``terminate/2``
   callback with ``{:stop, reason}`` as argument. If the event handler
   later is deleted, the event manager sends a message
   ``{:gen_event_EXIT, handler, reason}`` to the calling process. Reason is
   one of the following:
   
   -  ``:normal`` - if the event handler has been removed due to a call to
      :elixir:func:`remove_handler/3`, or ``:remove_handler`` has been returned by a
      callback function;
   
   -  ``:shutdown`` - if the event handler has been removed because the
      event manager is terminating;
   
   -  ``{:swapped, new_handler, pid}`` - if the process pid has replaced
      the event handler by another;
   
   -  a term - if the event handler is removed due to an error. Which term
      depends on the error;
   
   
   
   

.. elixir:function:: GenEvent.call/4
   :sig: call(manager, handler, request, timeout \\ 5000)


   Specs:
   
 
   * call(:elixir:type:`manager/0`, :elixir:type:`handler/0`, term, timeout) :: term | {:error, term}
 

   
   Makes a synchronous call to the event ``handler`` installed in
   ``manager``.
   
   The given ``request`` is sent and the caller waits until a reply arrives
   or a timeout occurs. The event manager will call ``handle_call/2`` to
   handle the request.
   
   The return value ``reply`` is defined in the return value of
   ``handle_call/2``. If the specified event handler is not installed, the
   function returns ``{:error, :bad_module}``.
   
   

.. elixir:function:: GenEvent.cancel_streams/1
   :sig: cancel_streams(genevent)


   Specs:
   
 
   * cancel_streams(:elixir:type:`t/0`) :: :ok
 

   
   Cancels all streams currently running with the given ``:id``.
   
   In order for a stream to be cancelled, an ``:id`` must be passed when
   the stream is created via :elixir:func:`stream/2`. Passing a stream without an id
   leads to an argument error.
   
   

.. elixir:function:: GenEvent.notify/2
   :sig: notify(manager, event)


   Specs:
   
 
   * notify(:elixir:type:`manager/0`, term) :: :ok
 

   
   Sends an event notification to the event ``manager``.
   
   The event manager will call ``handle_event/2`` for each installed event
   handler.
   
   ``notify`` is asynchronous and will return immediately after the
   notification is sent. ``notify`` will not fail even if the specified
   event manager does not exist, unless it is specified as ``name`` (atom).
   
   

.. elixir:function:: GenEvent.remove_handler/3
   :sig: remove_handler(manager, handler, args)


   Specs:
   
 
   * remove_handler(:elixir:type:`manager/0`, :elixir:type:`handler/0`, term) :: term | {:error, term}
 

   
   Removes an event handler from the event ``manager``.
   
   The event manager will call ``terminate/2`` to terminate the event
   handler and return the callback value. If the specified event handler is
   not installed, the function returns ``{:error, :module_not_found}``.
   
   

.. elixir:function:: GenEvent.start/1
   :sig: start(options \\ [])


   Specs:
   
 
   * start(:elixir:type:`options/0`) :: :elixir:type:`on_start/0`
 

   
   Starts an event manager process without links (outside of a supervision
   tree).
   
   See :elixir:func:`start_link/1` for more information.
   
   

.. elixir:function:: GenEvent.start_link/1
   :sig: start_link(options \\ [])


   Specs:
   
 
   * start_link(:elixir:type:`options/0`) :: :elixir:type:`on_start/0`
 

   
   Starts an event manager linked to the current process.
   
   This is often used to start the :elixir:mod:`GenEvent` as part of a supervision
   tree.
   
   It accepts the ``:name`` option which is described under the
   ``Name Registration`` section in the :elixir:mod:`GenServer` module docs.
   
   If the event manager is successfully created and initialized, the
   function returns ``{:ok, pid}``, where pid is the pid of the server. If
   there already exists a process with the specified server name, the
   function returns ``{:error, {:already_started, pid}}`` with the pid of
   that process.
   
   

.. elixir:function:: GenEvent.stop/1
   :sig: stop(manager)


   Specs:
   
 
   * stop(:elixir:type:`manager/0`) :: :ok
 

   
   Terminates the event ``manager``.
   
   Before terminating, the event manager will call
   ``terminate(:stop, ...)`` for each installed event handler.
   
   

.. elixir:function:: GenEvent.stream/2
   :sig: stream(manager, options \\ [])


   
   Returns a stream that consumes and notifies events to the ``manager``.
   
   The stream is a :elixir:mod:`GenEvent` struct that implements the :elixir:mod:`Enumerable`
   protocol. The supported options are:
   
   -  ``:id`` - an id to identify all live stream instances. When an
      ``:id`` is given, existing streams can be called with via
      ``cancel_streams``;
   -  ``:timeout`` (Enumerable) - raises if no event arrives in X
      milliseconds;
   -  ``:duration`` (Enumerable) - only consume events during the X
      milliseconds from the streaming start;
   
   
   

.. elixir:function:: GenEvent.swap_handler/6
   :sig: swap_handler(manager, handler1, args1, handler2, args2, options \\ [])


   Specs:
   
 
   * swap_handler(:elixir:type:`manager/0`, :elixir:type:`handler/0`, term, :elixir:type:`handler/0`, term, [{:link, boolean}]) :: :ok | {:error, term}
 

   
   Replaces an old event handler with a new one in the event ``manager``.
   
   First, the old event handler is deleted by calling ``terminate/2`` with
   the given ``args1`` and collects the return value. Then the new event
   handler is added and initiated by calling
   ``init({args2, term}), where term is the return value of calling``\ terminate/2\`
   in the old handler. This makes it possible to transfer information from
   one handler to another.
   
   The new handler will be added even if the specified old event handler is
   not installed in which case ``term = :error`` or if the handler fails to
   terminate with a given reason.
   
   If there was a linked connection between handler1 and a process pid,
   there will be a link connection between handler2 and pid instead. A new
   link in between the caller process and the new handler can also be set
   with by giving ``link: true`` as option. See :elixir:func:`add_handler/4` for more
   information.
   
   If ``init/1`` in the second handler returns a correct value, this
   function returns ``:ok``.
   
   

.. elixir:function:: GenEvent.sync_notify/2
   :sig: sync_notify(manager, event)


   Specs:
   
 
   * sync_notify(:elixir:type:`manager/0`, term) :: :ok
 

   
   Sends a sync event notification to the event ``manager``.
   
   In other words, this function only returns ``:ok`` after the event
   manager invokes the ``handle_event/2`` on each installed event handler.
   
   See :elixir:func:`notify/2` for more info.
   
   

.. elixir:function:: GenEvent.which_handlers/1
   :sig: which_handlers(manager)


   Specs:
   
 
   * which_handlers(:elixir:type:`manager/0`) :: [:elixir:type:`handler/0`]
 

   
   Returns a list of all event handlers installed in the ``manager``.
   
   







