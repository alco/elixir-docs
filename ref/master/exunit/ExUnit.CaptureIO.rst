ExUnit.CaptureIO
==============================================================

.. elixir:module:: ExUnit.CaptureIO

   :mtype: 

Overview
--------

Functionality to capture IO for testing.

Examples
~~~~~~~~

::

    defmodule AssertionTest do
      use ExUnit.Case

      import ExUnit.CaptureIO

      test :example do
        assert capture_io(fn ->
          IO.puts "a"
        end) == "a\n"
      end
    end






Summary
-------

=========================== =
:elixir:func:`capture_io/1` Captures IO generated when evaluating ``fun`` 

:elixir:func:`capture_io/2` 

:elixir:func:`capture_io/3` 
=========================== =





Functions
---------

.. elixir:function:: ExUnit.CaptureIO.capture_io/1
   :sig: capture_io(fun)


   
   Captures IO generated when evaluating ``fun``.
   
   Returns the binary which is the captured output.
   
   By default, ``capture_io`` replaces the ``group_leader`` (``:stdio``)
   for the current process. However, the capturing of any other named
   device, such as ``:stderr``, is also possible globally by giving the
   registered device name explicitly as an argument.
   
   Note that when capturing something other than ``:stdio``, the test
   should run with async false.
   
   When capturing ``:stdio``, if the ``:capture_prompt`` option is
   ``false``, prompts (specified as arguments to ``IO.get*`` functions) are
   not captured.
   
   A developer can set a string as an input. The default input is ``:eof``.
   
   **Examples**
   
   ::
   
       iex> capture_io(fn -> IO.write "josé" end) == "josé"
       true
   
       iex> capture_io(:stderr, fn -> IO.write(:stderr, "josé") end) == "josé"
       true
   
       iex> capture_io("this is input", fn ->
       ...>   input = IO.gets ">"
       ...>   IO.write input
       ...> end) == ">this is input"
       true
   
       iex> capture_io([input: "this is input", capture_prompt: false], fn ->
       ...>   input = IO.gets ">"
       ...>   IO.write input
       ...> end) == "this is input"
       true
   
   
   

.. elixir:function:: ExUnit.CaptureIO.capture_io/2
   :sig: capture_io(device, fun)


   
   
   

.. elixir:function:: ExUnit.CaptureIO.capture_io/3
   :sig: capture_io(device, input, fun)


   
   
   







