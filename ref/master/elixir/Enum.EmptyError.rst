Enum.EmptyError
==============================================================

.. elixir:module:: Enum.EmptyError

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

.. elixir:type:: Enum.EmptyError.t/0

   :elixir:type:`t/0` :: %Enum.EmptyError{__exception__: term}
   





Functions
---------

.. elixir:function:: Enum.EmptyError.exception/1
   :sig: exception(args)


   Specs:
   
 
   * exception(term) :: :elixir:type:`t/0`
 

   
   Callback implementation of ``Exception.exception/1``.
   
   

.. elixir:function:: Enum.EmptyError.message/1
   :sig: message()


   
   Callback implementation of :elixir:func:`Exception.message/1`.
   
   







