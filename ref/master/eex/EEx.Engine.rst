EEx.Engine
==============================================================

.. elixir:module:: EEx.Engine

   :mtype: behaviour

Overview
--------

This is the basic EEx engine that ships with Elixir. An engine needs to
implement three functions:

-  ``handle_body(quoted)`` - receives the final built quoted expression,
   should do final post-processing and return a quoted expression;

-  ``handle_text(buffer, text)`` - it receives the buffer, the text and
   must return a new quoted expression;

-  ``handle_expr(buffer, marker, expr)`` - it receives the buffer, the
   marker, the expr and must return a new quoted expression;

The marker is what follows exactly after ``<%``. For example,
``<% foo %>`` has an empty marker, but ``<%= foo %>`` has ``"="`` as
marker. The allowed markers so far are:

-  ``""``
-  ``"="``

Read ```handle_expr/3`` <#handle_expr/3>`__ below for more information
about the markers implemented by default by this engine.





Summary
-------

============================ =
:elixir:func:`handle_body/1` The default implementation implementation simply returns the given expression 

:elixir:func:`handle_expr/3` Implements expressions according to the markers 

:elixir:func:`handle_text/2` The default implementation simply concatenates text to the buffer 
============================ =





Functions
---------

.. elixir:function:: EEx.Engine.handle_body/1
   :sig: handle_body(quoted)


   
   The default implementation implementation simply returns the given
   expression.
   
   

.. elixir:function:: EEx.Engine.handle_expr/3
   :sig: handle_expr(buffer, binary2, expr)


   
   Implements expressions according to the markers.
   
   ::
   
       <% Elixir expression - inline with output %>
       <%= Elixir expression - replace with result %>
   
   All other markers are not implemented by this engine.
   
   

.. elixir:function:: EEx.Engine.handle_text/2
   :sig: handle_text(buffer, text)


   
   The default implementation simply concatenates text to the buffer.
   
   







Callbacks
---------

.. elixir:callback:: EEx.Engine.handle_body/1
   :sig: handle_body/1


   Specs:
   
 
   * handle_body(:elixir:type:`Macro.t/0`) :: :elixir:type:`Macro.t/0`
 

   
   
   

.. elixir:callback:: EEx.Engine.handle_expr/3
   :sig: handle_expr/3


   Specs:
   
 
   * handle_expr(:elixir:type:`Macro.t/0`, binary, :elixir:type:`Macro.t/0`) :: :elixir:type:`Macro.t/0`
 

   
   
   

.. elixir:callback:: EEx.Engine.handle_text/2
   :sig: handle_text/2


   Specs:
   
 
   * handle_text(:elixir:type:`Macro.t/0`, binary) :: :elixir:type:`Macro.t/0`
 

   
   
   



