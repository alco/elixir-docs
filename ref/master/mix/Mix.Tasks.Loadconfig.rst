Mix.Tasks.Loadconfig
==============================================================

.. elixir:module:: Mix.Tasks.Loadconfig

   :mtype: 

Overview
--------

Loads and persists the project configuration.

In case the application is an umbrella application, the configuration
for all children app will be merged together and, in case there are any
conflicts, they need to be resolved in the umbrella application.





Summary
-------

===================== =
:elixir:func:`load/0` Loads the configuration for the current project 

:elixir:func:`run/1`  Runs this task 
===================== =





Functions
---------

.. elixir:function:: Mix.Tasks.Loadconfig.load/0
   :sig: load()


   
   Loads the configuration for the current project.
   
   

.. elixir:function:: Mix.Tasks.Loadconfig.run/1
   :sig: run()


   
   Runs this task.
   
   







