ExUnit.Callbacks
==============================================================

.. elixir:module:: ExUnit.Callbacks

   :mtype: 

Overview
--------

Defines ExUnit Callbacks.

This module defines four callbacks: ``setup_all``, ``teardown_all``,
``setup`` and ``teardown``.

These callbacks are defined via macros and each one can optionally
receive a map with metadata, usually referred to as ``context``. The
callback may optionally put extra data into ``context`` to be used in
the tests.

If you return ``{:ok, <dict>}`` from ``setup`` or ``teardown``, the
keyword list will be merged into the context that will be available in
all subsequent ``setup``, ``test`` or ``teardown`` calls.

Similarly, returning ``{:ok, <dict>}`` from ``setup_all`` or
``teardown_all`` will merge the keyword list into the context that will
be available in all subsequent ``setup_all`` or ``teardown_all`` calls.

Returning ``:ok`` leaves the context unchanged in both cases.

Returning anything else from ``setup`` or ``teardown`` will force the
current test to fail, and subsequent ``setup``, ``test`` and
``teardown`` callbacks won't be called for it.

Returning anything else from ``setup_all`` or ``teardown_all`` will
force the whole case to fail, and no other callback will be called.

It is possible to define multiple ``setup`` and ``teardown`` callbacks
and they will be called sequentially. In the case of ``setup_all`` and
``teardown_all`` callbacks, each ``setup_all`` will be called only once
before the first test's ``setup`` and each ``teardown_all`` will be
called once after the last test. No callback runs if the test case has
no tests or all tests were filtered out via ``include``/``exclude``.

Examples
~~~~~~~~

::

    defmodule AssertionTest do
      use ExUnit.Case, async: true

      # `setup` is called before each test is run
      setup do
        IO.puts "This is a setup callback"

        # Return extra metadata, it must be a keyword list / map
        {:ok, hello: "world"}
      end

      # Same as `setup`, but receives the context for the current test
      setup context do
        # We can access the current test in the context
        IO.puts "Setting up: #{context[:test]}"

        # We can also access the data returned from `setup/0`
        assert context[:hello] == "world"

        # No metadata
        :ok
      end

      # This is called after each test finishes
      teardown context do
        assert context[:hello] == "world"
        :ok
      end

      test "always pass" do
        assert true
      end

      test "another one", context do
        assert context[:hello] == "world"
      end
    end






Summary
-------

============================== =
:elixir:macro:`setup/2`        Called before the start of each test 

:elixir:macro:`setup_all/2`    Called before the start of a case, i.e. called once before the first test in the current module and before any ``setup`` callbacks 

:elixir:macro:`teardown/2`     Called after the completion of each test 

:elixir:macro:`teardown_all/2` Called once after the last test finishes without emitting an ``:exit`` message 
============================== =







Macros
------

.. elixir:macro:: ExUnit.Callbacks.setup/2
   :sig: setup(var \\ {:_, [], ExUnit.Callbacks}, block)


   
   Called before the start of each test.
   
   

.. elixir:macro:: ExUnit.Callbacks.setup_all/2
   :sig: setup_all(var \\ {:_, [], ExUnit.Callbacks}, block)


   
   Called before the start of a case, i.e. called once before the first
   test in the current module and before any ``setup`` callbacks.
   
   

.. elixir:macro:: ExUnit.Callbacks.teardown/2
   :sig: teardown(var \\ {:_, [], ExUnit.Callbacks}, block)


   
   Called after the completion of each test.
   
   Note that if the test crashed with an ``:exit`` message, ``teardown``
   will not be run.
   
   

.. elixir:macro:: ExUnit.Callbacks.teardown_all/2
   :sig: teardown_all(var \\ {:_, [], ExUnit.Callbacks}, block)


   
   Called once after the last test finishes without emitting an ``:exit``
   message.
   
   





