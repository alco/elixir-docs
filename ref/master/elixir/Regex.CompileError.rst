Regex.CompileError
==============================================================

.. elixir:module:: Regex.CompileError

   :mtype: exception

Overview
--------






Summary
-------

========================== =
:elixir:func:`exception/1` Callback implementation of ``Exception.exception/1`` 

:elixir:func:`message/1`   Callback implementation of :elixir:func:`Exception.message/1` 
========================== =



Types
-----

.. elixir:type:: Regex.CompileError.t/0

   :elixir:type:`t/0` :: %Regex.CompileError{__exception__: term, message: term}
   





Functions
---------

.. elixir:function:: Regex.CompileError.exception/1
   :sig: exception(args)


   Specs:
   
 
   * exception(term) :: :elixir:type:`t/0`
 

   
   Callback implementation of ``Exception.exception/1``.
   
   

.. elixir:function:: Regex.CompileError.message/1
   :sig: message(exception)


   Specs:
   
 
   * message(:elixir:type:`t/0`) :: :elixir:type:`String.t/0`
 

   
   Callback implementation of :elixir:func:`Exception.message/1`.
   
   







