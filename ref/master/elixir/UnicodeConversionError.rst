UnicodeConversionError
==============================================================

.. elixir:module:: UnicodeConversionError

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

.. elixir:type:: UnicodeConversionError.t/0

   :elixir:type:`t/0` :: %UnicodeConversionError{__exception__: term, encoded: term, message: term}
   





Functions
---------

.. elixir:function:: UnicodeConversionError.exception/1
   :sig: exception(args)


   Specs:
   
 
   * exception(term) :: :elixir:type:`t/0`
 

   
   Callback implementation of ``Exception.exception/1``.
   
   

.. elixir:function:: UnicodeConversionError.message/1
   :sig: message(exception)


   Specs:
   
 
   * message(:elixir:type:`t/0`) :: :elixir:type:`String.t/0`
 

   
   Callback implementation of :elixir:func:`Exception.message/1`.
   
   







