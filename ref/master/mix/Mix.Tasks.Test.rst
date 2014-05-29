Mix.Tasks.Test
==============================================================

.. elixir:module:: Mix.Tasks.Test

   :mtype: 

Overview
--------

Run the tests for a project.

This task starts the current application, loads up
``test/test_helper.exs`` and then requires all files matching the
``test/**/_test.exs`` pattern in parallel.

A list of files can be given after the task name in order to select the
files to compile:

::

    mix test test/some/particular/file_test.exs

Command line options
~~~~~~~~~~~~~~~~~~~~

-  ``--trace`` - run tests with detailed reporting. Automatically sets
   ``--max-cases`` to 1
-  ``--max-cases`` - set the maximum number of cases running async
-  ``--cover`` - the directory to include coverage results
-  ``--force`` - forces compilation regardless of modification times
-  ``--no-compile`` - do not compile, even if files require compilation
-  ``--no-start`` - do not start applications after compilation
-  ``--no-color`` - disable color in the output
-  ``--include`` - include tests that match the filter
-  ``--exclude`` - exclude tests that match the filter
-  ``--only`` - run only tests that match the filter
-  ``--seed`` - seeds the random number generator used to randomize
   tests order

Filters
~~~~~~~

ExUnit provides tags and filtering functionality that allows developers
to select which tests to run. The most common functionality is to
exclude some particular tests from running by default in your test
helper file:

::

    # Exclude all external tests from running
    ExUnit.configure exclude: [external: true]

Then, whenever desired, those tests could be included in the run via the
``--include`` flag:

::

    mix test --include external:true

The example above will run all tests that have the external flag set to
true. It is also possible to include all examples that have a given tag,
regardless of its value:

::

    mix test --include external

Note that all tests are included by default, so unless they are excluded
first (either in the test helper or via the ``--exclude`` option), the
``--include`` flag has no effect.

For this reason, mix also provides an ``--only`` option that excludes
all tests and includes only the given ones:

::

    mix test --only external

Which is equivalent to:

::

    mix test --include external --exclude test

When filtering tests by line number the following styles are equivalent:

::

    mix test test/some/particular/file_test.exs:12
    mix test --only line:12 test/some/particular/file_test.exs

Configuration
~~~~~~~~~~~~~

-  ``:test_paths`` - list of paths containing test files, defaults to
   ``["test"]``. it is expected all test paths to contain a
   ``test_helper.exs`` file

-  ``:test_pattern`` - a pattern to load test files, defaults to
   ``*_test.exs``

-  ``:test_coverage`` - a set of options to be passed down to the
   coverage mechanism

Coverage
~~~~~~~~

The ``:test_coverage`` configuration accepts the following options:

-  ``:output`` - the output for cover results, defaults to ``"cover"``
-  ``:tool`` - the coverage tool

By default, a very simple wrapper around OTP's ``cover`` is used as a
tool, but it can be overridden as follows:

::

    test_coverage: [tool: CoverModule]

``CoverModule`` can be any module that exports ``start/2``, receiving
the compilation path and the ``test_coverage`` options as arguments. It
must return an anonymous function of zero arity that will be run after
the test suite is done or nil.





Summary
-------

==================== =
:elixir:func:`run/1` Callback implementation of :elixir:func:`Mix.Task.run/1` 
==================== =





Functions
---------

.. elixir:function:: Mix.Tasks.Test.run/1
   :sig: run(args)


   
   Callback implementation of :elixir:func:`Mix.Task.run/1`.
   
   







