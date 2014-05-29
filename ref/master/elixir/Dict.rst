Dict
==============================================================

.. elixir:module:: Dict

   :mtype: behaviour

Overview
--------

This module specifies the Dict API expected to be implemented by
different dictionaries. It also provides functions that redirect to the
underlying Dict, allowing a developer to work with different Dict
implementations using one API.

To create a new dict, use the ``new`` functions defined by each dict
type:

::

    HashDict.new  #=> creates an empty HashDict

In the examples below, ``dict_impl`` means a specific
```Dict`` <Dict.html>`__ implementation, for example
```HashDict`` <HashDict.html>`__ or ```Map`` <Map.html>`__.

Protocols
~~~~~~~~~

Besides implementing the functions in this module, all dictionaries are
required to implement the ```Access`` <Access.html>`__ protocol:

::

    iex> dict = dict_impl.new
    iex> dict = Dict.put(dict, :hello, :world)
    iex> dict[:hello]
    :world

As well as the ```Enumerable`` <Enumerable.html>`__ and
```Collectable`` <Collectable.html>`__ protocols.

Match
~~~~~

Dictionaries are required to implement all operations using the match
(``===``) operator.

Default implementation
~~~~~~~~~~~~~~~~~~~~~~

Default implementations for some functions in the
```Dict`` <Dict.html>`__ module are provided via ``use Dict``.

For example:

::

    defmodule MyDict do
      use Dict

      # implement required functions (see below)
      # override default implementations if optimization
      # is needed
    end

The client module must contain the following functions:

-  ```delete/2`` <#delete/2>`__
-  ```fetch/2`` <#fetch/2>`__
-  ```put/3`` <#put/3>`__
-  ``reduce/3``
-  ```size/1`` <#size/1>`__

All functions, except ``reduce/3``, are required by the Dict behaviour.
``reduce/3`` must be implemtented as per the Enumerable protocol.

Based on these functions, ```Dict`` <Dict.html>`__ generates default
implementations for the following functions:

-  ```drop/2`` <#drop/2>`__
-  ```equal?/2`` <#equal?/2>`__
-  ```fetch!/2`` <#fetch!/2>`__
-  ```get/2`` <#get/2>`__
-  ```get/3`` <#get/3>`__
-  ```has_key?/2`` <#has_key?/2>`__
-  ```keys/1`` <#keys/1>`__
-  ```merge/2`` <#merge/2>`__
-  ```merge/3`` <#merge/3>`__
-  ```pop/2`` <#pop/2>`__
-  ```pop/3`` <#pop/3>`__
-  ```put_new/3`` <#put_new/3>`__
-  ```split/2`` <#split/2>`__
-  ```take/2`` <#take/2>`__
-  ```to_list/1`` <#to_list/1>`__
-  ```update/4`` <#update/4>`__
-  ```update!/3`` <#update!/3>`__
-  ```values/1`` <#values/1>`__

All of these functions are defined as overridable, so you can provide
your own implementation if needed.

Note you can also test your custom module via ```Dict`` <Dict.html>`__'s
doctests:

::

    defmodule MyDict do
      # ...
    end

    defmodule MyTests do
      use ExUnit.Case
      doctest Dict
      defp dict_impl, do: MyDict
    end






Summary
-------

========================= =
:elixir:func:`delete/2`   Removes the entry stored under the given ``key`` from ``dict``. If ``dict`` does not contain ``key``, returns the dictionary unchanged 

:elixir:func:`drop/2`     Returns a new dict where the given ``keys`` are removed from ``dict``. Any non-member keys are ignored 

:elixir:func:`equal?/2`   Check if two dicts are equal using ``===`` 

:elixir:func:`fetch!/2`   Returns the value associated with ``key`` in ``dict``. If ``dict`` does not contain ``key``, it raises ```KeyError`` <KeyError.html>`__ 

:elixir:func:`fetch/2`    Returns ``{:ok, value}`` associated with ``key`` in ``dict``. If ``dict`` does not contain ``key``, returns ``:error`` 

:elixir:func:`get/3`      Returns the value associated with ``key`` in ``dict``. If ``dict`` does not contain ``key``, returns ``default`` (or ``nil`` if not provided) 

:elixir:func:`has_key?/2` Returns whether the given ``key`` exists in the given ``dict`` 

:elixir:func:`keys/1`     Returns a list of all keys in ``dict``. The keys are not guaranteed to be in any order 

:elixir:func:`merge/3`    Merges the dict ``b`` into dict ``a`` 

:elixir:func:`pop/3`      Returns the value associated with ``key`` in ``dict`` as well as the ``dict`` without ``key`` 

:elixir:func:`put/3`      Stores the given ``value`` under ``key`` in ``dict``. If ``dict`` already has ``key``, the stored value is replaced by the new one 

:elixir:func:`put_new/3`  Puts the given ``value`` under ``key`` in ``dict`` unless ``key`` already exists 

:elixir:func:`size/1`     Returns the number of elements in ``dict`` 

:elixir:func:`split/2`    Returns a tuple of two dicts, where the first dict contains only entries from ``dict`` with keys in ``keys``, and the second dict contains only entries from ``dict`` with keys not in ``keys`` 

:elixir:func:`take/2`     Returns a new dict where only the keys in ``keys`` from ``dict`` are included 

:elixir:func:`to_list/1`  Returns a list of key-value pairs stored in ``dict``. No particular order is enforced 

:elixir:func:`update!/3`  Update a value in ``dict`` by calling ``fun`` on the value to get a new value. An exception is generated if ``key`` is not present in the dict 

:elixir:func:`update/4`   Update a value in ``dict`` by calling ``fun`` on the value to get a new value. If ``key`` is not present in ``dict`` then ``initial`` will be stored as the first value 

:elixir:func:`values/1`   Returns a list of all values in ``dict``. The values are not guaranteed to be in any order 
========================= =



Types
-----

.. elixir:type:: Dict.key/0

   :elixir:type:`key/0` :: any
   

.. elixir:type:: Dict.value/0

   :elixir:type:`value/0` :: any
   

.. elixir:type:: Dict.t/0

   :elixir:type:`t/0` :: [] | %{}
   





Functions
---------

.. elixir:function:: Dict.delete/2
   :sig: delete(dict, key)


   Specs:
   
 
   * delete(:elixir:type:`t/0`, :elixir:type:`key/0`) :: :elixir:type:`t/0`
 

   
   Removes the entry stored under the given ``key`` from ``dict``. If
   ``dict`` does not contain ``key``, returns the dictionary unchanged.
   
   **Examples**
   
   ::
   
       iex> d = Enum.into([a: 1, b: 2], dict_impl.new)
       iex> d = Dict.delete(d, :a)
       iex> Dict.get(d, :a)
       nil
   
       iex> d = Enum.into([b: 2], dict_impl.new)
       iex> Dict.delete(d, :a) == d
       true
   
   
   

.. elixir:function:: Dict.drop/2
   :sig: drop(dict, keys)


   Specs:
   
 
   * drop(:elixir:type:`t/0`, [:elixir:type:`key/0`]) :: :elixir:type:`t/0`
 

   
   Returns a new dict where the given ``keys`` are removed from ``dict``.
   Any non-member keys are ignored.
   
   **Examples**
   
   ::
   
       iex> d = Enum.into([a: 1, b: 2], dict_impl.new)
       iex> d = Dict.drop(d, [:a, :c, :d])
       iex> Dict.to_list(d)
       [b: 2]
   
       iex> d = Enum.into([a: 1, b: 2], dict_impl.new)
       iex> d = Dict.drop(d, [:c, :d])
       iex> Dict.to_list(d) |> Enum.sort
       [a: 1, b: 2]
   
   
   

.. elixir:function:: Dict.equal?/2
   :sig: equal?(dict1, dict2)


   Specs:
   
 
   * equal?(:elixir:type:`t/0`, :elixir:type:`t/0`) :: boolean
 

   
   Check if two dicts are equal using ``===``.
   
   Notice this function is polymorphic as it compares dicts of any type.
   Each dict implementation also provides an ``equal?`` function, but they
   can only compare dicts of the same type.
   
   **Examples**
   
   ::
   
       iex> a = Enum.into([a: 2, b: 3, f: 5, c: 123], dict_impl.new)
       iex> b = [a: 2, b: 3, f: 5, c: 123]
       iex> Dict.equal?(a, b)
       true
   
       iex> a = Enum.into([a: 2, b: 3, f: 5, c: 123], dict_impl.new)
       iex> b = []
       iex> Dict.equal?(a, b)
       false
   
   
   

.. elixir:function:: Dict.fetch/2
   :sig: fetch(dict, key)


   Specs:
   
 
   * fetch(:elixir:type:`t/0`, :elixir:type:`key/0`) :: :elixir:type:`value/0`
 

   
   Returns ``{:ok, value}`` associated with ``key`` in ``dict``. If
   ``dict`` does not contain ``key``, returns ``:error``.
   
   **Examples**
   
   ::
   
       iex> d = Enum.into([a: 1], dict_impl.new)
       iex> Dict.fetch(d, :a)
       {:ok, 1}
       iex> Dict.fetch(d, :b)
       :error
   
   
   

.. elixir:function:: Dict.fetch!/2
   :sig: fetch!(dict, key)


   Specs:
   
 
   * fetch!(:elixir:type:`t/0`, :elixir:type:`key/0`) :: :elixir:type:`value/0` | no_return
 

   
   Returns the value associated with ``key`` in ``dict``. If ``dict`` does
   not contain ``key``, it raises ```KeyError`` <KeyError.html>`__.
   
   **Examples**
   
   ::
   
       iex> d = Enum.into([a: 1], dict_impl.new)
       iex> Dict.fetch!(d, :a)
       1
   
   
   

.. elixir:function:: Dict.get/3
   :sig: get(dict, key, default \\ nil)


   Specs:
   
 
   * get(:elixir:type:`t/0`, :elixir:type:`key/0`, :elixir:type:`value/0`) :: :elixir:type:`value/0`
 

   
   Returns the value associated with ``key`` in ``dict``. If ``dict`` does
   not contain ``key``, returns ``default`` (or ``nil`` if not provided).
   
   **Examples**
   
   ::
   
       iex> d = Enum.into([a: 1], dict_impl.new)
       iex> Dict.get(d, :a)
       1
       iex> Dict.get(d, :b)
       nil
       iex> Dict.get(d, :b, 3)
       3
   
   
   

.. elixir:function:: Dict.has_key?/2
   :sig: has_key?(dict, key)


   Specs:
   
 
   * has_key?(:elixir:type:`t/0`, :elixir:type:`key/0`) :: boolean
 

   
   Returns whether the given ``key`` exists in the given ``dict``.
   
   **Examples**
   
   ::
   
       iex> d = Enum.into([a: 1], dict_impl.new)
       iex> Dict.has_key?(d, :a)
       true
       iex> Dict.has_key?(d, :b)
       false
   
   
   

.. elixir:function:: Dict.keys/1
   :sig: keys(dict)


   Specs:
   
 
   * keys(:elixir:type:`t/0`) :: [:elixir:type:`key/0`]
 

   
   Returns a list of all keys in ``dict``. The keys are not guaranteed to
   be in any order.
   
   **Examples**
   
   ::
   
       iex> d = Enum.into([a: 1, b: 2], dict_impl.new)
       iex> Enum.sort(Dict.keys(d))
       [:a,:b]
   
   
   

.. elixir:function:: Dict.merge/3
   :sig: merge(dict1, dict2, fun \\ fn _k, _v1, v2 -> v2 end)


   Specs:
   
 
   * merge(:elixir:type:`t/0`, :elixir:type:`t/0`, (:elixir:type:`key/0`, :elixir:type:`value/0`, :elixir:type:`value/0` -> :elixir:type:`value/0`)) :: :elixir:type:`t/0`
 

   
   Merges the dict ``b`` into dict ``a``.
   
   If one of the dict ``b`` entries already exists in the ``dict``, the
   functions in entries in ``b`` have higher precedence unless a function
   is given to resolve conflicts.
   
   Notice this function is polymorphic as it merges dicts of any type. Each
   dict implementation also provides a ``merge`` function, but they can
   only merge dicts of the same type.
   
   **Examples**
   
   ::
   
       iex> d1 = Enum.into([a: 1, b: 2], dict_impl.new)
       iex> d2 = Enum.into([a: 3, d: 4], dict_impl.new)
       iex> d = Dict.merge(d1, d2)
       iex> [a: Dict.get(d, :a), b: Dict.get(d, :b), d: Dict.get(d, :d)]
       [a: 3, b: 2, d: 4]
   
       iex> d1 = Enum.into([a: 1, b: 2], dict_impl.new)
       iex> d2 = Enum.into([a: 3, d: 4], dict_impl.new)
       iex> d = Dict.merge(d1, d2, fn(_k, v1, v2) ->
       ...>   v1 + v2
       ...> end)
       iex> [a: Dict.get(d, :a), b: Dict.get(d, :b), d: Dict.get(d, :d)]
       [a: 4, b: 2, d: 4]
   
   
   

.. elixir:function:: Dict.pop/3
   :sig: pop(dict, key, default \\ nil)


   Specs:
   
 
   * pop(:elixir:type:`t/0`, :elixir:type:`key/0`, :elixir:type:`value/0`) :: {:elixir:type:`value/0`, :elixir:type:`t/0`}
 

   
   Returns the value associated with ``key`` in ``dict`` as well as the
   ``dict`` without ``key``.
   
   **Examples**
   
   ::
   
       iex> dict = Enum.into([a: 1], dict_impl.new)
       iex> {v, d} = Dict.pop dict, :a
       iex> {v, Enum.sort(d)}
       {1,[]}
   
       iex> dict = Enum.into([a: 1], dict_impl.new)
       iex> {v, d} = Dict.pop dict, :b
       iex> {v, Enum.sort(d)}
       {nil,[a: 1]}
   
       iex> dict = Enum.into([a: 1], dict_impl.new)
       iex> {v, d} = Dict.pop dict, :b, 3
       iex> {v, Enum.sort(d)}
       {3,[a: 1]}
   
   
   

.. elixir:function:: Dict.put/3
   :sig: put(dict, key, val)


   Specs:
   
 
   * put(:elixir:type:`t/0`, :elixir:type:`key/0`, :elixir:type:`value/0`) :: :elixir:type:`t/0`
 

   
   Stores the given ``value`` under ``key`` in ``dict``. If ``dict``
   already has ``key``, the stored value is replaced by the new one.
   
   **Examples**
   
   ::
   
       iex> d = Enum.into([a: 1, b: 2], dict_impl.new)
       iex> d = Dict.put(d, :a, 3)
       iex> Dict.get(d, :a)
       3
   
   
   

.. elixir:function:: Dict.put_new/3
   :sig: put_new(dict, key, val)


   Specs:
   
 
   * put_new(:elixir:type:`t/0`, :elixir:type:`key/0`, :elixir:type:`value/0`) :: :elixir:type:`t/0`
 

   
   Puts the given ``value`` under ``key`` in ``dict`` unless ``key``
   already exists.
   
   **Examples**
   
   ::
   
       iex> d = Enum.into([a: 1, b: 2], dict_impl.new)
       iex> d = Dict.put_new(d, :a, 3)
       iex> Dict.get(d, :a)
       1
   
   
   

.. elixir:function:: Dict.size/1
   :sig: size(dict)


   Specs:
   
 
   * size(:elixir:type:`t/0`) :: non_neg_integer
 

   
   Returns the number of elements in ``dict``.
   
   **Examples**
   
   ::
   
       iex> d = Enum.into([a: 1, b: 2], dict_impl.new)
       iex> Dict.size(d)
       2
   
   
   

.. elixir:function:: Dict.split/2
   :sig: split(dict, keys)


   Specs:
   
 
   * split(:elixir:type:`t/0`, [:elixir:type:`key/0`]) :: {:elixir:type:`t/0`, :elixir:type:`t/0`}
 

   
   Returns a tuple of two dicts, where the first dict contains only entries
   from ``dict`` with keys in ``keys``, and the second dict contains only
   entries from ``dict`` with keys not in ``keys``
   
   Any non-member keys are ignored.
   
   **Examples**
   
   ::
   
       iex> d = Enum.into([a: 1, b: 2, c: 3, d: 4], dict_impl.new)
       iex> {d1, d2} = Dict.split(d, [:a, :c, :e])
       iex> {Dict.to_list(d1) |> Enum.sort, Dict.to_list(d2) |> Enum.sort}
       {[a: 1, c: 3], [b: 2, d: 4]}
   
       iex> d = Enum.into([], dict_impl.new)
       iex> {d1, d2} = Dict.split(d, [:a, :c])
       iex> {Dict.to_list(d1), Dict.to_list(d2)}
       {[], []}
   
       iex> d = Enum.into([a: 1, b: 2], dict_impl.new)
       iex> {d1, d2} = Dict.split(d, [:a, :b, :c])
       iex> {Dict.to_list(d1) |> Enum.sort, Dict.to_list(d2)}
       {[a: 1, b: 2], []}
   
   
   

.. elixir:function:: Dict.take/2
   :sig: take(dict, keys)


   Specs:
   
 
   * take(:elixir:type:`t/0`, [:elixir:type:`key/0`]) :: :elixir:type:`t/0`
 

   
   Returns a new dict where only the keys in ``keys`` from ``dict`` are
   included.
   
   Any non-member keys are ignored.
   
   **Examples**
   
   ::
   
       iex> d = Enum.into([a: 1, b: 2], dict_impl.new)
       iex> d = Dict.take(d, [:a, :c, :d])
       iex> Dict.to_list(d)
       [a: 1]
       iex> d = Dict.take(d, [:c, :d])
       iex> Dict.to_list(d)
       []
   
   
   

.. elixir:function:: Dict.to_list/1
   :sig: to_list(dict)


   Specs:
   
 
   * to_list(:elixir:type:`t/0`) :: []
 

   
   Returns a list of key-value pairs stored in ``dict``. No particular
   order is enforced.
   
   

.. elixir:function:: Dict.update/4
   :sig: update(dict, key, initial, fun)


   Specs:
   
 
   * update(:elixir:type:`t/0`, :elixir:type:`key/0`, :elixir:type:`value/0`, (:elixir:type:`value/0` -> :elixir:type:`value/0`)) :: :elixir:type:`t/0`
 

   
   Update a value in ``dict`` by calling ``fun`` on the value to get a new
   value. If ``key`` is not present in ``dict`` then ``initial`` will be
   stored as the first value.
   
   **Examples**
   
   ::
   
       iex> d = Enum.into([a: 1, b: 2], dict_impl.new)
       iex> d = Dict.update(d, :c, 3, fn(val) -> -val end)
       iex> Dict.get(d, :c)
       3
   
   
   

.. elixir:function:: Dict.update!/3
   :sig: update!(dict, key, fun)


   Specs:
   
 
   * update!(:elixir:type:`t/0`, :elixir:type:`key/0`, (:elixir:type:`value/0` -> :elixir:type:`value/0`)) :: :elixir:type:`t/0`
 

   
   Update a value in ``dict`` by calling ``fun`` on the value to get a new
   value. An exception is generated if ``key`` is not present in the dict.
   
   **Examples**
   
   ::
   
       iex> d = Enum.into([a: 1, b: 2], dict_impl.new)
       iex> d = Dict.update!(d, :a, fn(val) -> -val end)
       iex> Dict.get(d, :a)
       -1
   
   
   

.. elixir:function:: Dict.values/1
   :sig: values(dict)


   Specs:
   
 
   * values(:elixir:type:`t/0`) :: [:elixir:type:`value/0`]
 

   
   Returns a list of all values in ``dict``. The values are not guaranteed
   to be in any order.
   
   **Examples**
   
   ::
   
       iex> d = Enum.into([a: 1, b: 2], dict_impl.new)
       iex> Enum.sort(Dict.values(d))
       [1,2]
   
   
   







Callbacks
---------

.. elixir:callback:: Dict.delete/2
   :sig: delete/2


   Specs:
   
 
   * delete(:elixir:type:`t/0`, :elixir:type:`key/0`) :: :elixir:type:`t/0`
 

   
   
   

.. elixir:callback:: Dict.drop/2
   :sig: drop/2


   Specs:
   
 
   * drop(:elixir:type:`t/0`, :elixir:type:`Enum.t/0`) :: :elixir:type:`t/0`
 

   
   
   

.. elixir:callback:: Dict.equal?/2
   :sig: equal?/2


   Specs:
   
 
   * equal?(:elixir:type:`t/0`, :elixir:type:`t/0`) :: boolean
 

   
   
   

.. elixir:callback:: Dict.fetch/2
   :sig: fetch/2


   Specs:
   
 
   * fetch(:elixir:type:`t/0`, :elixir:type:`key/0`) :: {:ok, :elixir:type:`value/0`} | :error
 

   
   
   

.. elixir:callback:: Dict.fetch!/2
   :sig: fetch!/2


   Specs:
   
 
   * fetch!(:elixir:type:`t/0`, :elixir:type:`key/0`) :: :elixir:type:`value/0` | no_return
 

   
   
   

.. elixir:callback:: Dict.get/2
   :sig: get/2


   Specs:
   
 
   * get(:elixir:type:`t/0`, :elixir:type:`key/0`) :: :elixir:type:`value/0`
 

   
   
   

.. elixir:callback:: Dict.get/3
   :sig: get/3


   Specs:
   
 
   * get(:elixir:type:`t/0`, :elixir:type:`key/0`, :elixir:type:`value/0`) :: :elixir:type:`value/0`
 

   
   
   

.. elixir:callback:: Dict.has_key?/2
   :sig: has_key?/2


   Specs:
   
 
   * has_key?(:elixir:type:`t/0`, :elixir:type:`key/0`) :: boolean
 

   
   
   

.. elixir:callback:: Dict.keys/1
   :sig: keys/1


   Specs:
   
 
   * keys(:elixir:type:`t/0`) :: [:elixir:type:`key/0`]
 

   
   
   

.. elixir:callback:: Dict.merge/2
   :sig: merge/2


   Specs:
   
 
   * merge(:elixir:type:`t/0`, :elixir:type:`t/0`) :: :elixir:type:`t/0`
 

   
   
   

.. elixir:callback:: Dict.merge/3
   :sig: merge/3


   Specs:
   
 
   * merge(:elixir:type:`t/0`, :elixir:type:`t/0`, (:elixir:type:`key/0`, :elixir:type:`value/0`, :elixir:type:`value/0` -> :elixir:type:`value/0`)) :: :elixir:type:`t/0`
 

   
   
   

.. elixir:callback:: Dict.new/0
   :sig: new/0


   Specs:
   
 
   * new :: :elixir:type:`t/0`
 

   
   
   

.. elixir:callback:: Dict.pop/2
   :sig: pop/2


   Specs:
   
 
   * pop(:elixir:type:`t/0`, :elixir:type:`key/0`) :: {:elixir:type:`value/0`, :elixir:type:`t/0`}
 

   
   
   

.. elixir:callback:: Dict.pop/3
   :sig: pop/3


   Specs:
   
 
   * pop(:elixir:type:`t/0`, :elixir:type:`key/0`, :elixir:type:`value/0`) :: {:elixir:type:`value/0`, :elixir:type:`t/0`}
 

   
   
   

.. elixir:callback:: Dict.put/3
   :sig: put/3


   Specs:
   
 
   * put(:elixir:type:`t/0`, :elixir:type:`key/0`, :elixir:type:`value/0`) :: :elixir:type:`t/0`
 

   
   
   

.. elixir:callback:: Dict.put_new/3
   :sig: put_new/3


   Specs:
   
 
   * put_new(:elixir:type:`t/0`, :elixir:type:`key/0`, :elixir:type:`value/0`) :: :elixir:type:`t/0`
 

   
   
   

.. elixir:callback:: Dict.size/1
   :sig: size/1


   Specs:
   
 
   * size(:elixir:type:`t/0`) :: non_neg_integer
 

   
   
   

.. elixir:callback:: Dict.split/2
   :sig: split/2


   Specs:
   
 
   * split(:elixir:type:`t/0`, :elixir:type:`Enum.t/0`) :: {:elixir:type:`t/0`, :elixir:type:`t/0`}
 

   
   
   

.. elixir:callback:: Dict.take/2
   :sig: take/2


   Specs:
   
 
   * take(:elixir:type:`t/0`, :elixir:type:`Enum.t/0`) :: :elixir:type:`t/0`
 

   
   
   

.. elixir:callback:: Dict.to_list/1
   :sig: to_list/1


   Specs:
   
 
   * to_list(:elixir:type:`t/0`) :: []
 

   
   
   

.. elixir:callback:: Dict.update/4
   :sig: update/4


   Specs:
   
 
   * update(:elixir:type:`t/0`, :elixir:type:`key/0`, :elixir:type:`value/0`, (:elixir:type:`value/0` -> :elixir:type:`value/0`)) :: :elixir:type:`t/0`
 

   
   
   

.. elixir:callback:: Dict.update!/3
   :sig: update!/3


   Specs:
   
 
   * update!(:elixir:type:`t/0`, :elixir:type:`key/0`, (:elixir:type:`value/0` -> :elixir:type:`value/0`)) :: :elixir:type:`t/0` | no_return
 

   
   
   

.. elixir:callback:: Dict.values/1
   :sig: values/1


   Specs:
   
 
   * values(:elixir:type:`t/0`) :: [:elixir:type:`value/0`]
 

   
   
   



