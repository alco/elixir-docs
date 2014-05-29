List
==============================================================

.. elixir:module:: List

   :mtype: 

Overview
--------

Implements functions that only make sense for lists and cannot be part
of the Enum protocol. In general, favor using the Enum API instead of
List.

Some functions in this module expect an index. Index access for list is
linear. Negative indexes are also supported but they imply the list will
be iterated twice, one to calculate the proper index and another to the
operation.

A decision was taken to delegate most functions to Erlang's standard
library but follow Elixir's convention of receiving the target (in this
case, a list) as the first argument.





Summary
-------

================================= =
:elixir:func:`delete/2`           Deletes the given item from the list. Returns a list without the item. If the item occurs more than once in the list, just the first occurrence is removed 

:elixir:func:`delete_at/2`        Produces a new list by removing the value at the specified ``index``. Negative indices indicate an offset from the end of the list. If ``index`` is out of bounds, the original ``list`` is returned 

:elixir:func:`duplicate/2`        Duplicates the given element ``n`` times in a list 

:elixir:func:`first/1`            Returns the first element in ``list`` or ``nil`` if ``list`` is empty 

:elixir:func:`flatten/1`          Flattens the given ``list`` of nested lists 

:elixir:func:`flatten/2`          Flattens the given ``list`` of nested lists. The list ``tail`` will be added at the end of the flattened list 

:elixir:func:`foldl/3`            Folds (reduces) the given list to the left with a function. Requires an accumulator 

:elixir:func:`foldr/3`            Folds (reduces) the given list to the right with a function. Requires an accumulator 

:elixir:func:`insert_at/3`        Returns a list with ``value`` inserted at the specified ``index``. Note that ``index`` is capped at the list length. Negative indices indicate an offset from the end of the list 

:elixir:func:`keydelete/3`        Receives a list of tuples and deletes the first tuple where the item at ``position`` matches the given ``item``. Returns the new list 

:elixir:func:`keyfind/4`          Receives a list of tuples and returns the first tuple where the item at ``position`` in the tuple matches the given ``item`` 

:elixir:func:`keymember?/3`       Receives a list of tuples and returns ``true`` if there is a tuple where the item at ``position`` in the tuple matches the given ``item`` 

:elixir:func:`keyreplace/4`       Receives a list of tuples and replaces the item identified by ``key`` at ``position`` if it exists 

:elixir:func:`keysort/2`          Receives a list of tuples and sorts the items at ``position`` of the tuples. The sort is stable 

:elixir:func:`keystore/4`         Receives a list of tuples and replaces the item identified by ``key`` at ``position``. If the item does not exist, it is added to the end of the list 

:elixir:func:`last/1`             Returns the last element in ``list`` or ``nil`` if ``list`` is empty 

:elixir:func:`replace_at/3`       Returns a list with a replaced value at the specified ``index``. Negative indices indicate an offset from the end of the list. If ``index`` is out of bounds, the original ``list`` is returned 

:elixir:func:`to_atom/1`          Converts a char list to an atom 

:elixir:func:`to_existing_atom/1` Converts a char list to an existing atom 

:elixir:func:`to_float/1`         Returns the float whose text representation is ``char_list`` 

:elixir:func:`to_integer/1`       Returns an integer whose text representation is ``char_list`` 

:elixir:func:`to_integer/2`       Returns an integer whose text representation is ``char_list`` in base ``base`` 

:elixir:func:`to_string/1`        Converts a list of integers representing codepoints, lists or strings into a string 

:elixir:func:`to_tuple/1`         Converts a list to a tuple 

:elixir:func:`unzip/1`            Unzips the given list of lists or tuples into separate lists and returns a list of lists 

:elixir:func:`update_at/3`        Returns a list with an updated value at the specified ``index``. Negative indices indicate an offset from the end of the list. If ``index`` is out of bounds, the original ``list`` is returned 

:elixir:func:`wrap/1`             Wraps the argument in a list. If the argument is already a list, returns the list. If the argument is ``nil``, returns an empty list 

:elixir:func:`zip/1`              Zips corresponding elements from each list in ``list_of_lists`` 
================================= =





Functions
---------

.. elixir:function:: List.delete/2
   :sig: delete(list, item)


   Specs:
   
 
   * delete([], any) :: []
 

   
   Deletes the given item from the list. Returns a list without the item.
   If the item occurs more than once in the list, just the first occurrence
   is removed.
   
   **Examples**
   
   ::
   
       iex> List.delete([1, 2, 3], 1)
       [2,3]
   
       iex> List.delete([1, 2, 2, 3], 2)
       [1, 2, 3]
   
   
   

.. elixir:function:: List.delete_at/2
   :sig: delete_at(list, index)


   Specs:
   
 
   * delete_at([], integer) :: []
 

   
   Produces a new list by removing the value at the specified ``index``.
   Negative indices indicate an offset from the end of the list. If
   ``index`` is out of bounds, the original ``list`` is returned.
   
   **Examples**
   
   ::
   
       iex> List.delete_at([1, 2, 3], 0)
       [2, 3]
   
       iex List.delete_at([1, 2, 3], 10)
       [1, 2, 3]
   
       iex> List.delete_at([1, 2, 3], -1)
       [1, 2]
   
   
   

.. elixir:function:: List.duplicate/2
   :sig: duplicate(elem, n)


   Specs:
   
 
   * (duplicate(elem, non_neg_integer) :: [elem]) when elem: var
 

   
   Duplicates the given element ``n`` times in a list.
   
   **Examples**
   
   ::
   
       iex> List.duplicate("hello", 3)
       ["hello","hello","hello"]
   
       iex> List.duplicate([1, 2], 2)
       [[1,2],[1,2]]
   
   
   

.. elixir:function:: List.first/1
   :sig: first(list1)


   Specs:
   
 
   * (first([elem]) :: nil | elem) when elem: var
 

   
   Returns the first element in ``list`` or ``nil`` if ``list`` is empty.
   
   **Examples**
   
   ::
   
       iex> List.first([])
       nil
   
       iex> List.first([1])
       1
   
       iex> List.first([1, 2, 3])
       1
   
   
   

.. elixir:function:: List.flatten/1
   :sig: flatten(list)


   Specs:
   
 
   * (flatten(deep_list) :: []) when deep_list: [any | deep_list]
 

   
   Flattens the given ``list`` of nested lists.
   
   **Examples**
   
   ::
   
       iex> List.flatten([1, [[2], 3]])
       [1,2,3]
   
   
   

.. elixir:function:: List.flatten/2
   :sig: flatten(list, tail)


   Specs:
   
 
   * (flatten(deep_list, [elem]) :: [elem]) when deep_list: [elem | deep_list], elem: var
 

   
   Flattens the given ``list`` of nested lists. The list ``tail`` will be
   added at the end of the flattened list.
   
   **Examples**
   
   ::
   
       iex> List.flatten([1, [[2], 3]], [4, 5])
       [1,2,3,4,5]
   
   
   

.. elixir:function:: List.foldl/3
   :sig: foldl(list, acc, function)


   Specs:
   
 
   * (foldl([elem], acc, (elem, acc -> acc)) :: acc) when elem: var, acc: var
 

   
   Folds (reduces) the given list to the left with a function. Requires an
   accumulator.
   
   **Examples**
   
   ::
   
       iex> List.foldl([5, 5], 10, fn (x, acc) -> x + acc end)
       20
   
       iex> List.foldl([1, 2, 3, 4], 0, fn (x, acc) -> x - acc end)
       2
   
   
   

.. elixir:function:: List.foldr/3
   :sig: foldr(list, acc, function)


   Specs:
   
 
   * (foldr([elem], acc, (elem, acc -> acc)) :: acc) when elem: var, acc: var
 

   
   Folds (reduces) the given list to the right with a function. Requires an
   accumulator.
   
   **Examples**
   
   ::
   
       iex> List.foldr([1, 2, 3, 4], 0, fn (x, acc) -> x - acc end)
       -2
   
   
   

.. elixir:function:: List.insert_at/3
   :sig: insert_at(list, index, value)


   Specs:
   
 
   * insert_at([], integer, any) :: []
 

   
   Returns a list with ``value`` inserted at the specified ``index``. Note
   that ``index`` is capped at the list length. Negative indices indicate
   an offset from the end of the list.
   
   **Examples**
   
   ::
   
       iex> List.insert_at([1, 2, 3, 4], 2, 0)
       [1, 2, 0, 3, 4]
   
       iex> List.insert_at([1, 2, 3], 10, 0)
       [1, 2, 3, 0]
   
       iex> List.insert_at([1, 2, 3], -1, 0)
       [1, 2, 3, 0]
   
       iex> List.insert_at([1, 2, 3], -10, 0)
       [0, 1, 2, 3]
   
   
   

.. elixir:function:: List.keydelete/3
   :sig: keydelete(list, key, position)


   Specs:
   
 
   * keydelete([tuple], any, non_neg_integer) :: [tuple]
 

   
   Receives a list of tuples and deletes the first tuple where the item at
   ``position`` matches the given ``item``. Returns the new list.
   
   **Examples**
   
   ::
   
       iex> List.keydelete([a: 1, b: 2], :a, 0)
       [b: 2]
   
       iex> List.keydelete([a: 1, b: 2], 2, 1)
       [a: 1]
   
       iex> List.keydelete([a: 1, b: 2], :c, 0)
       [a: 1, b: 2]
   
   
   

.. elixir:function:: List.keyfind/4
   :sig: keyfind(list, key, position, default \\ nil)


   Specs:
   
 
   * keyfind([tuple], any, non_neg_integer, any) :: any
 

   
   Receives a list of tuples and returns the first tuple where the item at
   ``position`` in the tuple matches the given ``item``.
   
   **Examples**
   
   ::
   
       iex> List.keyfind([a: 1, b: 2], :a, 0)
       {:a, 1}
   
       iex> List.keyfind([a: 1, b: 2], 2, 1)
       {:b, 2}
   
       iex> List.keyfind([a: 1, b: 2], :c, 0)
       nil
   
   
   

.. elixir:function:: List.keymember?/3
   :sig: keymember?(list, key, position)


   Specs:
   
 
   * keymember?([tuple], any, non_neg_integer) :: any
 

   
   Receives a list of tuples and returns ``true`` if there is a tuple where
   the item at ``position`` in the tuple matches the given ``item``.
   
   **Examples**
   
   ::
   
       iex> List.keymember?([a: 1, b: 2], :a, 0)
       true
   
       iex> List.keymember?([a: 1, b: 2], 2, 1)
       true
   
       iex> List.keymember?([a: 1, b: 2], :c, 0)
       false
   
   
   

.. elixir:function:: List.keyreplace/4
   :sig: keyreplace(list, key, position, new_tuple)


   Specs:
   
 
   * keyreplace([tuple], any, non_neg_integer, tuple) :: [tuple]
 

   
   Receives a list of tuples and replaces the item identified by ``key`` at
   ``position`` if it exists.
   
   **Examples**
   
   ::
   
       iex> List.keyreplace([a: 1, b: 2], :a, 0, {:a, 3})
       [a: 3, b: 2]
   
   
   

.. elixir:function:: List.keysort/2
   :sig: keysort(list, position)


   Specs:
   
 
   * keysort([tuple], non_neg_integer) :: [tuple]
 

   
   Receives a list of tuples and sorts the items at ``position`` of the
   tuples. The sort is stable.
   
   **Examples**
   
   ::
   
       iex> List.keysort([a: 5, b: 1, c: 3], 1)
       [b: 1, c: 3, a: 5]
   
       iex> List.keysort([a: 5, c: 1, b: 3], 0)
       [a: 5, b: 3, c: 1]
   
   
   

.. elixir:function:: List.keystore/4
   :sig: keystore(list, key, position, new_tuple)


   Specs:
   
 
   * keystore([tuple], any, non_neg_integer, tuple) :: [tuple]
 

   
   Receives a list of tuples and replaces the item identified by ``key`` at
   ``position``. If the item does not exist, it is added to the end of the
   list.
   
   **Examples**
   
   ::
   
       iex> List.keystore([a: 1, b: 2], :a, 0, {:a, 3})
       [a: 3, b: 2]
   
       iex> List.keystore([a: 1, b: 2], :c, 0, {:c, 3})
       [a: 1, b: 2, c: 3]
   
   
   

.. elixir:function:: List.last/1
   :sig: last(list1)


   Specs:
   
 
   * (last([elem]) :: nil | elem) when elem: var
 

   
   Returns the last element in ``list`` or ``nil`` if ``list`` is empty.
   
   **Examples**
   
   ::
   
       iex> List.last([])
       nil
   
       iex> List.last([1])
       1
   
       iex> List.last([1, 2, 3])
       3
   
   
   

.. elixir:function:: List.replace_at/3
   :sig: replace_at(list, index, value)


   Specs:
   
 
   * replace_at([], integer, any) :: []
 

   
   Returns a list with a replaced value at the specified ``index``.
   Negative indices indicate an offset from the end of the list. If
   ``index`` is out of bounds, the original ``list`` is returned.
   
   **Examples**
   
   ::
   
       iex> List.replace_at([1, 2, 3], 0, 0)
       [0, 2, 3]
   
       iex> List.replace_at([1, 2, 3], 10, 0)
       [1, 2, 3]
   
       iex> List.replace_at([1, 2, 3], -1, 0)
       [1, 2, 0]
   
       iex> List.replace_at([1, 2, 3], -10, 0)
       [1, 2, 3]
   
   
   

.. elixir:function:: List.to_atom/1
   :sig: to_atom(char_list)


   Specs:
   
 
   * to_atom(char_list) :: atom
 

   
   Converts a char list to an atom.
   
   Currently Elixir does not support conversions from char lists which
   contains Unicode codepoints greater than 0xFF.
   
   Inlined by the compiler.
   
   **Examples**
   
   ::
   
       iex> List.to_atom('elixir')
       :elixir
   
   
   

.. elixir:function:: List.to_existing_atom/1
   :sig: to_existing_atom(char_list)


   Specs:
   
 
   * to_existing_atom(char_list) :: atom
 

   
   Converts a char list to an existing atom.
   
   Currently Elixir does not support conversions from char lists which
   contains Unicode codepoints greater than 0xFF.
   
   Inlined by the compiler.
   
   

.. elixir:function:: List.to_float/1
   :sig: to_float(char_list)


   Specs:
   
 
   * to_float(char_list) :: float
 

   
   Returns the float whose text representation is ``char_list``.
   
   Inlined by the compiler.
   
   **Examples**
   
   ::
   
       iex> List.to_float('2.2017764e+0')
       2.2017764
   
   
   

.. elixir:function:: List.to_integer/1
   :sig: to_integer(char_list)


   Specs:
   
 
   * to_integer(char_list) :: integer
 

   
   Returns an integer whose text representation is ``char_list``.
   
   Inlined by the compiler.
   
   **Examples**
   
   ::
   
       iex> List.to_integer('123')
       123
   
   
   

.. elixir:function:: List.to_integer/2
   :sig: to_integer(char_list, base)


   Specs:
   
 
   * to_integer(char_list, non_neg_integer) :: integer
 

   
   Returns an integer whose text representation is ``char_list`` in base
   ``base``.
   
   Inlined by the compiler.
   
   **Examples**
   
   ::
   
       iex> List.to_integer('3FF', 16)
       1023
   
   
   

.. elixir:function:: List.to_string/1
   :sig: to_string(list)


   Specs:
   
 
   * to_string(:unicode.char_list) :: :elixir:type:`String.t/0`
 

   
   Converts a list of integers representing codepoints, lists or strings
   into a string.
   
   Notice that this function expect a list of integer representing UTF-8
   codepoints. If you have a list of bytes, you must instead use `the
   ``:binary`` module <http://erlang.org/doc/man/binary.html>`__.
   
   **Examples**
   
   ::
   
       iex> List.to_string([0x00E6, 0x00DF])
       "æß"
   
       iex> List.to_string([0x0061, "bc"])
       "abc"
   
   
   

.. elixir:function:: List.to_tuple/1
   :sig: to_tuple(list)


   Specs:
   
 
   * to_tuple([]) :: tuple
 

   
   Converts a list to a tuple.
   
   Inlined by the compiler.
   
   **Examples**
   
   ::
   
       iex> List.to_tuple([:share, [:elixir, 163]])
       {:share, [:elixir, 163]}
   
   
   

.. elixir:function:: List.unzip/1
   :sig: unzip(list)


   Specs:
   
 
   * unzip([tuple]) :: [[]]
 

   
   Unzips the given list of lists or tuples into separate lists and returns
   a list of lists.
   
   **Examples**
   
   ::
   
       iex> List.unzip([{1, 2}, {3, 4}])
       [[1, 3], [2, 4]]
   
       iex> List.unzip([{1, :a, "apple"}, {2, :b, "banana"}, {3, :c}])
       [[1, 2, 3], [:a, :b, :c]]
   
   
   

.. elixir:function:: List.update_at/3
   :sig: update_at(list, index, fun)


   Specs:
   
 
   * (update_at([elem], integer, (elem -> any)) :: []) when elem: var
 

   
   Returns a list with an updated value at the specified ``index``.
   Negative indices indicate an offset from the end of the list. If
   ``index`` is out of bounds, the original ``list`` is returned.
   
   **Examples**
   
   ::
   
       iex> List.update_at([1, 2, 3], 0, &(&1 + 10))
       [11, 2, 3]
   
       iex> List.update_at([1, 2, 3], 10, &(&1 + 10))
       [1, 2, 3]
   
       iex> List.update_at([1, 2, 3], -1, &(&1 + 10))
       [1, 2, 13]
   
       iex> List.update_at([1, 2, 3], -10, &(&1 + 10))
       [1, 2, 3]
   
   
   

.. elixir:function:: List.wrap/1
   :sig: wrap(list)


   Specs:
   
 
   * wrap([] | any) :: []
 

   
   Wraps the argument in a list. If the argument is already a list, returns
   the list. If the argument is ``nil``, returns an empty list.
   
   **Examples**
   
   ::
   
       iex> List.wrap("hello")
       ["hello"]
   
       iex> List.wrap([1, 2, 3])
       [1,2,3]
   
       iex> List.wrap(nil)
       []
   
   
   

.. elixir:function:: List.zip/1
   :sig: zip(list_of_lists)


   Specs:
   
 
   * zip([[]]) :: [tuple]
 

   
   Zips corresponding elements from each list in ``list_of_lists``.
   
   **Examples**
   
   ::
   
       iex> List.zip([[1, 2], [3, 4], [5, 6]])
       [{1, 3, 5}, {2, 4, 6}]
   
       iex> List.zip([[1, 2], [3], [5, 6]])
       [{1, 3, 5}]
   
   
   







