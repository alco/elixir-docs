EEx.AssignsEngine
==============================================================

.. elixir:module:: EEx.AssignsEngine

   :mtype: 

Overview
--------

An abstract engine that, when used with the ``TransformerEngine``,
allows a developer to access assigns using ``@`` as syntax.

This engine is included by default on the SmartEngine.

Examples
~~~~~~~~

::

    defmodule MyEngine do
      use EEx.TransformerEngine
      use EEx.AssignsEngine
    end

    iex> EEx.eval_string("<%= @foo %>", assigns: [foo: 1])
    "1"

In the example above, we can access the value ``foo`` under the binding
``assigns`` using ``@foo``. This is useful when a template, after
compiled, may receive different assigns and the developer don't want to
recompile it for each variable set.

Assigns can also be used when compiled to a function:

::

    # sample.eex
    <%= @a + @b %>

    # sample.ex
    defmodule Sample do
      require EEx
      EEx.function_from_file :def, :sample, "sample.eex", [:assigns]
    end

    # iex
    Sample.sample(a: 1, b: 2) #=> "3"














