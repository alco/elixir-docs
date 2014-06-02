ExUnit.Case
==============================================================

.. elixir:module:: ExUnit.Case

   :mtype: 

Overview
--------

Sets up an ExUnit test case.

This module must be used in other modules as a way to configure and
prepare them for testing.

When used, it accepts the following options:

-  :async - configure Elixir to run that specific test case in parallel
   with others. Must be used for performance when your test cases do not
   change any global state;

This module automatically includes all callbacks defined in
:elixir:mod:`ExUnit.Callbacks`. See that module's documentation for more
information.

Examples
~~~~~~~~

::

     defmodule AssertionTest do
       # Use the module
       use ExUnit.Case, async: true

       # The `test` macro is imported by ExUnit.Case
       test "always pass" do
         assert true
       end
     end

Context
~~~~~~~

All tests receive a context as an argument. The context is particularly
useful for sharing information between callbacks and tests:

::

    defmodule KVTest do
      use ExUnit.Case

      setup do
        {:ok, pid} = KV.start_link
        {:ok, [pid: pid]}
      end

      test "stores key-values", context do
        assert KV.put(context[:pid], :hello, :world) == :ok
        assert KV.get(context[:pid], :hello) == :world
      end
    end

As the context is a map, it can be pattern matched on to extract
information:

::

    test "stores key-values", %{pid: pid} do
      assert KV.put(pid, :hello, :world) == :ok
      assert KV.get(pid, :hello) == :world
    end

Tags
~~~~

The context is used to pass information from the callbacks to the test.
In order to pass information from the test to the callback, ExUnit
provides tags.

By tagging a test, the tag value can be accessed in the context,
allowing the developer to customize the test. Let's see an example:

::

    defmodule FileTest do
      # Changing directory cannot be async
      use ExUnit.Case, async: false

      setup context do
        # Read the :cd tag value
        if cd = context[:cd] do
          prev_cd = File.cwd!
          File.cd!(cd)
          {:ok, [prev_cd: prev_cd]}
        else
          :ok
        end
      end

      teardown context do
        # Revert to the previous working directory
        if cd = context[:prev_cd] do
          File.cd!(cd)
        end
      end

      @tag cd: "fixtures"
      test "reads utf-8 fixtures" do
        File.read("hello")
      end
    end

In the example above, we have defined a tag called ``:cd`` that is read
in the setup callback to configure the working directory the test is
going to run on. We then use the same context to store the previous
working directory that is reverted to after the test in the teardown
callback.

Tags are also very effective when used with case templates
(:elixir:mod:`ExUnit.CaseTemplate`) allowing callbacks in the case template to
customize the test behaviour.

Note a tag can be set in two different ways:

::

    @tag key: value
    @tag :key       # equivalent to setting @tag key: true

If a tag is given more than once, the last value wins.

Module tags
^^^^^^^^^^^

A tag can be set for all tests in a module by setting ``@moduletag``:

::

    @moduletag :external

If the same key is set via ``@tag``, the ``@tag`` value has higher
precedence.

Reserved tags
^^^^^^^^^^^^^

The following tags are set automatically by ExUnit and are therefore
reserved:

-  ``:case`` - the test case module
-  ``:test`` - the test name
-  ``:line`` - the line on which the test was defined
-  ``:file`` - the file on which the test was defined

Filters
~~~~~~~

Tags can also be used to identify specific tests, which can then be
included or excluded using filters. The most common functionality is to
exclude some particular tests from running, which can be done via
:elixir:func:`ExUnit.configure/1`:

::

    # Exclude all external tests from running
    ExUnit.configure(exclude: [external: true])

From now on, ExUnit will not run any test that has the ``external`` flag
set to true. This behaviour can be reversed with the ``:include`` option
which is usually passed through the command line:

::

    mix test --include external:true

Run ``mix help test`` for more information on how to run filters via
Mix.

Another use case for tags and filters is to exclude all tests that have
a particular tag by default, regardless of its value, and include only a
certain subset:

::

    ExUnit.configure(exclude: :os, include: [os: :unix])

Keep in mind that all tests are included by default, so unless they are
excluded first, the ``include`` option has no effect.





Summary
-------

===================== =
:elixir:func:`test/3` Define a test with a string 
===================== =







Macros
------

.. elixir:macro:: ExUnit.Case.test/3
   :sig: test(message, var \\ {:_, [], ExUnit.Case}, contents)


   
   Define a test with a string.
   
   Provides a convenient macro that allows a test to be defined with a
   string. This macro automatically inserts the atom ``:ok`` as the last
   line of the test. That said, a passing test always returns ``:ok``, but,
   more importantly, it forces Elixir to not tail call optimize the test
   and therefore avoids hiding lines from the backtrace.
   
   **Examples**
   
   ::
   
       test "true is equal to true" do
         assert true == true
       end
   
   
   





