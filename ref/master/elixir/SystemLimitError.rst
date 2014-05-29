SystemLimitError
==============================================================

.. elixir:module:: SystemLimitError

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

.. elixir:type:: SystemLimitError.t/0

   :elixir:type:`t/0` :: %SystemLimitError{__exception__: term}
   





Functions
---------

.. elixir:function:: SystemLimitError.exception/1
   :sig: exception(args)


   Specs:
   
 
   * exception(term) :: :elixir:type:`t/0`
 

   
   Callback implementation of ``Exception.exception/1``.
   
   

.. elixir:function:: SystemLimitError.message/1
   :sig: message()


   
   Callback implementation of
   ```Exception.message/1`` <Exception.html#message/1>`__.
   
   







