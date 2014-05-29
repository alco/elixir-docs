BadFunctionError
==============================================================

.. elixir:module:: BadFunctionError

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

.. elixir:type:: BadFunctionError.t/0

   :elixir:type:`t/0` :: %BadFunctionError{__exception__: term, term: term}
   





Functions
---------

.. elixir:function:: BadFunctionError.exception/1
   :sig: exception(args)


   Specs:
   
 
   * exception(term) :: :elixir:type:`t/0`
 

   
   Callback implementation of ``Exception.exception/1``.
   
   

.. elixir:function:: BadFunctionError.message/1
   :sig: message(exception)


   
   Callback implementation of :elixir:func:`Exception.message/1`.
   
   







