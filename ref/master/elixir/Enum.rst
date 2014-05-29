Enum
==============================================================

.. elixir:module:: Enum

   :mtype: 

Overview
--------

Provides a set of algorithms that enumerate over collections according
to the :elixir:mod:`Enumerable` protocol:

::

    iex> Enum.map([1, 2, 3], fn(x) -> x * 2 end)
    [2,4,6]

Some particular types, like dictionaries, yield a specific format on
enumeration. For dicts, the argument is always a ``{key, value}`` tuple:

::

    iex> dict = %{a: 1, b: 2}
    iex> Enum.map(dict, fn {k, v} -> {k, v * 2} end)
    [a: 2, b: 4]

Note that the functions in the :elixir:mod:`Enum` module are eager: they always
start the enumeration of the given collection. The :elixir:mod:`Stream` module
allows lazy enumeration of collections and provides infinite streams.

Since the majority of the functions in :elixir:mod:`Enum` enumerate the whole
collection and return a list as result, infinite streams need to be
carefully used with such functions, as they can potentially run forever.
For example:

::

    Enum.each Stream.cycle([1,2,3]), &IO.puts(&1)






Summary
-------

================================ =
:elixir:func:`all?/2`            Invokes the given ``fun`` for each item in the ``collection`` and returns ``false`` if at least one invocation returns ``false``. Otherwise returns ``true`` 

:elixir:func:`any?/2`            Invokes the given ``fun`` for each item in the ``collection`` and returns ``true`` if at least one invocation returns ``true``. Returns ``false`` otherwise 

:elixir:func:`at/3`              Finds the element at the given index (zero-based). Returns ``default`` if index is out of bounds 

:elixir:func:`chunk/2`           Shortcut to ``chunk(coll, n, n)`` 

:elixir:func:`chunk/4`           Returns a collection of lists containing ``n`` items each, where each new chunk starts ``step`` elements into the collection 

:elixir:func:`chunk_by/2`        Splits ``coll`` on every element for which ``fun`` returns a new value 

:elixir:func:`concat/1`          Given an enumerable of enumerables, concatenate the enumerables into a single list 

:elixir:func:`concat/2`          Concatenates the enumerable on the right with the enumerable on the left 

:elixir:func:`count/1`           Returns the collection's size 

:elixir:func:`count/2`           Returns the count of items in the collection for which ``fun`` returns ``true`` 

:elixir:func:`drop/2`            Drops the first ``count`` items from ``collection`` 

:elixir:func:`drop_while/2`      Drops items at the beginning of ``collection`` while ``fun`` returns ``true`` 

:elixir:func:`each/2`            Invokes the given ``fun`` for each item in the ``collection``. Returns ``:ok`` 

:elixir:func:`empty?/1`          Returns ``true`` if the collection is empty, otherwise ``false`` 

:elixir:func:`fetch!/2`          Finds the element at the given index (zero-based). Raises ``OutOfBoundsError`` if the given position is outside the range of the collection 

:elixir:func:`fetch/2`           Finds the element at the given index (zero-based). Returns ``{:ok, element}`` if found, otherwise ``:error`` 

:elixir:func:`filter/2`          Filters the collection, i.e. returns only those elements for which ``fun`` returns ``true`` 

:elixir:func:`filter_map/3`      Filters the collection and maps its values in one pass 

:elixir:func:`find/3`            Returns the first item for which ``fun`` returns a truthy value. If no such item is found, returns ``ifnone`` 

:elixir:func:`find_index/2`      Similar to :elixir:func:`find/3`, but returns the index (zero-based) of the element instead of the element itself 

:elixir:func:`find_value/3`      Similar to :elixir:func:`find/3`, but returns the value of the function invocation instead of the element itself 

:elixir:func:`flat_map/2`        Returns a new collection appending the result of invoking ``fun`` on each corresponding item of ``collection`` 

:elixir:func:`flat_map_reduce/3` Maps and reduces a collection, flattening the given results 

:elixir:func:`group_by/3`        Splits ``collection`` into groups based on ``fun`` 

:elixir:func:`intersperse/2`     Intersperses ``element`` between each element of the enumeration 

:elixir:func:`into/2`            Inserts the given enumerable into a collectable 

:elixir:func:`into/3`            Inserts the given enumerable into a collectable according to the transformation function 

:elixir:func:`join/2`            Joins the given ``collection`` according to ``joiner``. ``joiner`` can be either a binary or a list and the result will be of the same type as ``joiner``. If ``joiner`` is not passed at all, it defaults to an empty binary 

:elixir:func:`map/2`             Returns a new collection, where each item is the result of invoking ``fun`` on each corresponding item of ``collection`` 

:elixir:func:`map_join/3`        Maps and joins the given ``collection`` in one pass. ``joiner`` can be either a binary or a list and the result will be of the same type as ``joiner``. If ``joiner`` is not passed at all, it defaults to an empty binary 

:elixir:func:`map_reduce/3`      Invokes the given ``fun`` for each item in the ``collection`` while also keeping an accumulator. Returns a tuple where the first element is the mapped collection and the second one is the final accumulator 

:elixir:func:`max/1`             Returns the maximum value. Raises ``EmptyError`` if the collection is empty 

:elixir:func:`max_by/2`          Returns the maximum value as calculated by the given function. Raises ``EmptyError`` if the collection is empty 

:elixir:func:`member?/2`         Checks if ``value`` exists within the ``collection`` 

:elixir:func:`min/1`             Returns the minimum value. Raises ``EmptyError`` if the collection is empty 

:elixir:func:`min_by/2`          Returns the minimum value as calculated by the given function. Raises ``EmptyError`` if the collection is empty 

:elixir:func:`partition/2`       Partitions ``collection`` into two collections, where the first one contains elements for which ``fun`` returns a truthy value, and the second one -- for which ``fun`` returns ``false`` or ``nil`` 

:elixir:func:`reduce/2`          Invokes ``fun`` for each element in the collection passing that element and the accumulator ``acc`` as arguments. ``fun``'s return value is stored in ``acc``. The first element of the collection is used as the initial value of ``acc``. Returns the accumulator 

:elixir:func:`reduce/3`          Invokes ``fun`` for each element in the collection passing that element and the accumulator ``acc`` as arguments. ``fun``'s return value is stored in ``acc``. Returns the accumulator 

:elixir:func:`reject/2`          Returns elements of collection for which ``fun`` returns ``false`` 

:elixir:func:`reverse/1`         Reverses the collection 

:elixir:func:`reverse/2`         Reverses the collection and appends the tail. This is an optimization for ``Enum.concat(Enum.reverse(collection), tail)`` 

:elixir:func:`scan/2`            Applies the given function to each element in the collection, storing the result in a list and passing it as the accumulator for the next computation 

:elixir:func:`scan/3`            Applies the given function to each element in the collection, storing the result in a list and passing it as the accumulator for the next computation. Uses the given ``acc`` as the starting value 

:elixir:func:`shuffle/1`         Returns a list of collection elements shuffled 

:elixir:func:`slice/2`           Returns a subset list of the given collection. Drops elements until element position ``range.first``, then takes elements until element position ``range.last`` (inclusive) 

:elixir:func:`slice/3`           Returns a subset list of the given collection. Drops elements until element position ``start``, then takes ``count`` elements 

:elixir:func:`sort/1`            Sorts the collection according to Elixir's term ordering 

:elixir:func:`sort/2`            Sorts the collection by the given function 

:elixir:func:`split/2`           Splits the enumerable into two collections, leaving ``count`` elements in the first one. If ``count`` is a negative number, it starts counting from the back to the beginning of the collection 

:elixir:func:`split_while/2`     Splits ``collection`` in two while ``fun`` returns ``true`` 

:elixir:func:`sum/1`             Returns the sum of all values 

:elixir:func:`take/2`            Takes the first ``count`` items from the collection 

:elixir:func:`take_every/2`      Returns a collection of every ``nth`` item in the collection, starting with the first element 

:elixir:func:`take_while/2`      Takes the items at the beginning of ``collection`` while ``fun`` returns ``true`` 

:elixir:func:`to_list/1`         Convert ``collection`` to a list 

:elixir:func:`traverse/2`        Traverses the given enumerable keeping its shape 

:elixir:func:`uniq/2`            Enumerates the collection, removing all duplicated items 

:elixir:func:`with_index/1`      Returns the collection with each element wrapped in a tuple alongside its index 

:elixir:func:`zip/2`             Zips corresponding elements from two collections into one list of tuples 
================================ =



Types
-----

.. elixir:type:: Enum.t/0

   :elixir:type:`t/0` :: :elixir:type:`Enumerable.t/0`
   

.. elixir:type:: Enum.element/0

   :elixir:type:`element/0` :: any
   

.. elixir:type:: Enum.index/0

   :elixir:type:`index/0` :: non_neg_integer
   

.. elixir:type:: Enum.default/0

   :elixir:type:`default/0` :: any
   





Functions
---------

.. elixir:function:: Enum.all?/2
   :sig: all?(collection, fun \\ fn x -> x end)


   Specs:
   
 
   * all?(:elixir:type:`t/0`, (:elixir:type:`element/0` -> as_boolean(term))) :: boolean
 

   
   Invokes the given ``fun`` for each item in the ``collection`` and
   returns ``false`` if at least one invocation returns ``false``.
   Otherwise returns ``true``.
   
   **Examples**
   
   ::
   
       iex> Enum.all?([2, 4, 6], fn(x) -> rem(x, 2) == 0 end)
       true
   
       iex> Enum.all?([2, 3, 4], fn(x) -> rem(x, 2) == 0 end)
       false
   
   If no function is given, it defaults to checking if all items in the
   collection evaluate to ``true``.
   
   ::
   
       iex> Enum.all?([1, 2, 3])
       true
   
       iex> Enum.all?([1, nil, 3])
       false
   
   
   

.. elixir:function:: Enum.any?/2
   :sig: any?(collection, fun \\ fn x -> x end)


   Specs:
   
 
   * any?(:elixir:type:`t/0`, (:elixir:type:`element/0` -> as_boolean(term))) :: boolean
 

   
   Invokes the given ``fun`` for each item in the ``collection`` and
   returns ``true`` if at least one invocation returns ``true``. Returns
   ``false`` otherwise.
   
   **Examples**
   
   ::
   
       iex> Enum.any?([2, 4, 6], fn(x) -> rem(x, 2) == 1 end)
       false
   
       iex> Enum.any?([2, 3, 4], fn(x) -> rem(x, 2) == 1 end)
       true
   
   If no function is given, it defaults to checking if at least one item in
   the collection evaluates to ``true``.
   
   ::
   
       iex> Enum.any?([false, false, false])
       false
   
       iex> Enum.any?([false, true, false])
       true
   
   
   

.. elixir:function:: Enum.at/3
   :sig: at(collection, n, default \\ nil)


   Specs:
   
 
   * at(:elixir:type:`t/0`, integer, :elixir:type:`default/0`) :: :elixir:type:`element/0` | :elixir:type:`default/0`
 

   
   Finds the element at the given index (zero-based). Returns ``default``
   if index is out of bounds.
   
   **Examples**
   
   ::
   
       iex> Enum.at([2, 4, 6], 0)
       2
   
       iex> Enum.at([2, 4, 6], 2)
       6
   
       iex> Enum.at([2, 4, 6], 4)
       nil
   
       iex> Enum.at([2, 4, 6], 4, :none)
       :none
   
   
   

.. elixir:function:: Enum.chunk/2
   :sig: chunk(coll, n)


   Specs:
   
 
   * chunk(:elixir:type:`t/0`, non_neg_integer) :: [[]]
 

   
   Shortcut to ``chunk(coll, n, n)``.
   
   

.. elixir:function:: Enum.chunk/4
   :sig: chunk(coll, n, step, pad \\ nil)


   Specs:
   
 
   * chunk(:elixir:type:`t/0`, non_neg_integer, non_neg_integer, :elixir:type:`t/0` | nil) :: [[]]
 

   
   Returns a collection of lists containing ``n`` items each, where each
   new chunk starts ``step`` elements into the collection.
   
   ``step`` is optional and, if not passed, defaults to ``n``, i.e. chunks
   do not overlap. If the final chunk does not have ``n`` elements to fill
   the chunk, elements are taken as necessary from ``pad`` if it was
   passed. If ``pad`` is passed and does not have enough elements to fill
   the chunk, then the chunk is returned anyway with less than ``n``
   elements. If ``pad`` is not passed at all or is ``nil``, then the
   partial chunk is discarded from the result.
   
   **Examples**
   
   ::
   
       iex> Enum.chunk([1, 2, 3, 4, 5, 6], 2)
       [[1, 2], [3, 4], [5, 6]]
   
       iex> Enum.chunk([1, 2, 3, 4, 5, 6], 3, 2)
       [[1, 2, 3], [3, 4, 5]]
   
       iex> Enum.chunk([1, 2, 3, 4, 5, 6], 3, 2, [7])
       [[1, 2, 3], [3, 4, 5], [5, 6, 7]]
   
       iex> Enum.chunk([1, 2, 3, 4, 5, 6], 3, 3, [])
       [[1, 2, 3], [4, 5, 6]]
   
   
   

.. elixir:function:: Enum.chunk_by/2
   :sig: chunk_by(coll, fun)


   Specs:
   
 
   * chunk_by(:elixir:type:`t/0`, (:elixir:type:`element/0` -> any)) :: [[]]
 

   
   Splits ``coll`` on every element for which ``fun`` returns a new value.
   
   **Examples**
   
   ::
   
       iex> Enum.chunk_by([1, 2, 2, 3, 4, 4, 6, 7, 7], &(rem(&1, 2) == 1))
       [[1], [2, 2], [3], [4, 4, 6], [7, 7]]
   
   
   

.. elixir:function:: Enum.concat/1
   :sig: concat(enumerables)


   Specs:
   
 
   * concat(:elixir:type:`t/0`) :: :elixir:type:`t/0`
 

   
   Given an enumerable of enumerables, concatenate the enumerables into a
   single list.
   
   **Examples**
   
   ::
   
       iex> Enum.concat([1..3, 4..6, 7..9])
       [1,2,3,4,5,6,7,8,9]
   
       iex> Enum.concat([[1, [2], 3], [4], [5, 6]])
       [1,[2],3,4,5,6]
   
   
   

.. elixir:function:: Enum.concat/2
   :sig: concat(left, right)


   Specs:
   
 
   * concat(:elixir:type:`t/0`, :elixir:type:`t/0`) :: :elixir:type:`t/0`
 

   
   Concatenates the enumerable on the right with the enumerable on the
   left.
   
   This function produces the same result as the :elixir:func:`Kernel.++/2` operator
   for lists.
   
   **Examples**
   
   ::
   
       iex> Enum.concat(1..3, 4..6)
       [1,2,3,4,5,6]
   
       iex> Enum.concat([1, 2, 3], [4, 5, 6])
       [1,2,3,4,5,6]
   
   
   

.. elixir:function:: Enum.count/1
   :sig: count(collection)


   Specs:
   
 
   * count(:elixir:type:`t/0`) :: non_neg_integer
 

   
   Returns the collection's size.
   
   **Examples**
   
   ::
   
       iex> Enum.count([1, 2, 3])
       3
   
   
   

.. elixir:function:: Enum.count/2
   :sig: count(collection, fun)


   Specs:
   
 
   * count(:elixir:type:`t/0`, (:elixir:type:`element/0` -> as_boolean(term))) :: non_neg_integer
 

   
   Returns the count of items in the collection for which ``fun`` returns
   ``true``.
   
   **Examples**
   
   ::
   
       iex> Enum.count([1, 2, 3, 4, 5], fn(x) -> rem(x, 2) == 0 end)
       2
   
   
   

.. elixir:function:: Enum.drop/2
   :sig: drop(collection, count)


   Specs:
   
 
   * drop(:elixir:type:`t/0`, integer) :: []
 

   
   Drops the first ``count`` items from ``collection``.
   
   If a negative value ``count`` is given, the last ``count`` values will
   be dropped. The collection is enumerated once to retrieve the proper
   index and the remaining calculation is performed from the end.
   
   **Examples**
   
   ::
   
       iex> Enum.drop([1, 2, 3], 2)
       [3]
   
       iex> Enum.drop([1, 2, 3], 10)
       []
   
       iex> Enum.drop([1, 2, 3], 0)
       [1,2,3]
   
       iex> Enum.drop([1, 2, 3], -1)
       [1,2]
   
   
   

.. elixir:function:: Enum.drop_while/2
   :sig: drop_while(collection, fun)


   Specs:
   
 
   * drop_while(:elixir:type:`t/0`, (:elixir:type:`element/0` -> as_boolean(term))) :: []
 

   
   Drops items at the beginning of ``collection`` while ``fun`` returns
   ``true``.
   
   **Examples**
   
   ::
   
       iex> Enum.drop_while([1, 2, 3, 4, 5], fn(x) -> x < 3 end)
       [3,4,5]
   
   
   

.. elixir:function:: Enum.each/2
   :sig: each(collection, fun)


   Specs:
   
 
   * each(:elixir:type:`t/0`, (:elixir:type:`element/0` -> any)) :: :ok
 

   
   Invokes the given ``fun`` for each item in the ``collection``. Returns
   ``:ok``.
   
   **Examples**
   
   ::
   
       Enum.each(["some", "example"], fn(x) -> IO.puts x end)
       "some"
       "example"
       #=> :ok
   
   
   

.. elixir:function:: Enum.empty?/1
   :sig: empty?(collection)


   Specs:
   
 
   * empty?(:elixir:type:`t/0`) :: boolean
 

   
   Returns ``true`` if the collection is empty, otherwise ``false``.
   
   **Examples**
   
   ::
   
       iex> Enum.empty?([])
       true
   
       iex> Enum.empty?([1, 2, 3])
       false
   
   
   

.. elixir:function:: Enum.fetch/2
   :sig: fetch(collection, n)


   Specs:
   
 
   * fetch(:elixir:type:`t/0`, integer) :: {:ok, :elixir:type:`element/0`} | :error
 

   
   Finds the element at the given index (zero-based). Returns
   ``{:ok, element}`` if found, otherwise ``:error``.
   
   A negative index can be passed, which means the collection is enumerated
   once and the index is counted from the end (i.e. ``-1`` fetches the last
   element).
   
   **Examples**
   
   ::
   
       iex> Enum.fetch([2, 4, 6], 0)
       {:ok, 2}
   
       iex> Enum.fetch([2, 4, 6], 2)
       {:ok, 6}
   
       iex> Enum.fetch([2, 4, 6], 4)
       :error
   
   
   

.. elixir:function:: Enum.fetch!/2
   :sig: fetch!(collection, n)


   Specs:
   
 
   * fetch!(:elixir:type:`t/0`, integer) :: :elixir:type:`element/0` | no_return
 

   
   Finds the element at the given index (zero-based). Raises
   ``OutOfBoundsError`` if the given position is outside the range of the
   collection.
   
   **Examples**
   
   ::
   
       iex> Enum.fetch!([2, 4, 6], 0)
       2
   
       iex> Enum.fetch!([2, 4, 6], 2)
       6
   
       iex> Enum.fetch!([2, 4, 6], 4)
       ** (Enum.OutOfBoundsError) out of bounds error
   
   
   

.. elixir:function:: Enum.filter/2
   :sig: filter(collection, fun)


   Specs:
   
 
   * filter(:elixir:type:`t/0`, (:elixir:type:`element/0` -> as_boolean(term))) :: []
 

   
   Filters the collection, i.e. returns only those elements for which
   ``fun`` returns ``true``.
   
   **Examples**
   
   ::
   
       iex> Enum.filter([1, 2, 3], fn(x) -> rem(x, 2) == 0 end)
       [2]
   
   
   

.. elixir:function:: Enum.filter_map/3
   :sig: filter_map(collection, filter, mapper)


   Specs:
   
 
   * filter_map(:elixir:type:`t/0`, (:elixir:type:`element/0` -> as_boolean(term)), (:elixir:type:`element/0` -> :elixir:type:`element/0`)) :: []
 

   
   Filters the collection and maps its values in one pass.
   
   **Examples**
   
   ::
   
       iex> Enum.filter_map([1, 2, 3], fn(x) -> rem(x, 2) == 0 end, &(&1 * 2))
       [4]
   
   
   

.. elixir:function:: Enum.find/3
   :sig: find(collection, ifnone \\ nil, fun)


   Specs:
   
 
   * find(:elixir:type:`t/0`, :elixir:type:`default/0`, (:elixir:type:`element/0` -> any)) :: :elixir:type:`element/0` | :elixir:type:`default/0`
 

   
   Returns the first item for which ``fun`` returns a truthy value. If no
   such item is found, returns ``ifnone``.
   
   **Examples**
   
   ::
   
       iex> Enum.find([2, 4, 6], fn(x) -> rem(x, 2) == 1 end)
       nil
   
       iex> Enum.find([2, 4, 6], 0, fn(x) -> rem(x, 2) == 1 end)
       0
   
       iex> Enum.find([2, 3, 4], fn(x) -> rem(x, 2) == 1 end)
       3
   
   
   

.. elixir:function:: Enum.find_index/2
   :sig: find_index(collection, fun)


   Specs:
   
 
   * find_index(:elixir:type:`t/0`, (:elixir:type:`element/0` -> any)) :: :elixir:type:`index/0` | nil
 

   
   Similar to :elixir:func:`find/3`, but returns the index (zero-based) of the element
   instead of the element itself.
   
   **Examples**
   
   ::
   
       iex> Enum.find_index([2, 4, 6], fn(x) -> rem(x, 2) == 1 end)
       nil
   
       iex> Enum.find_index([2, 3, 4], fn(x) -> rem(x, 2) == 1 end)
       1
   
   
   

.. elixir:function:: Enum.find_value/3
   :sig: find_value(collection, ifnone \\ nil, fun)


   Specs:
   
 
   * find_value(:elixir:type:`t/0`, any, (:elixir:type:`element/0` -> any)) :: any | nil
 

   
   Similar to :elixir:func:`find/3`, but returns the value of the function invocation
   instead of the element itself.
   
   **Examples**
   
   ::
   
       iex> Enum.find_value([2, 4, 6], fn(x) -> rem(x, 2) == 1 end)
       nil
   
       iex> Enum.find_value([2, 3, 4], fn(x) -> rem(x, 2) == 1 end)
       true
   
   
   

.. elixir:function:: Enum.flat_map/2
   :sig: flat_map(collection, fun)


   Specs:
   
 
   * flat_map(:elixir:type:`t/0`, (:elixir:type:`element/0` -> :elixir:type:`t/0`)) :: []
 

   
   Returns a new collection appending the result of invoking ``fun`` on
   each corresponding item of ``collection``.
   
   The given function should return an enumerable.
   
   **Examples**
   
   ::
   
       iex> Enum.flat_map([:a, :b, :c], fn(x) -> [x, x] end)
       [:a, :a, :b, :b, :c, :c]
   
       iex> Enum.flat_map([{1,3}, {4,6}], fn({x,y}) -> x..y end)
       [1, 2, 3, 4, 5, 6]
   
   
   

.. elixir:function:: Enum.flat_map_reduce/3
   :sig: flat_map_reduce(collection, acc, fun)


   Specs:
   
 
   * (flat_map_reduce(:elixir:type:`t/0`, acc, fun) :: {[any], any}) when fun: (:elixir:type:`element/0`, acc -> {:elixir:type:`t/0`, acc} | {:halt, acc}), acc: any
 

   
   Maps and reduces a collection, flattening the given results.
   
   It expects an accumulator and a function that receives each stream item
   and an accumulator, and must return a tuple containing a new stream
   (often a list) with the new accumulator or a tuple with ``:halt`` as
   first element and the accumulator as second.
   
   **Examples**
   
   ::
   
       iex> enum = 1..100
       iex> n = 3
       iex> Enum.flat_map_reduce(enum, 0, fn i, acc ->
       ...>   if acc < n, do: {[i], acc + 1}, else: {:halt, acc}
       ...> end)
       {[1,2,3], 3}
   
   
   

.. elixir:function:: Enum.group_by/3
   :sig: group_by(collection, dict \\ %{}, fun)


   Specs:
   
 
   * (group_by(:elixir:type:`t/0`, dict, (:elixir:type:`element/0` -> any)) :: dict) when dict: :elixir:type:`Dict.t/0`
 

   
   Splits ``collection`` into groups based on ``fun``.
   
   The result is a dict (by default a map) where each key is a group and
   each value is a list of elements from ``collection`` for which ``fun``
   returned that group. Ordering is not necessarily preserved.
   
   **Examples**
   
   ::
   
       iex> Enum.group_by(~w{ant buffalo cat dingo}, &String.length/1)
       %{3 => ["cat", "ant"], 7 => ["buffalo"], 5 => ["dingo"]}
   
   
   

.. elixir:function:: Enum.intersperse/2
   :sig: intersperse(collection, element)


   Specs:
   
 
   * intersperse(:elixir:type:`t/0`, :elixir:type:`element/0`) :: []
 

   
   Intersperses ``element`` between each element of the enumeration.
   
   Complexity: O(n)
   
   **Examples**
   
   ::
   
       iex> Enum.intersperse([1, 2, 3], 0)
       [1, 0, 2, 0, 3]
   
       iex> Enum.intersperse([1], 0)
       [1]
   
       iex> Enum.intersperse([], 0)
       []
   
   
   

.. elixir:function:: Enum.into/2
   :sig: into(collection, list)


   Specs:
   
 
   * into(:elixir:type:`Enumerable.t/0`, :elixir:type:`Collectable.t/0`) :: :elixir:type:`Collectable.t/0`
 

   
   Inserts the given enumerable into a collectable.
   
   **Examples**
   
   ::
   
       iex> Enum.into([1, 2], [0])
       [0, 1, 2]
   
       iex> Enum.into([a: 1, b: 2], %{})
       %{a: 1, b: 2}
   
   
   

.. elixir:function:: Enum.into/3
   :sig: into(collection, list, transform)


   Specs:
   
 
   * into(:elixir:type:`Enumerable.t/0`, :elixir:type:`Collectable.t/0`, (term -> term)) :: :elixir:type:`Collectable.t/0`
 

   
   Inserts the given enumerable into a collectable according to the
   transformation function.
   
   **Examples**
   
   ::
   
       iex> Enum.into([2, 3], [3], fn x -> x * 3 end)
       [3, 6, 9]
   
   
   

.. elixir:function:: Enum.join/2
   :sig: join(collection, joiner \\ "")


   Specs:
   
 
   * join(:elixir:type:`t/0`, :elixir:type:`String.t/0`) :: :elixir:type:`String.t/0`
 

   
   Joins the given ``collection`` according to ``joiner``. ``joiner`` can
   be either a binary or a list and the result will be of the same type as
   ``joiner``. If ``joiner`` is not passed at all, it defaults to an empty
   binary.
   
   All items in the collection must be convertible to a binary, otherwise
   an error is raised.
   
   **Examples**
   
   ::
   
       iex> Enum.join([1, 2, 3])
       "123"
   
       iex> Enum.join([1, 2, 3], " = ")
       "1 = 2 = 3"
   
   
   

.. elixir:function:: Enum.map/2
   :sig: map(collection, fun)


   Specs:
   
 
   * map(:elixir:type:`t/0`, (:elixir:type:`element/0` -> any)) :: []
 

   
   Returns a new collection, where each item is the result of invoking
   ``fun`` on each corresponding item of ``collection``.
   
   For dicts, the function expects a key-value tuple.
   
   **Examples**
   
   ::
   
       iex> Enum.map([1, 2, 3], fn(x) -> x * 2 end)
       [2, 4, 6]
   
       iex> Enum.map([a: 1, b: 2], fn({k, v}) -> {k, -v} end)
       [a: -1, b: -2]
   
   
   

.. elixir:function:: Enum.map_join/3
   :sig: map_join(collection, joiner \\ "", mapper)


   Specs:
   
 
   * map_join(:elixir:type:`t/0`, :elixir:type:`String.t/0`, (:elixir:type:`element/0` -> any)) :: :elixir:type:`String.t/0`
 

   
   Maps and joins the given ``collection`` in one pass. ``joiner`` can be
   either a binary or a list and the result will be of the same type as
   ``joiner``. If ``joiner`` is not passed at all, it defaults to an empty
   binary.
   
   All items in the collection must be convertible to a binary, otherwise
   an error is raised.
   
   **Examples**
   
   ::
   
       iex> Enum.map_join([1, 2, 3], &(&1 * 2))
       "246"
   
       iex> Enum.map_join([1, 2, 3], " = ", &(&1 * 2))
       "2 = 4 = 6"
   
   
   

.. elixir:function:: Enum.map_reduce/3
   :sig: map_reduce(collection, acc, fun)


   Specs:
   
 
   * map_reduce(:elixir:type:`t/0`, any, (:elixir:type:`element/0`, any -> any)) :: any
 

   
   Invokes the given ``fun`` for each item in the ``collection`` while also
   keeping an accumulator. Returns a tuple where the first element is the
   mapped collection and the second one is the final accumulator.
   
   For dicts, the first tuple element must be a ``{key, value}`` tuple.
   
   **Examples**
   
   ::
   
       iex> Enum.map_reduce([1, 2, 3], 0, fn(x, acc) -> {x * 2, x + acc} end)
       {[2, 4, 6], 6}
   
   
   

.. elixir:function:: Enum.max/1
   :sig: max(collection)


   Specs:
   
 
   * max(:elixir:type:`t/0`) :: :elixir:type:`element/0` | no_return
 

   
   Returns the maximum value. Raises ``EmptyError`` if the collection is
   empty.
   
   **Examples**
   
   ::
   
       iex> Enum.max([1, 2, 3])
       3
   
   
   

.. elixir:function:: Enum.max_by/2
   :sig: max_by(collection, fun)


   Specs:
   
 
   * max_by(:elixir:type:`t/0`, (:elixir:type:`element/0` -> any)) :: :elixir:type:`element/0` | no_return
 

   
   Returns the maximum value as calculated by the given function. Raises
   ``EmptyError`` if the collection is empty.
   
   **Examples**
   
   ::
   
       iex> Enum.max_by(["a", "aa", "aaa"], fn(x) -> String.length(x) end)
       "aaa"
   
   
   

.. elixir:function:: Enum.member?/2
   :sig: member?(collection, value)


   Specs:
   
 
   * member?(:elixir:type:`t/0`, :elixir:type:`element/0`) :: boolean
 

   
   Checks if ``value`` exists within the ``collection``.
   
   Membership is tested with the match (``===``) operator, although
   enumerables like ranges may include floats inside the given range.
   
   **Examples**
   
   ::
   
       iex> Enum.member?(1..10, 5)
       true
   
       iex> Enum.member?([:a, :b, :c], :d)
       false
   
   
   

.. elixir:function:: Enum.min/1
   :sig: min(collection)


   Specs:
   
 
   * min(:elixir:type:`t/0`) :: :elixir:type:`element/0` | no_return
 

   
   Returns the minimum value. Raises ``EmptyError`` if the collection is
   empty.
   
   **Examples**
   
   ::
   
       iex> Enum.min([1, 2, 3])
       1
   
   
   

.. elixir:function:: Enum.min_by/2
   :sig: min_by(collection, fun)


   Specs:
   
 
   * min_by(:elixir:type:`t/0`, (:elixir:type:`element/0` -> any)) :: :elixir:type:`element/0` | no_return
 

   
   Returns the minimum value as calculated by the given function. Raises
   ``EmptyError`` if the collection is empty.
   
   **Examples**
   
   ::
   
       iex> Enum.min_by(["a", "aa", "aaa"], fn(x) -> String.length(x) end)
       "a"
   
   
   

.. elixir:function:: Enum.partition/2
   :sig: partition(collection, fun)


   Specs:
   
 
   * partition(:elixir:type:`t/0`, (:elixir:type:`element/0` -> any)) :: {[], []}
 

   
   Partitions ``collection`` into two collections, where the first one
   contains elements for which ``fun`` returns a truthy value, and the
   second one -- for which ``fun`` returns ``false`` or ``nil``.
   
   **Examples**
   
   ::
   
       iex> Enum.partition([1, 2, 3], fn(x) -> rem(x, 2) == 0 end)
       {[2], [1,3]}
   
   
   

.. elixir:function:: Enum.reduce/2
   :sig: reduce(collection, fun)


   Specs:
   
 
   * reduce(:elixir:type:`t/0`, (:elixir:type:`element/0`, any -> any)) :: any
 

   
   Invokes ``fun`` for each element in the collection passing that element
   and the accumulator ``acc`` as arguments. ``fun``'s return value is
   stored in ``acc``. The first element of the collection is used as the
   initial value of ``acc``. Returns the accumulator.
   
   **Examples**
   
   ::
   
       iex> Enum.reduce([1, 2, 3, 4], fn(x, acc) -> x * acc end)
       24
   
   
   

.. elixir:function:: Enum.reduce/3
   :sig: reduce(collection, acc, fun)


   Specs:
   
 
   * reduce(:elixir:type:`t/0`, any, (:elixir:type:`element/0`, any -> any)) :: any
 

   
   Invokes ``fun`` for each element in the collection passing that element
   and the accumulator ``acc`` as arguments. ``fun``'s return value is
   stored in ``acc``. Returns the accumulator.
   
   **Examples**
   
   ::
   
       iex> Enum.reduce([1, 2, 3], 0, fn(x, acc) -> x + acc end)
       6
   
   
   

.. elixir:function:: Enum.reject/2
   :sig: reject(collection, fun)


   Specs:
   
 
   * reject(:elixir:type:`t/0`, (:elixir:type:`element/0` -> as_boolean(term))) :: []
 

   
   Returns elements of collection for which ``fun`` returns ``false``.
   
   **Examples**
   
   ::
   
       iex> Enum.reject([1, 2, 3], fn(x) -> rem(x, 2) == 0 end)
       [1, 3]
   
   
   

.. elixir:function:: Enum.reverse/1
   :sig: reverse(collection)


   Specs:
   
 
   * reverse(:elixir:type:`t/0`) :: []
 

   
   Reverses the collection.
   
   **Examples**
   
   ::
   
       iex> Enum.reverse([1, 2, 3])
       [3, 2, 1]
   
   
   

.. elixir:function:: Enum.reverse/2
   :sig: reverse(collection, tail)


   Specs:
   
 
   * reverse(:elixir:type:`t/0`, :elixir:type:`t/0`) :: []
 

   
   Reverses the collection and appends the tail. This is an optimization
   for ``Enum.concat(Enum.reverse(collection), tail)``.
   
   **Examples**
   
   ::
   
       iex> Enum.reverse([1, 2, 3], [4, 5, 6])
       [3, 2, 1, 4, 5, 6]
   
   
   

.. elixir:function:: Enum.scan/2
   :sig: scan(enum, fun)


   Specs:
   
 
   * scan(:elixir:type:`t/0`, (:elixir:type:`element/0`, any -> any)) :: []
 

   
   Applies the given function to each element in the collection, storing
   the result in a list and passing it as the accumulator for the next
   computation.
   
   **Examples**
   
   ::
   
       iex> Enum.scan(1..5, &(&1 + &2))
       [1,3,6,10,15]
   
   
   

.. elixir:function:: Enum.scan/3
   :sig: scan(enum, acc, fun)


   Specs:
   
 
   * scan(:elixir:type:`t/0`, any, (:elixir:type:`element/0`, any -> any)) :: []
 

   
   Applies the given function to each element in the collection, storing
   the result in a list and passing it as the accumulator for the next
   computation. Uses the given ``acc`` as the starting value.
   
   **Examples**
   
   ::
   
       iex> Enum.scan(1..5, 0, &(&1 + &2))
       [1,3,6,10,15]
   
   
   

.. elixir:function:: Enum.shuffle/1
   :sig: shuffle(collection)


   Specs:
   
 
   * shuffle(:elixir:type:`t/0`) :: []
 

   
   Returns a list of collection elements shuffled.
   
   Notice that you need to explicitly call `[`:random.seed/1`](http://www.erlang.org/doc/man/random.html#seed-1)` and set a
   seed value for the random algorithm. Otherwise, the default seed will be
   set which will always return the same result. For example, one could do
   the following to set a seed dynamically:
   
   ::
   
       :random.seed(:erlang.now)
   
   **Examples**
   
   ::
   
       iex> Enum.shuffle([1, 2, 3])
       [3, 2, 1]
       iex> Enum.shuffle([1, 2, 3])
       [3, 1, 2]
   
   
   

.. elixir:function:: Enum.slice/2
   :sig: slice(coll, arg2)


   Specs:
   
 
   * slice(:elixir:type:`t/0`, :elixir:type:`Range.t/0`) :: []
 

   
   Returns a subset list of the given collection. Drops elements until
   element position ``range.first``, then takes elements until element
   position ``range.last`` (inclusive).
   
   Positions are calculated by adding the number of items in the collection
   to negative positions (so position -3 in a collection with count 5
   becomes position 2).
   
   The first position (after adding count to negative positions) must be
   smaller or equal to the last position.
   
   **Examples**
   
   ::
   
       iex> Enum.slice(1..100, 5..10)
       [6, 7, 8, 9, 10, 11]
   
   
   

.. elixir:function:: Enum.slice/3
   :sig: slice(coll, start, count)


   Specs:
   
 
   * slice(:elixir:type:`t/0`, integer, non_neg_integer) :: []
 

   
   Returns a subset list of the given collection. Drops elements until
   element position ``start``, then takes ``count`` elements.
   
   **Examples**
   
   ::
   
       iex> Enum.slice(1..100, 5, 10)
       [6, 7, 8, 9, 10, 11, 12, 13, 14, 15]
   
   
   

.. elixir:function:: Enum.sort/1
   :sig: sort(collection)


   Specs:
   
 
   * sort(:elixir:type:`t/0`) :: []
 

   
   Sorts the collection according to Elixir's term ordering.
   
   Uses the merge sort algorithm.
   
   **Examples**
   
   ::
   
       iex> Enum.sort([3, 2, 1])
       [1, 2, 3]
   
   
   

.. elixir:function:: Enum.sort/2
   :sig: sort(collection, fun)


   Specs:
   
 
   * sort(:elixir:type:`t/0`, (:elixir:type:`element/0`, :elixir:type:`element/0` -> boolean)) :: []
 

   
   Sorts the collection by the given function.
   
   This function uses the merge sort algorithm. The given function must
   return false if the first argument is less than right one.
   
   **Examples**
   
   ::
   
       iex> Enum.sort([1, 2, 3], &(&1 > &2))
       [3, 2, 1]
   
   The sorting algorithm will be stable as long as the given function
   returns true for values considered equal:
   
   ::
   
       iex> Enum.sort ["some", "kind", "of", "monster"], &(byte_size(&1) <= byte_size(&2))
       ["of", "some", "kind", "monster"]
   
   If the function does not return true, the sorting is not stable and the
   order of equal terms may be shuffled:
   
   ::
   
       iex> Enum.sort ["some", "kind", "of", "monster"], &(byte_size(&1) < byte_size(&2))
       ["of", "kind", "some", "monster"]
   
   
   

.. elixir:function:: Enum.split/2
   :sig: split(collection, count)


   Specs:
   
 
   * split(:elixir:type:`t/0`, integer) :: {[], []}
 

   
   Splits the enumerable into two collections, leaving ``count`` elements
   in the first one. If ``count`` is a negative number, it starts counting
   from the back to the beginning of the collection.
   
   Be aware that a negative ``count`` implies the collection will be
   enumerated twice: once to calculate the position, and a second time to
   do the actual splitting.
   
   **Examples**
   
   ::
   
       iex> Enum.split([1, 2, 3], 2)
       {[1,2], [3]}
   
       iex> Enum.split([1, 2, 3], 10)
       {[1,2,3], []}
   
       iex> Enum.split([1, 2, 3], 0)
       {[], [1,2,3]}
   
       iex> Enum.split([1, 2, 3], -1)
       {[1,2], [3]}
   
       iex> Enum.split([1, 2, 3], -5)
       {[], [1,2,3]}
   
   
   

.. elixir:function:: Enum.split_while/2
   :sig: split_while(collection, fun)


   Specs:
   
 
   * split_while(:elixir:type:`t/0`, (:elixir:type:`element/0` -> as_boolean(term))) :: {[], []}
 

   
   Splits ``collection`` in two while ``fun`` returns ``true``.
   
   **Examples**
   
   ::
   
       iex> Enum.split_while([1, 2, 3, 4], fn(x) -> x < 3 end)
       {[1, 2], [3, 4]}
   
   
   

.. elixir:function:: Enum.sum/1
   :sig: sum(collection)


   Specs:
   
 
   * sum(:elixir:type:`t/0`) :: number
 

   
   Returns the sum of all values.
   
   Raises :elixir:mod:`ArithmeticError` if collection contains a non-numeric value.
   
   **Examples**
   
   ::
   
       iex> Enum.sum([1, 2, 3])
       6
   
   
   

.. elixir:function:: Enum.take/2
   :sig: take(collection, count)


   Specs:
   
 
   * take(:elixir:type:`t/0`, integer) :: []
 

   
   Takes the first ``count`` items from the collection.
   
   If a negative ``count`` is given, the last ``count`` values will be
   taken. For such, the collection is fully enumerated keeping up to
   ``2 * count`` elements in memory. Once the end of the collection is
   reached, the last ``count`` elements are returned.
   
   **Examples**
   
   ::
   
       iex> Enum.take([1, 2, 3], 2)
       [1,2]
   
       iex> Enum.take([1, 2, 3], 10)
       [1,2,3]
   
       iex> Enum.take([1, 2, 3], 0)
       []
   
       iex> Enum.take([1, 2, 3], -1)
       [3]
   
   
   

.. elixir:function:: Enum.take_every/2
   :sig: take_every(collection, nth)


   Specs:
   
 
   * take_every(:elixir:type:`t/0`, integer) :: []
 

   
   Returns a collection of every ``nth`` item in the collection, starting
   with the first element.
   
   **Examples**
   
   ::
   
       iex> Enum.take_every(1..10, 2)
       [1, 3, 5, 7, 9]
   
   
   

.. elixir:function:: Enum.take_while/2
   :sig: take_while(collection, fun)


   Specs:
   
 
   * take_while(:elixir:type:`t/0`, (:elixir:type:`element/0` -> as_boolean(term))) :: []
 

   
   Takes the items at the beginning of ``collection`` while ``fun`` returns
   ``true``.
   
   **Examples**
   
   ::
   
       iex> Enum.take_while([1, 2, 3], fn(x) -> x < 3 end)
       [1, 2]
   
   
   

.. elixir:function:: Enum.to_list/1
   :sig: to_list(collection)


   Specs:
   
 
   * to_list(:elixir:type:`t/0`) :: [term]
 

   
   Convert ``collection`` to a list.
   
   **Examples**
   
   ::
   
       iex> Enum.to_list(1 .. 3)
       [1, 2, 3]
   
   
   

.. elixir:function:: Enum.traverse/2
   :sig: traverse(collection, transform)


   Specs:
   
 
   * traverse(:elixir:type:`Enumerable.t/0`, (term -> term)) :: :elixir:type:`Collectable.t/0`
 

   
   Traverses the given enumerable keeping its shape.
   
   It also expects the enumerable to implement the :elixir:mod:`Collectable`
   protocol.
   
   **Examples**
   
   ::
   
       iex> Enum.traverse(%{a: 1, b: 2}, fn {k, v} -> {k, v * 2} end)
       %{a: 2, b: 4}
   
   
   

.. elixir:function:: Enum.uniq/2
   :sig: uniq(collection, fun \\ fn x -> x end)


   Specs:
   
 
   * uniq(:elixir:type:`t/0`, (:elixir:type:`element/0` -> term)) :: []
 

   
   Enumerates the collection, removing all duplicated items.
   
   **Examples**
   
   ::
   
       iex> Enum.uniq([1, 2, 3, 2, 1])
       [1, 2, 3]
   
       iex> Enum.uniq([{1, :x}, {2, :y}, {1, :z}], fn {x, _} -> x end)
       [{1,:x}, {2,:y}]
   
   
   

.. elixir:function:: Enum.with_index/1
   :sig: with_index(collection)


   Specs:
   
 
   * with_index(:elixir:type:`t/0`) :: [{:elixir:type:`element/0`, non_neg_integer}]
 

   
   Returns the collection with each element wrapped in a tuple alongside
   its index.
   
   **Examples**
   
   ::
   
       iex> Enum.with_index [1,2,3]
       [{1,0},{2,1},{3,2}]
   
   
   

.. elixir:function:: Enum.zip/2
   :sig: zip(coll1, coll2)


   Specs:
   
 
   * zip(:elixir:type:`t/0`, :elixir:type:`t/0`) :: [{any, any}]
 

   
   Zips corresponding elements from two collections into one list of
   tuples.
   
   The zipping finishes as soon as any enumerable completes.
   
   **Examples**
   
   ::
   
       iex> Enum.zip([1, 2, 3], [:a, :b, :c])
       [{1,:a},{2,:b},{3,:c}]
   
       iex> Enum.zip([1,2,3,4,5], [:a, :b, :c])
       [{1,:a},{2,:b},{3,:c}]
   
   
   







