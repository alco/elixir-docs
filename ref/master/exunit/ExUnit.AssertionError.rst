ExUnit.AssertionError
==============================================================

.. elixir:module:: ExUnit.AssertionError

   :mtype: exception

Overview
--------






Summary
-------

========================== =
:elixir:func:`exception/1` Callback implementation of ``Exception.exception/1`` 

:elixir:func:`message/1`   Callback implementation of ``Exception.message/1`` 

:elixir:func:`no_value/0`  Indicates no meaningful value for a field 
========================== =



Types
-----

.. elixir:type:: ExUnit.AssertionError.t/0

   :elixir:type:`t/0` :: %ExUnit.AssertionError{__exception__: term, left: term, right: term, message: term, expr: term}
   





Functions
---------

.. elixir:function:: ExUnit.AssertionError.exception/1
   :sig: exception(args)


   Specs:
   
 
   * exception(term) :: :elixir:type:`t/0`
 

   
   Callback implementation of ``Exception.exception/1``.
   
   

.. elixir:function:: ExUnit.AssertionError.message/1
   :sig: message(exception)


   Specs:
   
 
   * message(:elixir:type:`t/0`) :: :elixir:type:`String.t/0`
 

   
   Callback implementation of ``Exception.message/1``.
   
   

.. elixir:function:: ExUnit.AssertionError.no_value/0
   :sig: no_value()


   
   Indicates no meaningful value for a field.
   
   







