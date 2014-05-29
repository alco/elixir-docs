EEx.SyntaxError
==============================================================

.. elixir:module:: EEx.SyntaxError

   :mtype: exception

Overview
--------






Summary
-------

========================== =
:elixir:func:`exception/1` Callback implementation of ``Exception.exception/1`` 

:elixir:func:`message/1`   Callback implementation of ``Exception.message/1`` 
========================== =



Types
-----

.. elixir:type:: EEx.SyntaxError.t/0

   :elixir:type:`t/0` :: %EEx.SyntaxError{__exception__: term, message: term}
   





Functions
---------

.. elixir:function:: EEx.SyntaxError.exception/1
   :sig: exception(args)


   Specs:
   
 
   * exception(term) :: :elixir:type:`t/0`
 

   
   Callback implementation of ``Exception.exception/1``.
   
   

.. elixir:function:: EEx.SyntaxError.message/1
   :sig: message(exception)


   Specs:
   
 
   * message(:elixir:type:`t/0`) :: :elixir:type:`String.t/0`
 

   
   Callback implementation of ``Exception.message/1``.
   
   







