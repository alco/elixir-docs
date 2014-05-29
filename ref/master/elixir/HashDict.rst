HashDict
==============================================================

.. elixir:module:: HashDict

   :mtype: 

Overview
--------

A key-value store.

The ```HashDict`` <HashDict.html>`__ is represented internally as a
struct, therefore ``%HashDict{}`` can be used whenever there is a need
to match on any ```HashDict`` <HashDict.html>`__. Note though the struct
fields are private and must not be accessed directly. Instead, use the
functions on this or in the ```Dict`` <Dict.html>`__ module.

Implementation-wise, ```HashDict`` <HashDict.html>`__ is implemented
using tries, which grows in space as the number of keys grows, working
well with both small and large set of keys. For more information about
the functions and their APIs, please consult the
```Dict`` <Dict.html>`__ module.





Summary
-------

========================= =
:elixir:func:`delete/2`   Callback implementation of ```Dict.delete/2`` <Dict.html#delete/2>`__ 

:elixir:func:`drop/2`     Callback implementation of ```Dict.drop/2`` <Dict.html#drop/2>`__ 

:elixir:func:`equal?/2`   Callback implementation of ```Dict.equal?/2`` <Dict.html#equal?/2>`__ 

:elixir:func:`fetch!/2`   Callback implementation of ```Dict.fetch!/2`` <Dict.html#fetch!/2>`__ 

:elixir:func:`fetch/2`    Callback implementation of ```Dict.fetch/2`` <Dict.html#fetch/2>`__ 

:elixir:func:`get/3`      Callback implementation of ```Dict.get/3`` <Dict.html#get/3>`__ 

:elixir:func:`has_key?/2` Callback implementation of ```Dict.has_key?/2`` <Dict.html#has_key?/2>`__ 

:elixir:func:`keys/1`     Callback implementation of ```Dict.keys/1`` <Dict.html#keys/1>`__ 

:elixir:func:`merge/3`    Callback implementation of ```Dict.merge/3`` <Dict.html#merge/3>`__ 

:elixir:func:`new/0`      Creates a new empty dict 

:elixir:func:`pop/3`      Callback implementation of ```Dict.pop/3`` <Dict.html#pop/3>`__ 

:elixir:func:`put/3`      Callback implementation of ```Dict.put/3`` <Dict.html#put/3>`__ 

:elixir:func:`put_new/3`  Callback implementation of ```Dict.put_new/3`` <Dict.html#put_new/3>`__ 

:elixir:func:`size/1`     Callback implementation of ```Dict.size/1`` <Dict.html#size/1>`__ 

:elixir:func:`split/2`    Callback implementation of ```Dict.split/2`` <Dict.html#split/2>`__ 

:elixir:func:`take/2`     Callback implementation of ```Dict.take/2`` <Dict.html#take/2>`__ 

:elixir:func:`to_list/1`  Callback implementation of ```Dict.to_list/1`` <Dict.html#to_list/1>`__ 

:elixir:func:`update!/3`  Callback implementation of ```Dict.update!/3`` <Dict.html#update!/3>`__ 

:elixir:func:`update/4`   Callback implementation of ```Dict.update/4`` <Dict.html#update/4>`__ 

:elixir:func:`values/1`   Callback implementation of ```Dict.values/1`` <Dict.html#values/1>`__ 
========================= =



Types
-----

.. elixir:type:: HashDict.t/0

   :elixir:type:`t/0`
   





Functions
---------

.. elixir:function:: HashDict.delete/2
   :sig: delete(dict, key)


   
   Callback implementation of ```Dict.delete/2`` <Dict.html#delete/2>`__.
   
   

.. elixir:function:: HashDict.drop/2
   :sig: drop(dict, keys)


   
   Callback implementation of ```Dict.drop/2`` <Dict.html#drop/2>`__.
   
   

.. elixir:function:: HashDict.equal?/2
   :sig: equal?(dict1, dict2)


   
   Callback implementation of ```Dict.equal?/2`` <Dict.html#equal?/2>`__.
   
   

.. elixir:function:: HashDict.fetch/2
   :sig: fetch(hashdict, key)


   
   Callback implementation of ```Dict.fetch/2`` <Dict.html#fetch/2>`__.
   
   

.. elixir:function:: HashDict.fetch!/2
   :sig: fetch!(dict, key)


   
   Callback implementation of ```Dict.fetch!/2`` <Dict.html#fetch!/2>`__.
   
   

.. elixir:function:: HashDict.get/3
   :sig: get(dict, key, default \\ nil)


   
   Callback implementation of ```Dict.get/3`` <Dict.html#get/3>`__.
   
   

.. elixir:function:: HashDict.has_key?/2
   :sig: has_key?(dict, key)


   
   Callback implementation of
   ```Dict.has_key?/2`` <Dict.html#has_key?/2>`__.
   
   

.. elixir:function:: HashDict.keys/1
   :sig: keys(dict)


   
   Callback implementation of ```Dict.keys/1`` <Dict.html#keys/1>`__.
   
   

.. elixir:function:: HashDict.merge/3
   :sig: merge(dict1, dict2, fun \\ fn _k, _v1, v2 -> v2 end)


   
   Callback implementation of ```Dict.merge/3`` <Dict.html#merge/3>`__.
   
   

.. elixir:function:: HashDict.new/0
   :sig: new()


   Specs:
   
 
   * new :: :elixir:type:`Dict.t/0`
 

   
   Creates a new empty dict.
   
   

.. elixir:function:: HashDict.pop/3
   :sig: pop(dict, key, default \\ nil)


   
   Callback implementation of ```Dict.pop/3`` <Dict.html#pop/3>`__.
   
   

.. elixir:function:: HashDict.put/3
   :sig: put(hashdict, key, value)


   
   Callback implementation of ```Dict.put/3`` <Dict.html#put/3>`__.
   
   

.. elixir:function:: HashDict.put_new/3
   :sig: put_new(dict, key, value)


   
   Callback implementation of ```Dict.put_new/3`` <Dict.html#put_new/3>`__.
   
   

.. elixir:function:: HashDict.size/1
   :sig: size(hashdict)


   
   Callback implementation of ```Dict.size/1`` <Dict.html#size/1>`__.
   
   

.. elixir:function:: HashDict.split/2
   :sig: split(dict, keys)


   
   Callback implementation of ```Dict.split/2`` <Dict.html#split/2>`__.
   
   

.. elixir:function:: HashDict.take/2
   :sig: take(dict, keys)


   
   Callback implementation of ```Dict.take/2`` <Dict.html#take/2>`__.
   
   

.. elixir:function:: HashDict.to_list/1
   :sig: to_list(dict)


   
   Callback implementation of ```Dict.to_list/1`` <Dict.html#to_list/1>`__.
   
   

.. elixir:function:: HashDict.update/4
   :sig: update(dict, key, initial, fun)


   
   Callback implementation of ```Dict.update/4`` <Dict.html#update/4>`__.
   
   

.. elixir:function:: HashDict.update!/3
   :sig: update!(dict, key, fun)


   
   Callback implementation of ```Dict.update!/3`` <Dict.html#update!/3>`__.
   
   

.. elixir:function:: HashDict.values/1
   :sig: values(dict)


   
   Callback implementation of ```Dict.values/1`` <Dict.html#values/1>`__.
   
   







