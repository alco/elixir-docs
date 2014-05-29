EEx.SmartEngine
==============================================================

.. elixir:module:: EEx.SmartEngine

   :mtype: 

Overview
--------

An engine meant for end-user usage that includes :elixir:mod:`EEx.AssignsEngine`
and other conveniences. Read :elixir:mod:`EEx.AssignsEngine` for examples.





Summary
-------

============================ =
:elixir:func:`handle_body/1` Callback implementation of :elixir:func:`EEx.Engine.handle_body/1` 

:elixir:func:`handle_expr/3` Callback implementation of :elixir:func:`EEx.Engine.handle_expr/3` 

:elixir:func:`handle_text/2` Callback implementation of :elixir:func:`EEx.Engine.handle_text/2` 
============================ =





Functions
---------

.. elixir:function:: EEx.SmartEngine.handle_body/1
   :sig: handle_body(body)


   
   Callback implementation of :elixir:func:`EEx.Engine.handle_body/1`.
   
   

.. elixir:function:: EEx.SmartEngine.handle_expr/3
   :sig: handle_expr(buffer, mark, expr)


   
   Callback implementation of :elixir:func:`EEx.Engine.handle_expr/3`.
   
   

.. elixir:function:: EEx.SmartEngine.handle_text/2
   :sig: handle_text(buffer, text)


   
   Callback implementation of :elixir:func:`EEx.Engine.handle_text/2`.
   
   







