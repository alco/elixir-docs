ErlangError
==============================================================

.. elixir:module:: ErlangError

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

.. elixir:type:: ErlangError.t/0

   :elixir:type:`t/0` :: %ErlangError{__exception__: term, original: term}
   





Functions
---------

.. elixir:function:: ErlangError.exception/1
   :sig: exception(args)


   Specs:
   
 
   * exception(term) :: :elixir:type:`t/0`
 

   
   Callback implementation of ``Exception.exception/1``.
   
   

.. elixir:function:: ErlangError.message/1
   :sig: message(exception)


   
   Callback implementation of
   ```Exception.message/1`` <Exception.html#message/1>`__.
   
   







