ExUnit
==============================================================

.. elixir:module:: ExUnit

   :mtype: 

Overview
--------

Basic unit testing framework for Elixir.

Example
~~~~~~~

A basic setup for ExUnit is shown below:

::

    # File: assertion_test.exs

    # 1) Start ExUnit.
    ExUnit.start

    # 2) Create a new test module (test case) and use [`ExUnit.Case`](ExUnit.Case.html).
    defmodule AssertionTest do
      # 3) Notice we pass `async: true`, this runs the test case
      #    concurrently with other test cases
      use ExUnit.Case, async: true

      # 4) Use the `test` macro instead of `def` for clarity.
      test "the truth" do
        assert true
      end
    end

To run the tests above, run the file using ``elixir`` from the command
line. Assuming you named the file ``assertion_test.exs``, you can run it
as:

::

    bin/elixir assertion_test.exs

Case, Callbacks and Assertions
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

See ```ExUnit.Case`` <ExUnit.Case.html>`__ and
```ExUnit.Callbacks`` <ExUnit.Callbacks.html>`__ for more information
about defining test cases.

The ```ExUnit.Assertions`` <ExUnit.Assertions.html>`__ module contains a
set of macros to easily generate assertions with appropriate error
messages.

Integration with Mix
~~~~~~~~~~~~~~~~~~~~

Mix is the project management and build tool for Elixir. Invoking
``mix test`` from the command line will run the tests in each file
matching the pattern ``*_test.exs`` found in the ``test`` directory of
your project.

You must create a ``test_helper.exs`` file inside the ``test`` directory
and put the code common to all tests there.

The minimum example of a ``test_helper.exs`` file would be:

::

    # test/test_helper.exs
    ExUnit.start

Mix will load the ``test_helper.exs`` file before executing the tests.
It is not necessary to ``require`` the ``test_helper.exs`` file in your
test files. See ``Mix.Tasks.Test`` for more information.





Summary
-------

============================== =
:elixir:func:`configuration/0` Returns ExUnit configuration 

:elixir:func:`configure/1`     Configures ExUnit 

:elixir:func:`run/0`           API used to run the tests. It is invoked automatically if ExUnit is started via ```ExUnit.start/1`` <ExUnit.html#start/1>`__ 

:elixir:func:`start/1`         Starts ExUnit and automatically runs tests right before the VM terminates. It accepts a set of options to configure ```ExUnit`` <ExUnit.html>`__ (the same ones accepted by ```configure/1`` <#configure/1>`__) 
============================== =



Types
-----

.. elixir:type:: ExUnit.state/0

   :elixir:type:`state/0` :: nil | {:failed, :elixir:type:`failed/0`} | {:skip, binary} | {:invalid, module}
   

   The state returned by ExUnit.Test and ExUnit.TestCase
   

.. elixir:type:: ExUnit.failed/0

   :elixir:type:`failed/0` :: {:elixir:type:`Exception.kind/0`, reason :: term, stacktrace :: [tuple]}
   





Functions
---------

.. elixir:function:: ExUnit.configuration/0
   :sig: configuration()


   
   Returns ExUnit configuration.
   
   

.. elixir:function:: ExUnit.configure/1
   :sig: configure(options)


   
   Configures ExUnit.
   
   **Options**
   
   ExUnit supports the following options:
   
   -  ``:color`` - When color should be used by specific formatters.
      Defaults to the result of ``IO.ANSI.terminal?/1``;
   
   -  ``:formatters`` - The formatters that will print results. Defaults to
      ``[ExUnit.CLIFormatter]``;
   
   -  ``:max_cases`` - Maximum number of cases to run in parallel. Defaults
      to ``:erlang.system_info(:schedulers_online)``;
   
   -  ``:trace`` - Set ExUnit into trace mode, this sets ``:max_cases`` to
      ``1`` and prints each test case and test while running;
   
   -  ``:autorun`` - If ExUnit should run by default on exit, defaults to
      ``true``;
   
   -  ``:include`` - Specify which tests are run by skipping tests that do
      not match the filter
   
   -  ``:exclude`` - Specify which tests are run by skipping tests that
      match the filter
   
   -  ``:seed`` - An integer seed value to randomize the test suite
   
   
   
   

.. elixir:function:: ExUnit.run/0
   :sig: run()


   
   API used to run the tests. It is invoked automatically if ExUnit is
   started via ```ExUnit.start/1`` <ExUnit.html#start/1>`__.
   
   Returns a map containing the number of tests and the number of failures.
   
   

.. elixir:function:: ExUnit.start/1
   :sig: start(options \\ [])


   
   Starts ExUnit and automatically runs tests right before the VM
   terminates. It accepts a set of options to configure
   ```ExUnit`` <ExUnit.html>`__ (the same ones accepted by
   ```configure/1`` <#configure/1>`__).
   
   If you want to run tests manually, you can set ``:autorun`` to
   ``false``.
   
   







