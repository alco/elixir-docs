EEx v0.14.0-dev
===============


* Modules_


* Exceptions_




Modules
-------

=================================== =
:elixir:mod:`EEx`                   EEx stands for Embedded Elixir. It allows you to embed Elixir code inside a string in a robust way: 

:elixir:mod:`EEx.AssignsEngine`     An abstract engine that, when used with the ``TransformerEngine``, allows a developer to access assigns using ``@`` as syntax 

:elixir:mod:`EEx.Engine`            This is the basic EEx engine that ships with Elixir. An engine needs to implement three functions: 

:elixir:mod:`EEx.SmartEngine`       An engine meant for end-user usage that includes ``EEx.AssignsEngine`` and other conveniences. Read ``EEx.AssignsEngine`` for examples 

:elixir:mod:`EEx.TransformerEngine` An abstract engine that is meant to be used and built upon in other modules. This engine implements the ``EEx.Engine`` behaviour and provides a ``transform`` overridable directive that allows a developer to customize the expression returned by the engine 
=================================== =

.. toctree::
   :hidden:

   
   EEx
   
   EEx.AssignsEngine
   
   EEx.Engine
   
   EEx.SmartEngine
   
   EEx.TransformerEngine
   




Exceptions
----------

============================= =
:elixir:mod:`EEx.SyntaxError` 
============================= =

.. toctree::
   :hidden:

   
   EEx.SyntaxError
   



