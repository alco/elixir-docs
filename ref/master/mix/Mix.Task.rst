Mix.Task
==============================================================

.. elixir:module:: Mix.Task

   :mtype: behaviour

Overview
--------

A simple module that provides conveniences for creating, loading and
manipulating tasks.

A Mix task can be defined by simply using
```Mix.Task`` <Mix.Task.html>`__ in a module starting with
``Mix.Tasks.`` and defining the ```run/1`` <#run/1>`__ function:

::

    defmodule Mix.Tasks.Hello do
      use Mix.Task

      def run(_) do
        IO.puts "hello"
      end
    end

The ```run/1`` <#run/1>`__ function will receive all arguments passed to
the command line.

Attributes
~~~~~~~~~~

There are a couple attributes available in Mix tasks to configure them
in Mix:

-  ``@shortdoc`` - makes the task public with a short description that
   appears on ``mix help``
-  ``@recursive`` - run the task recursively in umbrella projects






Summary
-------

============================ =
:elixir:func:`all_modules/0` Returns all loaded tasks 

:elixir:func:`clear/0`       Clears all invoked tasks, allowing them to be reinvoked 

:elixir:func:`get!/1`        Receives a task name and retrieves the task module 

:elixir:func:`get/1`         Receives a task name and retrieves the task module. Returns nil if the task cannot be found 

:elixir:func:`is_task?/1`    Returns ``true`` if given module is a task 

:elixir:func:`load_all/0`    Loads all tasks in all code paths 

:elixir:func:`load_tasks/1`  Loads all tasks in the given ``paths`` 

:elixir:func:`moduledoc/1`   Gets the moduledoc for the given task ``module``. Returns the moduledoc or ``nil`` 

:elixir:func:`recursive/1`   Checks if the task should be run recursively for all sub-apps in umbrella projects. Returns ``true``, ``false`` or ``:both`` 

:elixir:func:`reenable/1`    Reenables a given task so it can be executed again down the stack. If an umbrella project reenables a task it is reenabled for all sub projects 

:elixir:func:`run/2`         Runs a ``task`` with the given ``args`` 

:elixir:func:`shortdoc/1`    Gets the shortdoc for the given task ``module``. Returns the shortdoc or ``nil`` 

:elixir:func:`task_name/1`   Returns the task name for the given ``module`` 
============================ =





Functions
---------

.. elixir:function:: Mix.Task.all_modules/0
   :sig: all_modules()


   
   Returns all loaded tasks.
   
   Modules that are not yet loaded won't show up. Check
   ```load_all/0`` <#load_all/0>`__ if you want to preload all tasks.
   
   

.. elixir:function:: Mix.Task.clear/0
   :sig: clear()


   
   Clears all invoked tasks, allowing them to be reinvoked.
   
   

.. elixir:function:: Mix.Task.get/1
   :sig: get(task)


   
   Receives a task name and retrieves the task module. Returns nil if the
   task cannot be found.
   
   

.. elixir:function:: Mix.Task.get!/1
   :sig: get!(task)


   
   Receives a task name and retrieves the task module.
   
   **Exceptions**
   
   -  ```Mix.NoTaskError`` <Mix.NoTaskError.html>`__ - raised if the task
      could not be found;
   -  ```Mix.InvalidTaskError`` <Mix.InvalidTaskError.html>`__ - raised if
      the task is not a valid ```Mix.Task`` <Mix.Task.html>`__
   
   
   

.. elixir:function:: Mix.Task.is_task?/1
   :sig: is_task?(module)


   
   Returns ``true`` if given module is a task.
   
   

.. elixir:function:: Mix.Task.load_all/0
   :sig: load_all()


   
   Loads all tasks in all code paths.
   
   

.. elixir:function:: Mix.Task.load_tasks/1
   :sig: load_tasks(paths)


   
   Loads all tasks in the given ``paths``.
   
   

.. elixir:function:: Mix.Task.moduledoc/1
   :sig: moduledoc(module)


   
   Gets the moduledoc for the given task ``module``. Returns the moduledoc
   or ``nil``.
   
   

.. elixir:function:: Mix.Task.recursive/1
   :sig: recursive(module)


   
   Checks if the task should be run recursively for all sub-apps in
   umbrella projects. Returns ``true``, ``false`` or ``:both``.
   
   

.. elixir:function:: Mix.Task.reenable/1
   :sig: reenable(task)


   
   Reenables a given task so it can be executed again down the stack. If an
   umbrella project reenables a task it is reenabled for all sub projects.
   
   

.. elixir:function:: Mix.Task.run/2
   :sig: run(task, args \\ [])


   
   Runs a ``task`` with the given ``args``.
   
   If the task was not yet invoked, it runs the task and returns the
   result.
   
   If the task was already invoked, it does not run the task again and
   simply aborts with ``:noop``.
   
   It may raise an exception if the task was not found or it is invalid.
   Check ```get!/1`` <#get!/1>`__ for more information.
   
   

.. elixir:function:: Mix.Task.shortdoc/1
   :sig: shortdoc(module)


   
   Gets the shortdoc for the given task ``module``. Returns the shortdoc or
   ``nil``.
   
   

.. elixir:function:: Mix.Task.task_name/1
   :sig: task_name(module)


   
   Returns the task name for the given ``module``.
   
   







Callbacks
---------

.. elixir:callback:: Mix.Task.run/1
   :sig: run/1


   Specs:
   
 
   * run([binary]) :: any
 

   
   A task needs to implement ``run`` which receives a list of command line
   args.
   
   



