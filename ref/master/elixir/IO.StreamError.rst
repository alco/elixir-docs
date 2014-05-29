IO.StreamError
==============================================================

.. elixir:module:: IO.StreamError

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

.. elixir:type:: IO.StreamError.t/0

   :elixir:type:`t/0` :: %IO.StreamError{__exception__: term, reason: term, message: term}
   





Functions
---------

.. elixir:function:: IO.StreamError.exception/1
   :sig: exception(args)


   Specs:
   
 
   * exception(term) :: :elixir:type:`t/0`
 

   
   Callback implementation of ``Exception.exception/1``.
   
   

.. elixir:function:: IO.StreamError.message/1
   :sig: message(exception)


   Specs:
   
 
   * message(:elixir:type:`t/0`) :: :elixir:type:`String.t/0`
 

   
   Callback implementation of
   ```Exception.message/1`` <Exception.html#message/1>`__.
   
   







