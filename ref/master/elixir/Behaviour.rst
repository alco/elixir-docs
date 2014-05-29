Behaviour
==============================================================

.. elixir:module:: Behaviour

   :mtype: 

Overview
--------

Utilities for defining behaviour interfaces.

Behaviours can be referenced by other modules to ensure they implement
required callbacks.

For example, you can specify the ``URI.Parser`` behaviour as follows:

::

    defmodule URI.Parser do
      use Behaviour

      @doc "Parses the given URL"
      defcallback parse(uri_info :: URI.t) :: URI.t

      @doc "Defines a default port"
      defcallback default_port() :: integer
    end

And then a module may use it as:

::

    defmodule URI.HTTP do
      @behaviour URI.Parser
      def default_port(), do: 80
      def parse(info), do: info
    end

If the behaviour changes or ``URI.HTTP`` does not implement one of the
callbacks, a warning will be raised.

Implementation
~~~~~~~~~~~~~~

Since Erlang R15, behaviours must be defined via ``@callback``
attributes. ``defcallback`` is a simple mechanism that defines the
``@callback`` attribute according to the given type specification.
``defcallback`` allows documentation to be created for the callback and
defines a custom function signature.

The callbacks and their documentation can be retrieved via the
``__behaviour__`` callback function.





Summary
-------

================================== =
:elixir:macro:`defcallback/1`      Define a function callback according to the given type specification 

:elixir:macro:`defmacrocallback/1` Define a macro callback according to the given type specification 
================================== =







Macros
------

.. elixir:macro:: Behaviour.defcallback/1
   :sig: defcallback(spec)


   
   Define a function callback according to the given type specification.
   
   

.. elixir:macro:: Behaviour.defmacrocallback/1
   :sig: defmacrocallback(spec)


   
   Define a macro callback according to the given type specification.
   
   





