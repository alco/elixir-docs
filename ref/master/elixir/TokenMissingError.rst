TokenMissingError
==============================================================

.. elixir:module:: TokenMissingError

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

.. elixir:type:: TokenMissingError.t/0

   :elixir:type:`t/0` :: %TokenMissingError{__exception__: term, file: term, line: term, description: term}
   





Functions
---------

.. elixir:function:: TokenMissingError.exception/1
   :sig: exception(args)


   Specs:
   
 
   * exception(term) :: :elixir:type:`t/0`
 

   
   Callback implementation of ``Exception.exception/1``.
   
   

.. elixir:function:: TokenMissingError.message/1
   :sig: message(exception)


   
   Callback implementation of :elixir:func:`Exception.message/1`.
   
   







