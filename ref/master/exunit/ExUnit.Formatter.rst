ExUnit.Formatter
==============================================================

.. elixir:module:: ExUnit.Formatter

   :mtype: 

Overview
--------

This module holds helper functions related to formatting and contains
documentation about the formatting protocol.

Formatters are registered at the ``ExUnit.EventManager`` event manager
and will be send events by the runner.

The following events are possible:

-  ``{:suite_started, opts}`` - The suite has started with the specified
   options to the runner.
-  ``{:suite_finished, run_us, load_us}`` - The suite has finished.
   ``run_us`` and ``load_us`` are the run and load times in microseconds
   respectively.
-  ``{:case_started, test_case}`` - A test case has started. See
   :elixir:mod:`ExUnit.TestCase` for details.
-  ``{:case_finished, test_case}`` - A test case has finished. See
   :elixir:mod:`ExUnit.TestCase` for details.
-  ``{:test_started, test_case}`` - A test case has started. See
   :elixir:mod:`ExUnit.Test` for details.
-  ``{:test_finished, test_case}`` - A test case has finished. See
   :elixir:mod:`ExUnit.Test` for details.






Summary
-------

========================================= =
:elixir:func:`format_filters/2`           Formats filters used to constain cases to be run 

:elixir:func:`format_test_case_failure/5` Receives a test case and formats its failure 

:elixir:func:`format_test_failure/5`      Receives a test and formats its failure 

:elixir:func:`format_time/2`              Formats time taken running the test suite 
========================================= =



Types
-----

.. elixir:type:: ExUnit.Formatter.id/0

   :elixir:type:`id/0` :: term
   

.. elixir:type:: ExUnit.Formatter.test_case/0

   :elixir:type:`test_case/0` :: :elixir:type:`ExUnit.TestCase.t/0`
   

.. elixir:type:: ExUnit.Formatter.test/0

   :elixir:type:`test/0` :: :elixir:type:`ExUnit.Test.t/0`
   

.. elixir:type:: ExUnit.Formatter.run_us/0

   :elixir:type:`run_us/0` :: pos_integer
   

.. elixir:type:: ExUnit.Formatter.load_us/0

   :elixir:type:`load_us/0` :: pos_integer | nil
   





Functions
---------

.. elixir:function:: ExUnit.Formatter.format_filters/2
   :sig: format_filters(filters, type)


   Specs:
   
 
   * format_filters(:elixir:type:`Keyword.t/0`, atom) :: :elixir:type:`String.t/0`
 

   
   Formats filters used to constain cases to be run.
   
   **Examples**
   
   iex> format\_filters([run: true, slow: false], :include) "Including
   tags: [run: true, slow: false]"
   
   

.. elixir:function:: ExUnit.Formatter.format_test_case_failure/5
   :sig: format_test_case_failure(test_case, arg2, counter, width, formatter)


   
   Receives a test case and formats its failure.
   
   

.. elixir:function:: ExUnit.Formatter.format_test_failure/5
   :sig: format_test_failure(test, arg2, counter, width, formatter)


   
   Receives a test and formats its failure.
   
   

.. elixir:function:: ExUnit.Formatter.format_time/2
   :sig: format_time(run_us, load_us)


   Specs:
   
 
   * format_time(:elixir:type:`run_us/0`, :elixir:type:`load_us/0`) :: :elixir:type:`String.t/0`
 

   
   Formats time taken running the test suite.
   
   It receives the time spent running the tests and optionally the time
   spent loading the test suite.
   
   **Examples**
   
   ::
   
       iex> format_time(10000, nil)
       "Finished in 0.01 seconds"
   
       iex> format_time(10000, 20000)
       "Finished in 0.03 seconds (0.02s on load, 0.01s on tests)"
   
       iex> format_time(10000, 200000)
       "Finished in 0.2 seconds (0.2s on load, 0.01s on tests)"
   
   
   







