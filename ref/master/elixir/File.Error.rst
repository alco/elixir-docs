File.Error
==============================================================

.. elixir:module:: File.Error

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

.. elixir:type:: File.Error.t/0

   :elixir:type:`t/0` :: %File.Error{__exception__: term, reason: term, action: term, path: term}
   





Functions
---------

.. elixir:function:: File.Error.exception/1
   :sig: exception(args)


   Specs:
   
 
   * exception(term) :: :elixir:type:`t/0`
 

   
   Callback implementation of ``Exception.exception/1``.
   
   

.. elixir:function:: File.Error.message/1
   :sig: message(exception)


   
   Callback implementation of
   ```Exception.message/1`` <Exception.html#message/1>`__.
   
   







