Protocol.UndefinedError
==============================================================

.. elixir:module:: Protocol.UndefinedError

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

.. elixir:type:: Protocol.UndefinedError.t/0

   :elixir:type:`t/0` :: %Protocol.UndefinedError{__exception__: term, protocol: term, value: term, description: term}
   





Functions
---------

.. elixir:function:: Protocol.UndefinedError.exception/1
   :sig: exception(args)


   Specs:
   
 
   * exception(term) :: :elixir:type:`t/0`
 

   
   Callback implementation of ``Exception.exception/1``.
   
   

.. elixir:function:: Protocol.UndefinedError.message/1
   :sig: message(exception)


   
   Callback implementation of :elixir:func:`Exception.message/1`.
   
   







