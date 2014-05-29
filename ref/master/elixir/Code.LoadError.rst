Code.LoadError
==============================================================

.. elixir:module:: Code.LoadError

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

.. elixir:type:: Code.LoadError.t/0

   :elixir:type:`t/0` :: %Code.LoadError{__exception__: term, file: term, message: term}
   





Functions
---------

.. elixir:function:: Code.LoadError.exception/1
   :sig: exception(args)


   Specs:
   
 
   * exception(term) :: :elixir:type:`t/0`
 

   
   Callback implementation of ``Exception.exception/1``.
   
   

.. elixir:function:: Code.LoadError.message/1
   :sig: message(exception)


   Specs:
   
 
   * message(:elixir:type:`t/0`) :: :elixir:type:`String.t/0`
 

   
   Callback implementation of
   ```Exception.message/1`` <Exception.html#message/1>`__.
   
   







