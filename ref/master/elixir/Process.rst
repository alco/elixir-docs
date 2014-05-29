Process
==============================================================

.. elixir:module:: Process

   :mtype: 

Overview
--------

Conveniences for working with processes and the process dictionary.

Besides the functions available in this module, the
```Kernel`` <Kernel.html>`__ module exposes and auto-imports some basic
functionality related to processes available through the functions:

-  ```Kernel.spawn/1`` <Kernel.html#spawn/1>`__ and
   ```Kernel.spawn/3`` <Kernel.html#spawn/3>`__
-  ```Kernel.spawn_link/1`` <Kernel.html#spawn_link/1>`__ and
   ```Kernel.spawn_link/3`` <Kernel.html#spawn_link/3>`__
-  ```Kernel.spawn_monitor/1`` <Kernel.html#spawn_monitor/1>`__ and
   ```Kernel.spawn_monitor/3`` <Kernel.html#spawn_monitor/3>`__
-  ```Kernel.self/0`` <Kernel.html#self/0>`__
-  ```Kernel.send/2`` <Kernel.html#send/2>`__






Summary
-------

============================= =
:elixir:func:`alive?/1`       Returns true if the process exists and is alive, that is, is not exiting and has not exited. Otherwise, returns false 

:elixir:func:`delete/1`       Deletes the given key from the dictionary 

:elixir:func:`demonitor/2`    If monitor\_ref is a reference which the calling process obtained by calling monitor/1, this monitoring is turned off. If the monitoring is already turned off, nothing happens 

:elixir:func:`exit/2`         Sends an exit signal with the given reason to the pid 

:elixir:func:`flag/2`         Sets certain flags for the process which calls this function. Returns the old value of the flag 

:elixir:func:`flag/3`         Sets certain flags for the process Pid, in the same manner as flag/2. Returns the old value of the flag. The allowed values for Flag are only a subset of those allowed in flag/2, namely: save\_calls 

:elixir:func:`get/0`          Returns all key-values in the dictionary 

:elixir:func:`get/2`          Returns the value for the given key 

:elixir:func:`get_keys/1`     Returns all keys that have the given ``value`` 

:elixir:func:`group_leader/0` Returns the pid of the group leader for the process which evaluates the function 

:elixir:func:`group_leader/2` Sets the group leader of ``pid`` to ``leader``. Typically, this is used when a processes started from a certain shell should have another group leader than ``:init`` 

:elixir:func:`info/1`         Returns information about the process identified by pid or nil if the process is not alive. Use this only for debugging information 

:elixir:func:`info/2`         Returns information about the process identified by pid or nil if the process is not alive 

:elixir:func:`link/1`         Creates a link between the calling process and another process (or port) ``pid``, if there is not such a link already 

:elixir:func:`list/0`         Returns a list of process identifiers corresponding to all the processes currently existing on the local node 

:elixir:func:`monitor/1`      The calling process starts monitoring the item given. It returns the monitor reference 

:elixir:func:`put/2`          Stores the given key-value in the process dictionary 

:elixir:func:`register/2`     Associates the name with a pid or a port identifier. name, which must be an atom, can be used instead of the pid / port identifier with the ```Kernel.send/2`` <Kernel.html#send/2>`__ function 

:elixir:func:`registered/0`   Returns a list of names which have been registered using register/2 

:elixir:func:`send/3`         Sends a message to the given process 

:elixir:func:`send_after/3`   Sends ``msg`` to ``dest`` after ``time`` millisecons 

:elixir:func:`spawn/2`        Spawns the given module and function passing the given args according to the given options 

:elixir:func:`spawn/4`        Spawns the given module and function passing the given args according to the given options 

:elixir:func:`unlink/1`       Removes the link, if there is one, between the calling process and the process or port referred to by ``pid``. Returns true and does not fail, even if there is no link or ``id`` does not exist 

:elixir:func:`unregister/1`   Removes the registered name, associated with a pid or a port identifier 

:elixir:func:`whereis/1`      Returns the pid or port identifier with the registered name. Returns nil if the name is not registered 
============================= =



Types
-----

.. elixir:type:: Process.spawn_opt/0

   :elixir:type:`spawn_opt/0` :: :link | :monitor | {:priority, :low | :normal | :high} | {:fullsweep_after, non_neg_integer} | {:min_heap_size, non_neg_integer} | {:min_bin_vheap_size, non_neg_integer}
   

.. elixir:type:: Process.spawn_opts/0

   :elixir:type:`spawn_opts/0` :: [:elixir:type:`spawn_opt/0`]
   





Functions
---------

.. elixir:function:: Process.alive?/1
   :sig: alive?(pid)


   Specs:
   
 
   * alive?(pid) :: boolean
 

   
   Returns true if the process exists and is alive, that is, is not exiting
   and has not exited. Otherwise, returns false.
   
   ``pid`` must refer to a process at the local node.
   
   

.. elixir:function:: Process.delete/1
   :sig: delete(key)


   Specs:
   
 
   * delete(term) :: term | nil
 

   
   Deletes the given key from the dictionary.
   
   

.. elixir:function:: Process.demonitor/2
   :sig: demonitor(monitor_ref, options \\ [])


   Specs:
   
 
   * demonitor(reference, options :: [:flush | :info]) :: boolean
 

   
   If monitor\_ref is a reference which the calling process obtained by
   calling monitor/1, this monitoring is turned off. If the monitoring is
   already turned off, nothing happens.
   
   See http://www.erlang.org/doc/man/erlang.html#demonitor-2 for more info.
   
   Inlined by the compiler.
   
   

.. elixir:function:: Process.exit/2
   :sig: exit(pid, reason)


   Specs:
   
 
   * exit(pid, term) :: true
 

   
   Sends an exit signal with the given reason to the pid.
   
   The following behaviour applies if reason is any term except ``:normal``
   or ``:kill``:
   
   1) If pid is not trapping exits, pid will exit with the given reason;
   
   2) If pid is trapping exits, the exit signal is transformed into a
      message {:EXIT, from, reason} and delivered to the message queue of
      pid;
   
   3) If reason is the atom ``:normal``, pid will not exit. If it is
      trapping exits, the exit signal is transformed into a message {:EXIT,
      from, :normal} and delivered to its message queue;
   
   4) If reason is the atom ``:kill``, that is if ``exit(pid, :kill)`` is
      called, an untrappable exit signal is sent to pid which will
      unconditionally exit with exit reason ``:killed``.
   
   Inlined by the compiler.
   
   **Examples**
   
   ::
   
       Process.exit(pid, :kill)
   
   
   

.. elixir:function:: Process.flag/2
   :sig: flag(flag, value)


   Specs:
   
 
   * flag(process_flag, term) :: term
 

   
   Sets certain flags for the process which calls this function. Returns
   the old value of the flag.
   
   See http://www.erlang.org/doc/man/erlang.html#process\_flag-2 for more
   info.
   
   

.. elixir:function:: Process.flag/3
   :sig: flag(pid, flag, value)


   Specs:
   
 
   * flag(pid, process_flag, term) :: term
 

   
   Sets certain flags for the process Pid, in the same manner as flag/2.
   Returns the old value of the flag. The allowed values for Flag are only
   a subset of those allowed in flag/2, namely: save\_calls.
   
   See http://www.erlang.org/doc/man/erlang.html#process\_flag-3 for more
   info.
   
   

.. elixir:function:: Process.get/0
   :sig: get()


   Specs:
   
 
   * get :: [{term, term}]
 

   
   Returns all key-values in the dictionary.
   
   

.. elixir:function:: Process.get/2
   :sig: get(key, default \\ nil)


   Specs:
   
 
   * get(term, default :: term) :: term
 

   
   Returns the value for the given key.
   
   

.. elixir:function:: Process.get_keys/1
   :sig: get_keys(value)


   Specs:
   
 
   * get_keys(term) :: [term]
 

   
   Returns all keys that have the given ``value``.
   
   

.. elixir:function:: Process.group_leader/0
   :sig: group_leader()


   Specs:
   
 
   * group_leader :: pid
 

   
   Returns the pid of the group leader for the process which evaluates the
   function.
   
   

.. elixir:function:: Process.group_leader/2
   :sig: group_leader(pid, leader)


   Specs:
   
 
   * group_leader(pid, leader :: pid) :: true
 

   
   Sets the group leader of ``pid`` to ``leader``. Typically, this is used
   when a processes started from a certain shell should have another group
   leader than ``:init``.
   
   

.. elixir:function:: Process.info/1
   :sig: info(pid)


   Specs:
   
 
   * info(pid) :: :elixir:type:`Keyword.t/0`
 

   
   Returns information about the process identified by pid or nil if the
   process is not alive. Use this only for debugging information.
   
   See http://www.erlang.org/doc/man/erlang.html#process\_info-1 for more
   info.
   
   

.. elixir:function:: Process.info/2
   :sig: info(pid, spec)


   Specs:
   
 
   * info(pid, atom) :: {atom, term}
 

   
   Returns information about the process identified by pid or nil if the
   process is not alive.
   
   See http://www.erlang.org/doc/man/erlang.html#process\_info-2 for more
   info.
   
   

.. elixir:function:: Process.link/1
   :sig: link(pid)


   Specs:
   
 
   * link(pid | port) :: true
 

   
   Creates a link between the calling process and another process (or port)
   ``pid``, if there is not such a link already.
   
   See http://www.erlang.org/doc/man/erlang.html#link-1 for more info.
   
   Inlined by the compiler.
   
   

.. elixir:function:: Process.list/0
   :sig: list()


   Specs:
   
 
   * list :: [pid]
 

   
   Returns a list of process identifiers corresponding to all the processes
   currently existing on the local node.
   
   Note that a process that is exiting, exists but is not alive, i.e.,
   alive?/1 will return false for a process that is exiting, but its
   process identifier will be part of the result returned.
   
   See http://www.erlang.org/doc/man/erlang.html#processes-0 for more info.
   
   

.. elixir:function:: Process.monitor/1
   :sig: monitor(item)


   Specs:
   
 
   * monitor(pid | {reg_name :: atom, node :: atom} | reg_name :: atom) :: reference
 

   
   The calling process starts monitoring the item given. It returns the
   monitor reference.
   
   See http://www.erlang.org/doc/man/erlang.html#monitor-2 for more info.
   
   Inlined by the compiler.
   
   

.. elixir:function:: Process.put/2
   :sig: put(key, value)


   Specs:
   
 
   * put(term, term) :: term | nil
 

   
   Stores the given key-value in the process dictionary.
   
   

.. elixir:function:: Process.register/2
   :sig: register(pid, name)


   Specs:
   
 
   * register(pid | port, atom) :: true
 

   
   Associates the name with a pid or a port identifier. name, which must be
   an atom, can be used instead of the pid / port identifier with the
   ```Kernel.send/2`` <Kernel.html#send/2>`__ function.
   
   ```Process.register/2`` <Process.html#register/2>`__ will fail with
   ```ArgumentError`` <ArgumentError.html>`__ if the pid supplied is no
   longer alive, (check with ```alive?/1`` <#alive?/1>`__) or if the name
   is already registered (check with ``registered?/1``).
   
   

.. elixir:function:: Process.registered/0
   :sig: registered()


   Specs:
   
 
   * registered :: [atom]
 

   
   Returns a list of names which have been registered using register/2.
   
   

.. elixir:function:: Process.send/3
   :sig: send(dest, msg, options)


   Specs:
   
 
   * (send(dest, msg, [option]) :: result) when dest: pid | port | atom | {atom, node}, msg: any, option: :noconnect | :nosuspend, result: :ok | :noconnect | :nosuspend
 

   
   Sends a message to the given process.
   
   If the option ``:noconnect`` is used and sending the message would
   require an auto-connection to another node the message is not sent and
   ``:noconnect`` is returned.
   
   If the option ``:nosuspend`` is used and sending the message would cause
   the sender to be suspended the message is not sent and ``:nosuspend`` is
   returned.
   
   Otherwise the message is sent and ``:ok`` is returned.
   
   **Examples**
   
   ::
   
       iex> Process.send({:name, :node_does_not_exist}, :hi, [:noconnect])
       :noconnect
   
   
   

.. elixir:function:: Process.send_after/3
   :sig: send_after(dest, msg, time)


   Specs:
   
 
   * send_after(pid | atom, term, non_neg_integer) :: reference
 

   
   Sends ``msg`` to ``dest`` after ``time`` millisecons.
   
   If ``dest`` is a pid, it has to be a pid of a local process, dead or
   alive. If ``dest`` is an atom, it is supposed to be the name of a
   registered process which is looked up at the time of delivery. No error
   is given if the name does not refer to a process.
   
   This function returns a timer reference, which can be read or canceled
   with
   ```:erlang.read_timer/1`` <http://www.erlang.org/doc/man/erlang.html#read_timer-1>`__,
   ```:erlang.start_timer/3`` <http://www.erlang.org/doc/man/erlang.html#start_timer-3>`__
   and
   ```:erlang.cancel_timer/1`` <http://www.erlang.org/doc/man/erlang.html#cancel_timer-1>`__.
   Note ``time`` cannot be greater than ``4294967295``.
   
   Finally, the timer will be automatically canceled if the given ``dest``
   is a pid which is not alive or when the given pid exits. Note that
   timers will not be automatically canceled when ``dest`` is an atom (as
   the atom resolution is done on delivery).
   
   

.. elixir:function:: Process.spawn/2
   :sig: spawn(fun, opts)


   Specs:
   
 
   * spawn((() -> any), :elixir:type:`spawn_opts/0`) :: pid | {pid, reference}
 

   
   Spawns the given module and function passing the given args according to
   the given options.
   
   The result depends on the given options. In particular, if ``:monitor``
   is given as an option, it will return a tuple containing the pid and the
   monitoring reference, otherwise just the spawned process pid.
   
   It also accepts extra options, for the list of available options check
   http://www.erlang.org/doc/man/erlang.html#spawn\_opt-4
   
   Inlined by the compiler.
   
   

.. elixir:function:: Process.spawn/4
   :sig: spawn(mod, fun, args, opts)


   Specs:
   
 
   * spawn(module, atom, [], :elixir:type:`spawn_opts/0`) :: pid | {pid, reference}
 

   
   Spawns the given module and function passing the given args according to
   the given options.
   
   The result depends on the given options. In particular, if ``:monitor``
   is given as an option, it will return a tuple containing the pid and the
   monitoring reference, otherwise just the spawned process pid.
   
   It also accepts extra options, for the list of available options check
   http://www.erlang.org/doc/man/erlang.html#spawn\_opt-4
   
   Inlined by the compiler.
   
   

.. elixir:function:: Process.unlink/1
   :sig: unlink(pid)


   Specs:
   
 
   * unlink(pid | port) :: true
 

   
   Removes the link, if there is one, between the calling process and the
   process or port referred to by ``pid``. Returns true and does not fail,
   even if there is no link or ``id`` does not exist
   
   See http://www.erlang.org/doc/man/erlang.html#unlink-1 for more info.
   
   Inlined by the compiler.
   
   

.. elixir:function:: Process.unregister/1
   :sig: unregister(name)


   Specs:
   
 
   * unregister(atom) :: true
 

   
   Removes the registered name, associated with a pid or a port identifier.
   
   See http://www.erlang.org/doc/man/erlang.html#unregister-1 for more
   info.
   
   

.. elixir:function:: Process.whereis/1
   :sig: whereis(name)


   Specs:
   
 
   * whereis(atom) :: pid | port | nil
 

   
   Returns the pid or port identifier with the registered name. Returns nil
   if the name is not registered.
   
   See http://www.erlang.org/doc/man/erlang.html#whereis-1 for more info.
   
   







