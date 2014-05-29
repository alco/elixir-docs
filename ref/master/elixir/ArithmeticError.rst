ArithmeticError
==============================================================

.. elixir:module:: ArithmeticError

   :mtype: exception

Overview
--------






Summary
-------

========================== =
:elixir:func:`exception/1` Callback implementation of ``Exception.exception/1`` 

:elixir:func:`message/1`   Callback implementation of ```Exception.message/1`` <Exception.html#message/1>`__ 
========================== =



Types
-----

.. elixir:type:: ArithmeticError.t/0

   :elixir:type:`t/0` :: %ArithmeticError{__exception__: term}
   





Functions
---------

.. elixir:function:: ArithmeticError.exception/1
   :sig: exception(args)


   Specs:
   
 
   * exception(term) :: :elixir:type:`t/0`
 

   
   Callback implementation of ``Exception.exception/1``.
   
   

.. elixir:function:: ArithmeticError.message/1
   :sig: message()


   
   Callback implementation of
   ```Exception.message/1`` <Exception.html#message/1>`__.
   
   







