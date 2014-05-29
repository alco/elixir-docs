StringIO
==============================================================

.. elixir:module:: StringIO

   :mtype: 

Overview
--------

This module provides an IO device that wraps a string.

Examples
~~~~~~~~

::

    iex> {:ok, pid} = StringIO.open("foo")
    iex> IO.read(pid, 2)
    "fo"






Summary
-------

========================= =
:elixir:func:`close/1`    Stops the IO device and returns remaining buffers 

:elixir:func:`contents/1` Returns current buffers 

:elixir:func:`open/2`     Creates an IO device 
========================= =





Functions
---------

.. elixir:function:: StringIO.close/1
   :sig: close(pid)


   Specs:
   
 
   * close(pid) :: {:ok, {binary, binary}}
 

   
   Stops the IO device and returns remaining buffers.
   
   **Examples**
   
   ::
   
       iex> {:ok, pid} = StringIO.open("in")
       iex> IO.write(pid, "out")
       iex> StringIO.close(pid)
       {:ok, {"in", "out"}}
   
   
   

.. elixir:function:: StringIO.contents/1
   :sig: contents(pid)


   Specs:
   
 
   * contents(pid) :: {binary, binary}
 

   
   Returns current buffers.
   
   **Examples**
   
   ::
   
       iex> {:ok, pid} = StringIO.open("in")
       iex> IO.write(pid, "out")
       iex> StringIO.contents(pid)
       {"in", "out"}
   
   
   

.. elixir:function:: StringIO.open/2
   :sig: open(string, options \\ [])


   Specs:
   
 
   * open(binary, :elixir:type:`Keyword.t/0`) :: {:ok, pid}
 

   
   Creates an IO device.
   
   If the ``:capture_prompt`` option is set to ``true``, prompts (specified
   as arguments to ``IO.get*`` functions) are captured.
   
   **Examples**
   
   ::
   
       iex> {:ok, pid} = StringIO.open("foo")
       iex> IO.gets(pid, ">")
       "foo"
       iex> StringIO.contents(pid)
       {"", ""}
   
       iex> {:ok, pid} = StringIO.open("foo", capture_prompt: true)
       iex> IO.gets(pid, ">")
       "foo"
       iex> StringIO.contents(pid)
       {"", ">"}
   
   
   







