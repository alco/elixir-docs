Keyword
==============================================================

.. elixir:module:: Keyword

   :mtype: 

Overview
--------

A keyword is a list of tuples where the first element of the tuple is an
atom and the second element can be any value.

A keyword may have duplicated keys so it is not strictly a dictionary.
However most of the functions in this module behave exactly as a
dictionary and mimic the API defined by the :elixir:mod:`Dict` behaviour.

For example, ``Keyword.get`` will get the first entry matching the given
key, regardless if duplicated entries exist. Similarly, ``Keyword.put``
and ``Keyword.delete`` ensure all duplicated entries for a given key are
removed when invoked.

A handful of functions exist to handle duplicated keys, in particular,
``from_enum`` allows creating a new keywords without removing duplicated
keys, ``get_values`` returns all values for a given key and
``delete_first`` deletes just one of the existing entries.

Since a keyword list is simply a list, all the operations defined in
:elixir:mod:`Enum` and :elixir:mod:`List` can also be applied.





Summary
-------

============================= =
:elixir:func:`delete/2`       Deletes all entries in the keyword list for a specific ``key``. If the ``key`` does not exist, returns the keyword list unchanged. Use ``delete_first`` to delete just the first entry in case of duplicated keys 

:elixir:func:`delete/3`       Deletes the entry in the keyword list for a ``key`` with ``value``. If no ``key`` with ``value`` exists, returns the keyword list unchanged 

:elixir:func:`delete_first/2` Deletes the first entry in the keyword list for a specific ``key``. If the ``key`` does not exist, returns the keyword list unchanged 

:elixir:func:`drop/2`         Drops the given keys from the dict 

:elixir:func:`equal?/2`       Checks if two keywords are equal. I.e. they contain the same keys and those keys contain the same values 

:elixir:func:`fetch!/2`       Fetches the value for specific ``key``. If ``key`` does not exist, a :elixir:mod:`KeyError` is raised 

:elixir:func:`fetch/2`        Fetches the value for a specific ``key`` and returns it in a tuple. If the ``key`` does not exist, returns ``:error`` 

:elixir:func:`get/3`          Gets the value for a specific ``key`` 

:elixir:func:`get_values/2`   Gets all values for a specific ``key`` 

:elixir:func:`has_key?/2`     Returns whether a given ``key`` exists in the given ``keywords`` 

:elixir:func:`keys/1`         Returns all keys from the keyword list. Duplicated keys appear duplicated in the final list of keys 

:elixir:func:`keyword?/1`     Checks if the given argument is a keywords list or not 

:elixir:func:`merge/2`        Merges two keyword lists into one. If they have duplicated entries, the one given as second argument wins 

:elixir:func:`merge/3`        Merges two keyword lists into one. If they have duplicated entries, the given function is invoked to solve conflicts 

:elixir:func:`new/0`          Returns an empty keyword list, i.e. an empty list 

:elixir:func:`new/1`          Creates a keyword from an enumerable 

:elixir:func:`new/2`          Creates a keyword from an enumerable via the transformation function 

:elixir:func:`pop/3`          Returns the first value associated with ``key`` in the keyword list as well as the keyword list without ``key`` 

:elixir:func:`pop_first/3`    Returns the first value associated with ``key`` in the keyword list as well as the keyword list without that particular ocurrence of ``key`` 

:elixir:func:`put/3`          Puts the given ``value`` under ``key`` 

:elixir:func:`put_new/3`      Puts the given ``value`` under ``key`` unless the entry ``key`` already exists 

:elixir:func:`split/2`        Takes all entries corresponding to the given keys and extracts them into a separate keyword list. Returns a tuple with the new list and the old list with removed keys 

:elixir:func:`take/2`         Takes all entries corresponding to the given keys and returns them in a new keyword list 

:elixir:func:`update!/3`      Updates the ``key`` with the given function. If the ``key`` does not exist, raises :elixir:mod:`KeyError` 

:elixir:func:`update/4`       Updates the ``key`` with the given function. If the ``key`` does not exist, inserts the given ``initial`` value 

:elixir:func:`values/1`       Returns all values from the keyword list 
============================= =



Types
-----

.. elixir:type:: Keyword.key/0

   :elixir:type:`key/0` :: atom
   

.. elixir:type:: Keyword.value/0

   :elixir:type:`value/0` :: any
   

.. elixir:type:: Keyword.t/0

   :elixir:type:`t/0` :: [{:elixir:type:`key/0`, :elixir:type:`value/0`}]
   

.. elixir:type:: Keyword.t/1

   :elixir:type:`t/1` :: [{:elixir:type:`key/0`, value}]
   





Functions
---------

.. elixir:function:: Keyword.delete/2
   :sig: delete(keywords, key)


   Specs:
   
 
   * delete(:elixir:type:`t/0`, :elixir:type:`key/0`) :: :elixir:type:`t/0`
 

   
   Deletes all entries in the keyword list for a specific ``key``. If the
   ``key`` does not exist, returns the keyword list unchanged. Use
   ``delete_first`` to delete just the first entry in case of duplicated
   keys.
   
   **Examples**
   
   ::
   
       iex> Keyword.delete([a: 1, b: 2], :a)
       [b: 2]
   
       iex> Keyword.delete([a: 1, b: 2, a: 3], :a)
       [b: 2]
   
       iex> Keyword.delete([b: 2], :a)
       [b: 2]
   
   
   

.. elixir:function:: Keyword.delete/3
   :sig: delete(keywords, key, value)


   Specs:
   
 
   * delete(:elixir:type:`t/0`, :elixir:type:`key/0`, :elixir:type:`value/0`) :: :elixir:type:`t/0`
 

   
   Deletes the entry in the keyword list for a ``key`` with ``value``. If
   no ``key`` with ``value`` exists, returns the keyword list unchanged.
   
   **Examples**
   
   ::
   
       iex> Keyword.delete([a: 1, b: 2], :a, 1)
       [b: 2]
   
       iex> Keyword.delete([a: 1, b: 2, a: 3], :a, 3)
       [a: 1, b: 2]
   
       iex> Keyword.delete([b: 2], :a, 5)
       [b: 2]
   
   
   

.. elixir:function:: Keyword.delete_first/2
   :sig: delete_first(keywords, key)


   Specs:
   
 
   * delete_first(:elixir:type:`t/0`, :elixir:type:`key/0`) :: :elixir:type:`t/0`
 

   
   Deletes the first entry in the keyword list for a specific ``key``. If
   the ``key`` does not exist, returns the keyword list unchanged.
   
   **Examples**
   
   ::
   
       iex> Keyword.delete_first([a: 1, b: 2, a: 3], :a)
       [b: 2, a: 3]
   
       iex> Keyword.delete_first([b: 2], :a)
       [b: 2]
   
   
   

.. elixir:function:: Keyword.drop/2
   :sig: drop(keywords, keys)


   
   Drops the given keys from the dict.
   
   Duplicated keys are preserved in the new keyword list.
   
   **Examples**
   
   ::
   
       iex> d = [a: 1, b: 2, c: 3, d: 4]
       iex> Keyword.drop(d, [:b, :d])
       [a: 1, c: 3]
   
       iex> d = [a: 1, b: 2, b: 3, c: 3, d: 4, a: 5]
       iex> Keyword.drop(d, [:b, :d])
       [a: 1, c: 3, a: 5]
   
   
   

.. elixir:function:: Keyword.equal?/2
   :sig: equal?(left, right)


   Specs:
   
 
   * equal?(:elixir:type:`t/0`, :elixir:type:`t/0`) :: boolean
 

   
   Checks if two keywords are equal. I.e. they contain the same keys and
   those keys contain the same values.
   
   **Examples**
   
   ::
   
       iex> Keyword.equal?([a: 1, b: 2], [b: 2, a: 1])
       true
   
   
   

.. elixir:function:: Keyword.fetch/2
   :sig: fetch(keywords, key)


   Specs:
   
 
   * fetch(:elixir:type:`t/0`, :elixir:type:`key/0`) :: {:ok, :elixir:type:`value/0`}
 

   
   Fetches the value for a specific ``key`` and returns it in a tuple. If
   the ``key`` does not exist, returns ``:error``.
   
   **Examples**
   
   ::
   
       iex> Keyword.fetch([a: 1], :a)
       {:ok, 1}
   
       iex> Keyword.fetch([a: 1], :b)
       :error
   
   
   

.. elixir:function:: Keyword.fetch!/2
   :sig: fetch!(keywords, key)


   Specs:
   
 
   * fetch!(:elixir:type:`t/0`, :elixir:type:`key/0`) :: :elixir:type:`value/0` | no_return
 

   
   Fetches the value for specific ``key``. If ``key`` does not exist, a
   :elixir:mod:`KeyError` is raised.
   
   **Examples**
   
   ::
   
       iex> Keyword.fetch!([a: 1], :a)
       1
   
       iex> Keyword.fetch!([a: 1], :b)
       ** (KeyError) key :b not found in: [a: 1]
   
   
   

.. elixir:function:: Keyword.get/3
   :sig: get(keywords, key, default \\ nil)


   Specs:
   
 
   * get(:elixir:type:`t/0`, :elixir:type:`key/0`, :elixir:type:`value/0`) :: :elixir:type:`value/0`
 

   
   Gets the value for a specific ``key``.
   
   If ``key`` does not exist, return default value (``nil`` if no default
   value).
   
   If duplicated entries exist, the first one is returned. Use
   :elixir:func:`get_values/2` to retrieve all entries.
   
   **Examples**
   
   ::
   
       iex> Keyword.get([a: 1], :a)
       1
   
       iex> Keyword.get([a: 1], :b)
       nil
   
       iex> Keyword.get([a: 1], :b, 3)
       3
   
   
   

.. elixir:function:: Keyword.get_values/2
   :sig: get_values(keywords, key)


   Specs:
   
 
   * get_values(:elixir:type:`t/0`, :elixir:type:`key/0`) :: [:elixir:type:`value/0`]
 

   
   Gets all values for a specific ``key``.
   
   **Examples**
   
   ::
   
       iex> Keyword.get_values([a: 1, a: 2], :a)
       [1,2]
   
   
   

.. elixir:function:: Keyword.has_key?/2
   :sig: has_key?(keywords, key)


   Specs:
   
 
   * has_key?(:elixir:type:`t/0`, :elixir:type:`key/0`) :: boolean
 

   
   Returns whether a given ``key`` exists in the given ``keywords``.
   
   **Examples**
   
   ::
   
       iex> Keyword.has_key?([a: 1], :a)
       true
   
       iex> Keyword.has_key?([a: 1], :b)
       false
   
   
   

.. elixir:function:: Keyword.keys/1
   :sig: keys(keywords)


   Specs:
   
 
   * keys(:elixir:type:`t/0`) :: [:elixir:type:`key/0`]
 

   
   Returns all keys from the keyword list. Duplicated keys appear
   duplicated in the final list of keys.
   
   **Examples**
   
   ::
   
       iex> Keyword.keys([a: 1, b: 2])
       [:a,:b]
   
       iex> Keyword.keys([a: 1, b: 2, a: 3])
       [:a,:b,:a]
   
   
   

.. elixir:function:: Keyword.keyword?/1
   :sig: keyword?(arg1)


   Specs:
   
 
   * keyword?(term) :: boolean
 

   
   Checks if the given argument is a keywords list or not.
   
   

.. elixir:function:: Keyword.merge/2
   :sig: merge(d1, d2)


   Specs:
   
 
   * merge(:elixir:type:`t/0`, :elixir:type:`t/0`) :: :elixir:type:`t/0`
 

   
   Merges two keyword lists into one. If they have duplicated entries, the
   one given as second argument wins.
   
   **Examples**
   
   ::
   
       iex> Keyword.merge([a: 1, b: 2], [a: 3, d: 4]) |> Enum.sort
       [a: 3, b: 2, d: 4]
   
   
   

.. elixir:function:: Keyword.merge/3
   :sig: merge(d1, d2, fun)


   Specs:
   
 
   * merge(:elixir:type:`t/0`, :elixir:type:`t/0`, (:elixir:type:`key/0`, :elixir:type:`value/0`, :elixir:type:`value/0` -> :elixir:type:`value/0`)) :: :elixir:type:`t/0`
 

   
   Merges two keyword lists into one. If they have duplicated entries, the
   given function is invoked to solve conflicts.
   
   **Examples**
   
   ::
   
       iex> Keyword.merge([a: 1, b: 2], [a: 3, d: 4], fn (_k, v1, v2) ->
       ...>  v1 + v2
       ...> end)
       [a: 4, b: 2, d: 4]
   
   
   

.. elixir:function:: Keyword.new/0
   :sig: new()


   Specs:
   
 
   * new :: :elixir:type:`t/0`
 

   
   Returns an empty keyword list, i.e. an empty list.
   
   

.. elixir:function:: Keyword.new/1
   :sig: new(pairs)


   Specs:
   
 
   * new(:elixir:type:`Enum.t/0`) :: :elixir:type:`t/0`
 

   
   Creates a keyword from an enumerable.
   
   Duplicated entries are removed, the latest one prevails. I.e.
   differently from ``Enum.into(enumerable, [])``,
   ``Keyword.new(enumerable)`` guarantees the keys are unique.
   
   **Examples**
   
   ::
   
       iex> Keyword.new([{:b, 1}, {:a, 2}])
       [a: 2, b: 1]
   
   
   

.. elixir:function:: Keyword.new/2
   :sig: new(pairs, transform)


   Specs:
   
 
   * new(:elixir:type:`Enum.t/0`, ({:elixir:type:`key/0`, :elixir:type:`value/0`} -> {:elixir:type:`key/0`, :elixir:type:`value/0`})) :: :elixir:type:`t/0`
 

   
   Creates a keyword from an enumerable via the transformation function.
   
   Duplicated entries are removed, the latest one prevails. I.e.
   differently from ``Enum.into(enumerable, [], fun)``,
   ``Keyword.new(enumerable, fun)`` guarantees the keys are unique.
   
   **Examples**
   
   ::
   
       iex> Keyword.new([:a, :b], fn (x) -> {x, x} end) |> Enum.sort
       [a: :a, b: :b]
   
   
   

.. elixir:function:: Keyword.pop/3
   :sig: pop(keywords, key, default \\ nil)


   
   Returns the first value associated with ``key`` in the keyword list as
   well as the keyword list without ``key``.
   
   All duplicated entries are removed. See :elixir:func:`pop_first/3` for removing
   only the first entry.
   
   **Examples**
   
   ::
   
       iex> Keyword.pop [a: 1], :a
       {1,[]}
   
       iex> Keyword.pop [a: 1], :b
       {nil,[a: 1]}
   
       iex> Keyword.pop [a: 1], :b, 3
       {3,[a: 1]}
   
       iex> Keyword.pop [a: 1], :b, 3
       {3,[a: 1]}
   
       iex> Keyword.pop [a: 1, a: 2], :a
       {1,[]}
   
   
   

.. elixir:function:: Keyword.pop_first/3
   :sig: pop_first(keywords, key, default \\ nil)


   
   Returns the first value associated with ``key`` in the keyword list as
   well as the keyword list without that particular ocurrence of ``key``.
   
   Duplicated entries are not removed.
   
   **Examples**
   
   ::
   
       iex> Keyword.pop_first [a: 1], :a
       {1,[]}
   
       iex> Keyword.pop_first [a: 1], :b
       {nil,[a: 1]}
   
       iex> Keyword.pop_first [a: 1], :b, 3
       {3,[a: 1]}
   
       iex> Keyword.pop_first [a: 1], :b, 3
       {3,[a: 1]}
   
       iex> Keyword.pop_first [a: 1, a: 2], :a
       {1,[a: 2]}
   
   
   

.. elixir:function:: Keyword.put/3
   :sig: put(keywords, key, value)


   Specs:
   
 
   * put(:elixir:type:`t/0`, :elixir:type:`key/0`, :elixir:type:`value/0`) :: :elixir:type:`t/0`
 

   
   Puts the given ``value`` under ``key``.
   
   If a previous value is already stored, all entries are removed and the
   value is overridden.
   
   **Examples**
   
   ::
   
       iex> Keyword.put([a: 1, b: 2], :a, 3)
       [a: 3, b: 2]
   
       iex> Keyword.put([a: 1, b: 2, a: 4], :a, 3)
       [a: 3, b: 2]
   
   
   

.. elixir:function:: Keyword.put_new/3
   :sig: put_new(keywords, key, value)


   Specs:
   
 
   * put_new(:elixir:type:`t/0`, :elixir:type:`key/0`, :elixir:type:`value/0`) :: :elixir:type:`t/0`
 

   
   Puts the given ``value`` under ``key`` unless the entry ``key`` already
   exists.
   
   **Examples**
   
   ::
   
       iex> Keyword.put_new([a: 1], :b, 2)
       [b: 2, a: 1]
   
       iex> Keyword.put_new([a: 1, b: 2], :a, 3)
       [a: 1, b: 2]
   
   
   

.. elixir:function:: Keyword.split/2
   :sig: split(keywords, keys)


   
   Takes all entries corresponding to the given keys and extracts them into
   a separate keyword list. Returns a tuple with the new list and the old
   list with removed keys.
   
   Keys for which there are no entires in the keyword list are ignored.
   
   Entries with duplicated keys end up in the same keyword list.
   
   **Examples**
   
   ::
   
       iex> d = [a: 1, b: 2, c: 3, d: 4]
       iex> Keyword.split(d, [:a, :c, :e])
       {[a: 1, c: 3], [b: 2, d: 4]}
   
       iex> d = [a: 1, b: 2, c: 3, d: 4, a: 5]
       iex> Keyword.split(d, [:a, :c, :e])
       {[a: 1, c: 3, a: 5], [b: 2, d: 4]}
   
   
   

.. elixir:function:: Keyword.take/2
   :sig: take(keywords, keys)


   
   Takes all entries corresponding to the given keys and returns them in a
   new keyword list.
   
   Duplicated keys are preserved in the new keyword list.
   
   **Examples**
   
   ::
   
       iex> d = [a: 1, b: 2, c: 3, d: 4]
       iex> Keyword.take(d, [:a, :c, :e])
       [a: 1, c: 3]
   
       iex> d = [a: 1, b: 2, c: 3, d: 4, a: 5]
       iex> Keyword.take(d, [:a, :c, :e])
       [a: 1, c: 3, a: 5]
   
   
   

.. elixir:function:: Keyword.update/4
   :sig: update(list1, key, initial, fun)


   Specs:
   
 
   * update(:elixir:type:`t/0`, :elixir:type:`key/0`, :elixir:type:`value/0`, (:elixir:type:`value/0` -> :elixir:type:`value/0`)) :: :elixir:type:`t/0`
 

   
   Updates the ``key`` with the given function. If the ``key`` does not
   exist, inserts the given ``initial`` value.
   
   If there are duplicated entries, they are all removed and only the first
   one is updated.
   
   **Examples**
   
   ::
   
       iex> Keyword.update([a: 1], :a, 13, &(&1 * 2))
       [a: 2]
   
       iex> Keyword.update([a: 1], :b, 11, &(&1 * 2))
       [a: 1, b: 11]
   
   
   

.. elixir:function:: Keyword.update!/3
   :sig: update!(keywords, key, fun)


   Specs:
   
 
   * update!(:elixir:type:`t/0`, :elixir:type:`key/0`, (:elixir:type:`value/0` -> :elixir:type:`value/0`)) :: :elixir:type:`t/0` | no_return
 

   
   Updates the ``key`` with the given function. If the ``key`` does not
   exist, raises :elixir:mod:`KeyError`.
   
   If there are duplicated entries, they are all removed and only the first
   one is updated.
   
   **Examples**
   
   ::
   
       iex> Keyword.update!([a: 1], :a, &(&1 * 2))
       [a: 2]
   
       iex> Keyword.update!([a: 1], :b, &(&1 * 2))
       ** (KeyError) key :b not found in: [a: 1]
   
   
   

.. elixir:function:: Keyword.values/1
   :sig: values(keywords)


   Specs:
   
 
   * values(:elixir:type:`t/0`) :: [:elixir:type:`value/0`]
 

   
   Returns all values from the keyword list.
   
   **Examples**
   
   ::
   
       iex> Keyword.values([a: 1, b: 2])
       [1,2]
   
   
   







