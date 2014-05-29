ExUnit.Test
==============================================================

.. elixir:module:: ExUnit.Test

   :mtype: 

Overview
--------

A struct that keeps information about the test.

It is received by formatters and contains the following fields:

-  ``:name`` - the test name
-  ``:case`` - the test case
-  ``:state`` - the test state (see ExUnit.state)
-  ``:time`` - the time to run the test
-  ``:tags`` - the test tags








Types
-----

.. elixir:type:: ExUnit.Test.t/0

   :elixir:type:`t/0` :: %ExUnit.Test{name: atom, case: module, state: :elixir:type:`ExUnit.state/0`, time: non_neg_integer, tags: %{}}
   









