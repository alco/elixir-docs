ExUnit.DocTest.Error
==============================================================

.. elixir:module:: ExUnit.DocTest.Error

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

.. elixir:type:: ExUnit.DocTest.Error.t/0

   :elixir:type:`t/0` :: %ExUnit.DocTest.Error{__exception__: term, message: term}
   





Functions
---------

.. elixir:function:: ExUnit.DocTest.Error.exception/1
   :sig: exception(args)


   Specs:
   
 
   * exception(term) :: :elixir:type:`t/0`
 

   
   Callback implementation of ``Exception.exception/1``.
   
   

.. elixir:function:: ExUnit.DocTest.Error.message/1
   :sig: message(exception)


   Specs:
   
 
   * message(:elixir:type:`t/0`) :: :elixir:type:`String.t/0`
 

   
   Callback implementation of ``Exception.message/1``.
   
   







