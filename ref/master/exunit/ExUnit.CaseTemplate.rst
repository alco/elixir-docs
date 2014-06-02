ExUnit.CaseTemplate
==============================================================

.. elixir:module:: ExUnit.CaseTemplate

   :mtype: 

Overview
--------

This module allows a developer to define a test case template to be used
throughout his tests. This is useful when there are a set of functions
that should be shared between tests or a set of setup/teardown
callbacks.

By using this module, the callbacks and assertions available for regular
test cases will also be available.

Example
~~~~~~~

::

    defmodule MyCase do
      use ExUnit.CaseTemplate

      setup do
        IO.puts "This will run before each test that uses this case"
      end
    end

    defmodule MyTest do
      use MyCase, async: true

      test "truth" do
        assert true
      end
    end






Summary
-------

====================== =
:elixir:func:`using/2` Allows a developer to customize the using block when the case template is used 
====================== =







Macros
------

.. elixir:macro:: ExUnit.CaseTemplate.using/2
   :sig: using(var \\ {:_, [], ExUnit.CaseTemplate}, list2)


   
   Allows a developer to customize the using block when the case template
   is used.
   
   





