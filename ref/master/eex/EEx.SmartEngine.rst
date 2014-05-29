EEx.SmartEngine
==============================================================

.. elixir:module:: EEx.SmartEngine

   :mtype: 

Overview
--------

An engine meant for end-user usage that includes
```EEx.AssignsEngine`` <EEx.AssignsEngine.html>`__ and other
conveniences. Read ```EEx.AssignsEngine`` <EEx.AssignsEngine.html>`__
for examples.





Summary
-------

============================ =
:elixir:func:`handle_body/1` Callback implementation of ```EEx.Engine.handle_body/1`` <EEx.Engine.html#handle_body/1>`__ 

:elixir:func:`handle_expr/3` Callback implementation of ```EEx.Engine.handle_expr/3`` <EEx.Engine.html#handle_expr/3>`__ 

:elixir:func:`handle_text/2` Callback implementation of ```EEx.Engine.handle_text/2`` <EEx.Engine.html#handle_text/2>`__ 
============================ =





Functions
---------

.. elixir:function:: EEx.SmartEngine.handle_body/1
   :sig: handle_body(body)


   
   Callback implementation of
   ```EEx.Engine.handle_body/1`` <EEx.Engine.html#handle_body/1>`__.
   
   

.. elixir:function:: EEx.SmartEngine.handle_expr/3
   :sig: handle_expr(buffer, mark, expr)


   
   Callback implementation of
   ```EEx.Engine.handle_expr/3`` <EEx.Engine.html#handle_expr/3>`__.
   
   

.. elixir:function:: EEx.SmartEngine.handle_text/2
   :sig: handle_text(buffer, text)


   
   Callback implementation of
   ```EEx.Engine.handle_text/2`` <EEx.Engine.html#handle_text/2>`__.
   
   







