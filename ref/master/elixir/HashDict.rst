HashDict
==============================================================

.. elixir:module:: HashDict

   :mtype: 

Overview
--------

A key-value store.

The :elixir:mod:`HashDict` is represented internally as a struct, therefore
``%HashDict{}`` can be used whenever there is a need to match on any
:elixir:mod:`HashDict`. Note though the struct fields are private and must not be
accessed directly. Instead, use the functions on this or in the :elixir:mod:`Dict`
module.

Implementation-wise, :elixir:mod:`HashDict` is implemented using tries, which
grows in space as the number of keys grows, working well with both small
and large set of keys. For more information about the functions and
their APIs, please consult the :elixir:mod:`Dict` module.





Summary
-------

========================= =
:elixir:func:`delete/2`   Callback implementation of :elixir:func:`Dict.delete/2` 

:elixir:func:`drop/2`     Callback implementation of :elixir:func:`Dict.drop/2` 

:elixir:func:`equal?/2`   Callback implementation of :elixir:func:`Dict.equal?/2` 

:elixir:func:`fetch!/2`   Callback implementation of :elixir:func:`Dict.fetch!/2` 

:elixir:func:`fetch/2`    Callback implementation of :elixir:func:`Dict.fetch/2` 

:elixir:func:`get/3`      Callback implementation of :elixir:func:`Dict.get/3` 

:elixir:func:`has_key?/2` Callback implementation of :elixir:func:`Dict.has_key?/2` 

:elixir:func:`keys/1`     Callback implementation of :elixir:func:`Dict.keys/1` 

:elixir:func:`merge/3`    Callback implementation of :elixir:func:`Dict.merge/3` 

:elixir:func:`new/0`      Creates a new empty dict 

:elixir:func:`pop/3`      Callback implementation of :elixir:func:`Dict.pop/3` 

:elixir:func:`put/3`      Callback implementation of :elixir:func:`Dict.put/3` 

:elixir:func:`put_new/3`  Callback implementation of :elixir:func:`Dict.put_new/3` 

:elixir:func:`size/1`     Callback implementation of :elixir:func:`Dict.size/1` 

:elixir:func:`split/2`    Callback implementation of :elixir:func:`Dict.split/2` 

:elixir:func:`take/2`     Callback implementation of :elixir:func:`Dict.take/2` 

:elixir:func:`to_list/1`  Callback implementation of :elixir:func:`Dict.to_list/1` 

:elixir:func:`update!/3`  Callback implementation of :elixir:func:`Dict.update!/3` 

:elixir:func:`update/4`   Callback implementation of :elixir:func:`Dict.update/4` 

:elixir:func:`values/1`   Callback implementation of :elixir:func:`Dict.values/1` 
========================= =



Types
-----

.. elixir:type:: HashDict.t/0

   :elixir:type:`t/0`
   





Functions
---------

.. elixir:function:: HashDict.delete/2
   :sig: delete(dict, key)


   
   Callback implementation of :elixir:func:`Dict.delete/2`.
   
   

.. elixir:function:: HashDict.drop/2
   :sig: drop(dict, keys)


   
   Callback implementation of :elixir:func:`Dict.drop/2`.
   
   

.. elixir:function:: HashDict.equal?/2
   :sig: equal?(dict1, dict2)


   
   Callback implementation of :elixir:func:`Dict.equal?/2`.
   
   

.. elixir:function:: HashDict.fetch/2
   :sig: fetch(hashdict, key)


   
   Callback implementation of :elixir:func:`Dict.fetch/2`.
   
   

.. elixir:function:: HashDict.fetch!/2
   :sig: fetch!(dict, key)


   
   Callback implementation of :elixir:func:`Dict.fetch!/2`.
   
   

.. elixir:function:: HashDict.get/3
   :sig: get(dict, key, default \\ nil)


   
   Callback implementation of :elixir:func:`Dict.get/3`.
   
   

.. elixir:function:: HashDict.has_key?/2
   :sig: has_key?(dict, key)


   
   Callback implementation of :elixir:func:`Dict.has_key?/2`.
   
   

.. elixir:function:: HashDict.keys/1
   :sig: keys(dict)


   
   Callback implementation of :elixir:func:`Dict.keys/1`.
   
   

.. elixir:function:: HashDict.merge/3
   :sig: merge(dict1, dict2, fun \\ fn _k, _v1, v2 -> v2 end)


   
   Callback implementation of :elixir:func:`Dict.merge/3`.
   
   

.. elixir:function:: HashDict.new/0
   :sig: new()


   Specs:
   
 
   * new :: :elixir:type:`Dict.t/0`
 

   
   Creates a new empty dict.
   
   

.. elixir:function:: HashDict.pop/3
   :sig: pop(dict, key, default \\ nil)


   
   Callback implementation of :elixir:func:`Dict.pop/3`.
   
   

.. elixir:function:: HashDict.put/3
   :sig: put(hashdict, key, value)


   
   Callback implementation of :elixir:func:`Dict.put/3`.
   
   

.. elixir:function:: HashDict.put_new/3
   :sig: put_new(dict, key, value)


   
   Callback implementation of :elixir:func:`Dict.put_new/3`.
   
   

.. elixir:function:: HashDict.size/1
   :sig: size(hashdict)


   
   Callback implementation of :elixir:func:`Dict.size/1`.
   
   

.. elixir:function:: HashDict.split/2
   :sig: split(dict, keys)


   
   Callback implementation of :elixir:func:`Dict.split/2`.
   
   

.. elixir:function:: HashDict.take/2
   :sig: take(dict, keys)


   
   Callback implementation of :elixir:func:`Dict.take/2`.
   
   

.. elixir:function:: HashDict.to_list/1
   :sig: to_list(dict)


   
   Callback implementation of :elixir:func:`Dict.to_list/1`.
   
   

.. elixir:function:: HashDict.update/4
   :sig: update(dict, key, initial, fun)


   
   Callback implementation of :elixir:func:`Dict.update/4`.
   
   

.. elixir:function:: HashDict.update!/3
   :sig: update!(dict, key, fun)


   
   Callback implementation of :elixir:func:`Dict.update!/3`.
   
   

.. elixir:function:: HashDict.values/1
   :sig: values(dict)


   
   Callback implementation of :elixir:func:`Dict.values/1`.
   
   







