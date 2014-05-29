Mix.SCM
==============================================================

.. elixir:module:: Mix.SCM

   :mtype: behaviour

Overview
--------

This module provides helper functions and defines the behaviour required
by any SCM used by mix.





Summary
-------

========================== =
:elixir:func:`append/1`    Append the given SCM module to the list of available SCMs 

:elixir:func:`available/0` Returns all available SCMs. Each SCM is tried in order until a matching one is found 

:elixir:func:`prepend/1`   Prepend the given SCM module to the list of available SCMs 
========================== =



Types
-----

.. elixir:type:: Mix.SCM.opts/0

   :elixir:type:`opts/0` :: :elixir:type:`Keyword.t/0`
   





Functions
---------

.. elixir:function:: Mix.SCM.append/1
   :sig: append(mod)


   
   Append the given SCM module to the list of available SCMs.
   
   

.. elixir:function:: Mix.SCM.available/0
   :sig: available()


   
   Returns all available SCMs. Each SCM is tried in order until a matching
   one is found.
   
   

.. elixir:function:: Mix.SCM.prepend/1
   :sig: prepend(mod)


   
   Prepend the given SCM module to the list of available SCMs.
   
   







Callbacks
---------

.. elixir:callback:: Mix.SCM.accepts_options/2
   :sig: accepts_options/2


   Specs:
   
 
   * accepts_options(app :: atom, :elixir:type:`opts/0`) :: :elixir:type:`opts/0` | nil
 

   
   This behaviour function receives a keyword list of ``opts`` and should
   return an updated list in case the SCM consumes the available options.
   For example, when a developer specifies a dependency:
   
   ::
   
       {:foo, "0.1.0", github: "foo/bar"}
   
   Each registered SCM will be asked if they consume this dependency,
   receiving ``[github: "foo/bar"]`` as argument. Since this option makes
   sense for the Git SCM, it will return an update list of options while
   other SCMs would simply return nil.
   
   

.. elixir:callback:: Mix.SCM.checked_out?/1
   :sig: checked_out?/1


   Specs:
   
 
   * checked_out?(:elixir:type:`opts/0`) :: boolean
 

   
   This behaviour function returns a boolean if the dependency is
   available.
   
   

.. elixir:callback:: Mix.SCM.checkout/1
   :sig: checkout/1


   Specs:
   
 
   * checkout(:elixir:type:`opts/0`) :: any
 

   
   This behaviour function checks out dependencies.
   
   If the dependency is locked, a lock is received in ``opts`` and the
   repository must be check out at the lock. Otherwise, no lock is given
   and the repository can be checked out to the latest version.
   
   It must return the current lock.
   
   

.. elixir:callback:: Mix.SCM.equal?/2
   :sig: equal?/2


   Specs:
   
 
   * equal?(opts1 :: :elixir:type:`opts/0`, opts2 :: :elixir:type:`opts/0`) :: boolean
 

   
   Receives two options and must return true if they refer to the same
   repository. The options are guaranteed to belong to the same SCM.
   
   

.. elixir:callback:: Mix.SCM.fetchable?/0
   :sig: fetchable?/0


   Specs:
   
 
   * fetchable? :: boolean
 

   
   Returns a boolean if the dependency can be fetched or it is meant to be
   previously available in the filesystem.
   
   

.. elixir:callback:: Mix.SCM.format/1
   :sig: format/1


   Specs:
   
 
   * format(:elixir:type:`opts/0`) :: :elixir:type:`String.t/0`
 

   
   Returns a string representing the SCM. This is used when printing the
   dependency and not for inspection, so the amount of information should
   be concise and easy to spot.
   
   

.. elixir:callback:: Mix.SCM.format_lock/1
   :sig: format_lock/1


   Specs:
   
 
   * format_lock(:elixir:type:`opts/0`) :: :elixir:type:`String.t/0` | nil
 

   
   Returns a string representing the SCM. This is used when printing the
   dependency and not for inspection, so the amount of information should
   be concise and easy to spot.
   
   If nil is returned, it means no lock information is available.
   
   

.. elixir:callback:: Mix.SCM.lock_status/1
   :sig: lock_status/1


   Specs:
   
 
   * lock_status(:elixir:type:`opts/0`) :: :mismatch | :outdated | :ok
 

   
   This behaviour function checks the status of the lock. In particular, it
   checks if the revision stored in the lock is the same as the repository
   it is currently in. It may return:
   
   -  ``:mismatch`` - if the lock doesn't match and we need to simply move
      to the latest lock
   -  ``:outdated`` - the repository options are outdated in the lock and
      we need to trigger a full update
   -  ``:ok`` - everything is fine
   
   The lock is sent via ``opts[:lock]`` but it may not always be available.
   In such cases, if the SCM requires a lock, it must return
   ``:lockmismatch``, otherwise simply ``:ok``.
   
   Note the lock may also belong to another SCM and as such, an structural
   check is required. A structural mismatch should always return
   ``:outdated``.
   
   

.. elixir:callback:: Mix.SCM.update/1
   :sig: update/1


   Specs:
   
 
   * update(:elixir:type:`opts/0`) :: any
 

   
   This behaviour function updates dependencies. It may be called by
   ``deps.get`` or ``deps.update``.
   
   In the first scenario, a lock is received in ``opts`` and the repository
   must be updated to the lock. In the second, no lock is given and the
   repository can be updated freely.
   
   It must return the current lock.
   
   



