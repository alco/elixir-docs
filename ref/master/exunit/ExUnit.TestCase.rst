ExUnit.TestCase
==============================================================

.. elixir:module:: ExUnit.TestCase

   :mtype: 

Overview
--------

A struct that keeps information about the test case.

It is received by formatters and contains the following fields:

-  ``:name`` - the test case name
-  ``:state`` - the test state (see ExUnit.state)
-  ``:tests`` - all tests for this case








Types
-----

.. elixir:type:: ExUnit.TestCase.t/0

   :elixir:type:`t/0` :: %ExUnit.TestCase{name: module, state: :elixir:type:`ExUnit.state/0`, tests: [:elixir:type:`ExUnit.Test.t/0`]}
   









