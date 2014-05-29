Mix.Config
==============================================================

.. elixir:module:: Mix.Config

   :mtype: 

Overview
--------

Module for reading and merging app configurations.





Summary
-------

========================== =
:elixir:func:`merge/2`     Merges two configurations 

:elixir:func:`merge/3`     Merges two configurations 

:elixir:func:`persist/1`   Persists the given configuration by modifying the configured applications environment 

:elixir:func:`read/1`      Reads a configuration file 

:elixir:func:`validate!/1` Validates a configuration 
========================== =





Functions
---------

.. elixir:function:: Mix.Config.merge/2
   :sig: merge(config1, config2)


   
   Merges two configurations.
   
   The configuration of each application is merged together with the values
   in the second one having higher preference than the first in case of
   conflicts.
   
   **Examples**
   
   ::
   
       iex> Mix.Config.merge([app: [k: :v1]], [app: [k: :v2]])
       [app: [k: :v2]]
   
       iex> Mix.Config.merge([app1: []], [app2: []])
       [app1: [], app2: []]
   
   
   

.. elixir:function:: Mix.Config.merge/3
   :sig: merge(config1, config2, callback)


   
   Merges two configurations.
   
   The configuration of each application is merged together and a callback
   is invoked in case of conflicts receiving the app, the conflicting key
   and both values. It must return a value that will be used as part of the
   conflict resolution.
   
   **Examples**
   
   ::
   
       iex> Mix.Config.merge([app: [k: :v1]], [app: [k: :v2]],
       ...>   fn app, k, v1, v2 -> {app, k, v1, v2} end)
       [app: [k: {:app, :k, :v1, :v2}]]
   
   
   

.. elixir:function:: Mix.Config.persist/1
   :sig: persist(config)


   
   Persists the given configuration by modifying the configured
   applications environment.
   
   

.. elixir:function:: Mix.Config.read/1
   :sig: read(file)


   
   Reads a configuration file.
   
   It returns the read configuration and a list of dependencies this
   configuration may have on.
   
   

.. elixir:function:: Mix.Config.validate!/1
   :sig: validate!(config)


   
   Validates a configuration.
   
   







