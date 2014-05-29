File.CopyError
==============================================================

.. elixir:module:: File.CopyError

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

.. elixir:type:: File.CopyError.t/0

   :elixir:type:`t/0` :: %File.CopyError{__exception__: term, reason: term, action: term, source: term, destination: term, on: term}
   





Functions
---------

.. elixir:function:: File.CopyError.exception/1
   :sig: exception(args)


   Specs:
   
 
   * exception(term) :: :elixir:type:`t/0`
 

   
   Callback implementation of ``Exception.exception/1``.
   
   

.. elixir:function:: File.CopyError.message/1
   :sig: message(exception)


   
   Callback implementation of
   ```Exception.message/1`` <Exception.html#message/1>`__.
   
   







