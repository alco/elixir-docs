Mix.NoProjectError
==============================================================

.. elixir:module:: Mix.NoProjectError

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

.. elixir:type:: Mix.NoProjectError.t/0

   :elixir:type:`t/0` :: %Mix.NoProjectError{__exception__: term, mix_error: term, message: term}
   





Functions
---------

.. elixir:function:: Mix.NoProjectError.exception/1
   :sig: exception(args)


   Specs:
   
 
   * exception(term) :: :elixir:type:`t/0`
 

   
   Callback implementation of ``Exception.exception/1``.
   
   

.. elixir:function:: Mix.NoProjectError.message/1
   :sig: message(exception)


   Specs:
   
 
   * message(:elixir:type:`t/0`) :: :elixir:type:`String.t/0`
 

   
   Callback implementation of ``Exception.message/1``.
   
   







