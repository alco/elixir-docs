Map
==============================================================

.. elixir:module:: Map

   :mtype: 

Overview
--------

A Dict implementation that works on maps.

Maps are key-value stores where keys are compared using the match
operator (``===``). Maps can be created with the ``%{}`` special form
defined in the :elixir:mod:`Kernel.SpecialForms` module.

For more information about the functions in this module and their APIs,
please consult the :elixir:mod:`Dict` module.





Summary
-------

========================= =
:elixir:func:`delete/2`   Callback implementation of :elixir:func:`Dict.delete/2` 

:elixir:func:`drop/2`     Callback implementation of :elixir:func:`Dict.drop/2` 

:elixir:func:`equal?/2`   Callback implementation of :elixir:func:`Dict.equal?/2` 

:elixir:func:`fetch\!/2`  Callback implementation of :elixir:func:`Dict.fetch!/2` 

:elixir:func:`fetch/2`    Callback implementation of :elixir:func:`Dict.fetch/2` 

:elixir:func:`get/3`      Callback implementation of :elixir:func:`Dict.get/3` 

:elixir:func:`has_key?/2` Callback implementation of :elixir:func:`Dict.has_key?/2` 

:elixir:func:`keys/1`     Callback implementation of :elixir:func:`Dict.keys/1` 

:elixir:func:`merge/2`    Callback implementation of :elixir:func:`Dict.merge/2` 

:elixir:func:`merge/3`    Callback implementation of :elixir:func:`Dict.merge/3` 

:elixir:func:`new/0`      Returns a new empty map 

:elixir:func:`pop/3`      Callback implementation of :elixir:func:`Dict.pop/3` 

:elixir:func:`put/3`      Callback implementation of :elixir:func:`Dict.put/3` 

:elixir:func:`put_new/3`  Callback implementation of :elixir:func:`Dict.put_new/3` 

:elixir:func:`size/1`     Callback implementation of :elixir:func:`Dict.size/1` 

:elixir:func:`split/2`    Callback implementation of :elixir:func:`Dict.split/2` 

:elixir:func:`take/2`     Callback implementation of :elixir:func:`Dict.take/2` 

:elixir:func:`to_list/1`  Callback implementation of :elixir:func:`Dict.to_list/1` 

:elixir:func:`update\!/3` Callback implementation of :elixir:func:`Dict.update!/3` 

:elixir:func:`update/4`   Callback implementation of :elixir:func:`Dict.update/4` 

:elixir:func:`values/1`   Callback implementation of :elixir:func:`Dict.values/1` 
========================= =





Functions
---------

.. elixir:function:: Map.delete/2
   :sig: delete(map, key)


   
   Callback implementation of :elixir:func:`Dict.delete/2`.
   
   

.. elixir:function:: Map.drop/2
   :sig: drop(dict, keys)


   
   Callback implementation of :elixir:func:`Dict.drop/2`.
   
   

.. elixir:function:: Map.equal?/2
   :sig: equal?(dict1, dict2)


   
   Callback implementation of :elixir:func:`Dict.equal?/2`.
   
   

.. elixir:function:: Map.fetch/2
   :sig: fetch(map, key)


   
   Callback implementation of :elixir:func:`Dict.fetch/2`.
   
   

.. elixir:function:: Map.fetch!/2
   :sig: fetch!(dict, key)


   
   Callback implementation of :elixir:func:`Dict.fetch!/2`.
   
   

.. elixir:function:: Map.get/3
   :sig: get(dict, key, default \\ nil)


   
   Callback implementation of :elixir:func:`Dict.get/3`.
   
   

.. elixir:function:: Map.has_key?/2
   :sig: has_key?(dict, key)


   
   Callback implementation of :elixir:func:`Dict.has_key?/2`.
   
   

.. elixir:function:: Map.keys/1
   :sig: keys(dict)


   
   Callback implementation of :elixir:func:`Dict.keys/1`.
   
   

.. elixir:function:: Map.merge/2
   :sig: merge(map1, map2)


   
   Callback implementation of :elixir:func:`Dict.merge/2`.
   
   

.. elixir:function:: Map.merge/3
   :sig: merge(dict1, dict2, fun \\ fn _k, _v1, v2 -> v2 end)


   
   Callback implementation of :elixir:func:`Dict.merge/3`.
   
   

.. elixir:function:: Map.new/0
   :sig: new()


   
   Returns a new empty map.
   
   

.. elixir:function:: Map.pop/3
   :sig: pop(dict, key, default \\ nil)


   
   Callback implementation of :elixir:func:`Dict.pop/3`.
   
   

.. elixir:function:: Map.put/3
   :sig: put(map, key, val)


   
   Callback implementation of :elixir:func:`Dict.put/3`.
   
   

.. elixir:function:: Map.put_new/3
   :sig: put_new(dict, key, value)


   
   Callback implementation of :elixir:func:`Dict.put_new/3`.
   
   

.. elixir:function:: Map.size/1
   :sig: size(map)


   
   Callback implementation of :elixir:func:`Dict.size/1`.
   
   

.. elixir:function:: Map.split/2
   :sig: split(dict, keys)


   
   Callback implementation of :elixir:func:`Dict.split/2`.
   
   

.. elixir:function:: Map.take/2
   :sig: take(dict, keys)


   
   Callback implementation of :elixir:func:`Dict.take/2`.
   
   

.. elixir:function:: Map.to_list/1
   :sig: to_list(dict)


   
   Callback implementation of :elixir:func:`Dict.to_list/1`.
   
   

.. elixir:function:: Map.update/4
   :sig: update(dict, key, initial, fun)


   
   Callback implementation of :elixir:func:`Dict.update/4`.
   
   

.. elixir:function:: Map.update!/3
   :sig: update!(dict, key, fun)


   
   Callback implementation of :elixir:func:`Dict.update!/3`.
   
   

.. elixir:function:: Map.values/1
   :sig: values(dict)


   
   Callback implementation of :elixir:func:`Dict.values/1`.
   
   







