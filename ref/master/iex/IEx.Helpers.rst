IEx.Helpers
==============================================================

.. elixir:module:: IEx.Helpers

   :mtype: 

Overview
--------

Welcome to Interactive Elixir. You are currently seeing the
documentation for the module ```IEx.Helpers`` <IEx.Helpers.html>`__
which provides many helpers to make Elixir's shell more joyful to work
with.

This message was triggered by invoking the helper ``h()``, usually
referred to as ```h/0`` <#h/0>`__ (since it expects 0 arguments).

There are many other helpers available:

-  ```c/2`` <#c/2>`__ — compiles a file at the given path
-  ```cd/1`` <#cd/1>`__ — changes the current directory
-  ```clear/0`` <#clear/0>`__ — clears the screen
-  ```flush/0`` <#flush/0>`__ — flushes all messages sent to the shell
-  ```h/0`` <#h/0>`__ — prints this help message
-  ```h/1`` <#h/1>`__ — prints help for the given module, function or
   macro
-  ```l/1`` <#l/1>`__ — loads the given module's beam code and purges
   the current version
-  ``ls/0`` — lists the contents of the current directory
-  ```ls/1`` <#ls/1>`__ — lists the contents of the specified directory
-  ```pwd/0`` <#pwd/0>`__ — prints the current working directory
-  ```r/1`` <#r/1>`__ — recompiles and reloads the given module's source
   file
-  ```respawn/0`` <#respawn/0>`__ — respawns the current shell
-  ```s/1`` <#s/1>`__ — prints spec information
-  ```t/1`` <#t/1>`__ — prints type information
-  ```v/0`` <#v/0>`__ — prints the history of commands evaluated in the
   session
-  ```v/1`` <#v/1>`__ — retrieves the nth value from the history
-  ```import_file/1`` <#import_file/1>`__ — evaluates the given file in
   the shell's context

Help for functions in this module can be consulted directly from the
command line, as an example, try:

::

    h(c/2)

You can also retrieve the documentation for any module or function. Try
these:

::

    h(Enum)
    h(Enum.reverse/1)

To learn more about IEx as a whole, just type ``h(IEx)``.





Summary
-------

============================= =
:elixir:func:`c/2`            Expects a list of files to compile and a path to write their object code to. It returns the name of the compiled modules 

:elixir:func:`cd/1`           Changes the current working directory to the given path 

:elixir:func:`clear/0`        Clear the console screen 

:elixir:func:`flush/0`        Flushes all messages sent to the shell and prints them out 

:elixir:func:`h/0`            Prints the documentation for ```IEx.Helpers`` <IEx.Helpers.html>`__ 

:elixir:macro:`h/1`           Prints the documentation for the given module or for the given function/arity pair 

:elixir:macro:`import_file/1` Evaluates the contents of the file at ``path`` as if it were directly typed into the shell. ``path`` has to be a literal binary 

:elixir:func:`l/1`            Load the given module's beam code (and ensures any previous old version was properly purged before) 

:elixir:func:`ls/1`           Produces a simple list of a directory's contents. If ``path`` points to a file, prints its full path 

:elixir:func:`pwd/0`          Prints the current working directory 

:elixir:func:`r/1`            Recompiles and reloads the specified module's source file 

:elixir:func:`respawn/0`      Respawns the current shell by starting a new process and a new scope. Returns true if it worked 

:elixir:macro:`s/1`           Similar to ```t/1`` <#t/1>`__, only for specs 

:elixir:macro:`t/1`           When given a module, prints specifications (or simply specs) for all the types defined in it 

:elixir:func:`v/0`            Prints the history of expressions evaluated during the session along with their results 

:elixir:func:`v/1`            Retrieves the nth expression's value from the history 
============================= =





Functions
---------

.. elixir:function:: IEx.Helpers.c/2
   :sig: c(files, path \\ ".")


   
   Expects a list of files to compile and a path to write their object code
   to. It returns the name of the compiled modules.
   
   When compiling one file, there is no need to wrap it in a list.
   
   **Examples**
   
   ::
   
       c ["foo.ex", "bar.ex"], "ebin"
       #=> [Foo,Bar]
   
       c "baz.ex"
       #=> [Baz]
   
   
   

.. elixir:function:: IEx.Helpers.cd/1
   :sig: cd(directory)


   
   Changes the current working directory to the given path.
   
   

.. elixir:function:: IEx.Helpers.clear/0
   :sig: clear()


   
   Clear the console screen.
   
   

.. elixir:function:: IEx.Helpers.flush/0
   :sig: flush()


   
   Flushes all messages sent to the shell and prints them out.
   
   

.. elixir:function:: IEx.Helpers.h/0
   :sig: h()


   
   Prints the documentation for ```IEx.Helpers`` <IEx.Helpers.html>`__.
   
   

.. elixir:function:: IEx.Helpers.l/1
   :sig: l(module)


   
   Load the given module's beam code (and ensures any previous old version
   was properly purged before).
   
   

.. elixir:function:: IEx.Helpers.ls/1
   :sig: ls(path \\ ".")


   
   Produces a simple list of a directory's contents. If ``path`` points to
   a file, prints its full path.
   
   

.. elixir:function:: IEx.Helpers.pwd/0
   :sig: pwd()


   
   Prints the current working directory.
   
   

.. elixir:function:: IEx.Helpers.r/1
   :sig: r(module)


   
   Recompiles and reloads the specified module's source file.
   
   Please note that all the modules defined in the same file as ``module``
   are recompiled and reloaded.
   
   

.. elixir:function:: IEx.Helpers.respawn/0
   :sig: respawn()


   
   Respawns the current shell by starting a new process and a new scope.
   Returns true if it worked.
   
   

.. elixir:function:: IEx.Helpers.v/0
   :sig: v()


   
   Prints the history of expressions evaluated during the session along
   with their results.
   
   

.. elixir:function:: IEx.Helpers.v/1
   :sig: v(n)


   
   Retrieves the nth expression's value from the history.
   
   Use negative values to lookup expression values relative to the current
   one. For instance, v(-1) returns the result of the last evaluated
   expression.
   
   





Macros
------

.. elixir:macro:: IEx.Helpers.h/1
   :sig: h(other)


   
   Prints the documentation for the given module or for the given
   function/arity pair.
   
   **Examples**
   
   ::
   
       h(Enum)
       #=> Prints documentation for Enum
   
   It also accepts functions in the format ``fun/arity`` and
   ``module.fun/arity``, for example:
   
   ::
   
       h receive/1
       h Enum.all?/2
       h Enum.all?
   
   
   

.. elixir:macro:: IEx.Helpers.import_file/1
   :sig: import_file(path)


   
   Evaluates the contents of the file at ``path`` as if it were directly
   typed into the shell. ``path`` has to be a literal binary.
   
   A leading ``~`` in ``path`` is automatically expanded.
   
   **Examples**
   
   ::
   
       # ~/file.exs
       value = 13
   
       # in the shell
       iex(1)> import_file "~/file.exs"
       13
       iex(2)> value
       13
   
   
   

.. elixir:macro:: IEx.Helpers.s/1
   :sig: s(other)


   
   Similar to ```t/1`` <#t/1>`__, only for specs.
   
   When given a module, prints the list of all specs defined in the module.
   
   When given a particular spec name (with optional arity), prints its
   spec.
   
   **Examples**
   
   ::
   
       s(Enum)
       s(Enum.all?)
       s(Enum.all?/2)
       s(is_atom)
       s(is_atom/1)
   
   
   

.. elixir:macro:: IEx.Helpers.t/1
   :sig: t(module)


   
   When given a module, prints specifications (or simply specs) for all the
   types defined in it.
   
   When given a particular type name, prints its spec.
   
   **Examples**
   
   ::
   
       t(Enum)
       t(Enum.t/0)
       t(Enum.t)
   
   
   





