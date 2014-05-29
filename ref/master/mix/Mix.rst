Mix
==============================================================

.. elixir:module:: Mix

   :mtype: 

Overview
--------

Mix is a build tool that provides tasks for creating, compiling and
testing Elixir projects. Mix is inspired by the Leiningen build tool for
Clojure and was written by one of its contributors.

This module works as a facade for accessing the most common
functionality in Elixir, such as the shell and the current project
configuration.

For getting started with Elixir, checkout out the guide available on
`Elixir's website <http://elixir-lang.org>`__.





Summary
-------

====================== =
:elixir:func:`env/0`   Returns the mix environment 

:elixir:func:`env/1`   Changes the current mix env 

:elixir:func:`shell/0` The shell is a wrapper for doing IO 

:elixir:func:`shell/1` Sets the current shell 
====================== =





Functions
---------

.. elixir:function:: Mix.env/0
   :sig: env()


   
   Returns the mix environment.
   
   

.. elixir:function:: Mix.env/1
   :sig: env(env)


   
   Changes the current mix env.
   
   Be careful when invoking this function as any project configuration
   won't be reloaded.
   
   

.. elixir:function:: Mix.shell/0
   :sig: shell()


   
   The shell is a wrapper for doing IO.
   
   It contains conveniences for asking the user information, printing
   status and so forth. It is also swappable, allowing developers to use a
   test shell that simply sends the messages to the current process.
   
   

.. elixir:function:: Mix.shell/1
   :sig: shell(shell)


   
   Sets the current shell.
   
   







