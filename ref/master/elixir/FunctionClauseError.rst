FunctionClauseError
==============================================================

.. elixir:module:: FunctionClauseError

   :mtype: exception

Overview
--------






Summary
-------

========================== =
:elixir:func:`exception/1` Callback implementation of ``Exception.exception/1`` 

:elixir:func:`message/1`   Callback implementation of :elixir:func:`Exception.message/1` 
========================== =



Types
-----

.. elixir:type:: FunctionClauseError.t/0

   :elixir:type:`t/0` :: %FunctionClauseError{__exception__: term, module: term, function: term, arity: term}
   





Functions
---------

.. elixir:function:: FunctionClauseError.exception/1
   :sig: exception(args)


   Specs:
   
 
   * exception(term) :: :elixir:type:`t/0`
 

   
   Callback implementation of ``Exception.exception/1``.
   
   

.. elixir:function:: FunctionClauseError.message/1
   :sig: message(exception)


   
   Callback implementation of :elixir:func:`Exception.message/1`.
   
   







