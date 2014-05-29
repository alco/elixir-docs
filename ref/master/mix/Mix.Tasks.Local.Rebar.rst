Mix.Tasks.Local.Rebar
==============================================================

.. elixir:module:: Mix.Tasks.Local.Rebar

   :mtype: 

Overview
--------

Fetch a copy of rebar from the given path or url. It defaults to a rebar
copy that ships with Elixir source if available or fetches it from
http://s3.hex.pm/rebar.

The local copy is stored in your MIX\_HOME (defaults to ~/.mix). This
version of rebar will be used as required by ``mix deps.compile``.





Summary
-------

==================== =
:elixir:func:`run/1` Callback implementation of :elixir:func:`Mix.Task.run/1` 
==================== =





Functions
---------

.. elixir:function:: Mix.Tasks.Local.Rebar.run/1
   :sig: run(argv)


   
   Callback implementation of :elixir:func:`Mix.Task.run/1`.
   
   







