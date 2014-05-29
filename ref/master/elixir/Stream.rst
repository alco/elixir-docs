Stream
==============================================================

.. elixir:module:: Stream

   :mtype: 

Overview
--------

Module for creating and composing streams.

Streams are composable, lazy enumerables. Any enumerable that generates
items one by one during enumeration is called a stream. For example,
Elixir's :elixir:mod:`Range` is a stream:

::

    iex> range = 1..5
    1..5
    iex> Enum.map range, &(&1 * 2)
    [2,4,6,8,10]

In the example above, as we mapped over the range, the elements being
enumerated were created one by one, during enumeration. The :elixir:mod:`Stream`
module allows us to map the range, without triggering its enumeration:

::

    iex> range = 1..3
    iex> stream = Stream.map(range, &(&1 * 2))
    iex> Enum.map(stream, &(&1 + 1))
    [3,5,7]

Notice we started with a range and then we created a stream that is
meant to multiply each item in the range by 2. At this point, no
computation was done yet. Just when :elixir:func:`Enum.map/2` is called we
enumerate over each item in the range, multiplying it by 2 and adding 1.
We say the functions in :elixir:mod:`Stream` are *lazy* and the functions in
:elixir:mod:`Enum` are *eager*.

Due to their laziness, streams are useful when working with large (or
even infinite) collections. When chaining many operations with :elixir:mod:`Enum`,
intermediate lists are created, while :elixir:mod:`Stream` creates a recipe of
computations that are executed at a later moment. Let's see another
example:

::

    1..3 |>
      Enum.map(&IO.inspect(&1)) |>
      Enum.map(&(&1 * 2)) |>
      Enum.map(&IO.inspect(&1))
    1
    2
    3
    2
    4
    6
    #=> [2,4,6]

Notice that we first printed each item in the list, then multiplied each
element by 2 and finally printed each new value. In this example, the
list was enumerated three times. Let's see an example with streams:

::

    stream = 1..3 |>
      Stream.map(&IO.inspect(&1)) |>
      Stream.map(&(&1 * 2)) |>
      Stream.map(&IO.inspect(&1))
    Enum.to_list(stream)
    1
    2
    2
    4
    3
    6
    #=> [2,4,6]

Although the end result is the same, the order in which the items were
printed changed! With streams, we print the first item and then print
its double. In this example, the list was enumerated just once!

That's what we meant when we first said that streams are composable,
lazy enumerables. Notice we could call :elixir:func:`Stream.map/2` multiple times,
effectively composing the streams and they are lazy. The computations
are performed only when you call a function from the :elixir:mod:`Enum` module.

Creating Streams
~~~~~~~~~~~~~~~~

There are many functions in Elixir's standard library that return
streams, some examples are:

-  :elixir:func:`IO.stream/2` - Streams input lines, one by one;
-  :elixir:func:`URI.query_decoder/1` - Decodes a query string, pair by pair;

This module also provides many convenience functions for creating
streams, like :elixir:func:`Stream.cycle/1`, :elixir:func:`Stream.unfold/2`,
:elixir:func:`Stream.resource/3` and more.

Note the functions in this module are guaranteed to return enumerables.
Since enumerables can have different shapes (structs, anonymous
functions, and so on), the functions in this module may return any of
those shapes and that it may change at any time. For example, a function
that today returns an anonymous function may return a struct in future
releases.





Summary
-------

=========================== =
:elixir:func:`chunk/2`      Shortcut to ``chunk(enum, n, n)`` 

:elixir:func:`chunk/4`      Streams the enumerable in chunks, containing ``n`` items each, where each new chunk starts ``step`` elements into the enumerable 

:elixir:func:`chunk_by/2`   Chunks the ``enum`` by buffering elements for which ``fun`` returns the same value and only emit them when ``fun`` returns a new value or the ``enum`` finishes 

:elixir:func:`concat/1`     Creates a stream that enumerates each enumerable in an enumerable 

:elixir:func:`concat/2`     Creates a stream that enumerates the first argument, followed by the second 

:elixir:func:`cycle/1`      Creates a stream that cycles through the given enumerable, infinitely 

:elixir:func:`drop/2`       Lazily drops the next ``n`` items from the enumerable 

:elixir:func:`drop_while/2` Lazily drops elements of the enumerable while the given function returns ``true`` 

:elixir:func:`each/2`       Execute the given function for each item 

:elixir:func:`filter/2`     Creates a stream that filters elements according to the given function on enumeration 

:elixir:func:`filter_map/3` Creates a stream that filters and then maps elements according to given functions 

:elixir:func:`flat_map/2`   Creates a stream that will apply the given function on enumeration and flatten the result 

:elixir:func:`into/3`       Injects the stream values into the given collectable as a side-effect 

:elixir:func:`iterate/2`    Emit a sequence of values, starting with ``start_value``. Successive values are generated by calling ``next_fun`` on the previous value 

:elixir:func:`map/2`        Creates a stream that will apply the given function on enumeration 

:elixir:func:`reject/2`     Creates a stream that will reject elements according to the given function on enumeration 

:elixir:func:`repeatedly/1` Returns a stream generated by calling ``generator_fun`` repeatedly 

:elixir:func:`resource/3`   Emits a sequence of values for the given resource 

:elixir:func:`run/1`        Runs the given stream 

:elixir:func:`scan/2`       Creates a stream that applies the given function to each element, emits the result and uses the same result as the accumulator for the next computation 

:elixir:func:`scan/3`       Creates a stream that applies the given function to each element, emits the result and uses the same result as the accumulator for the next computation. Uses the given ``acc`` as the starting value 

:elixir:func:`take/2`       Lazily takes the next ``n`` items from the enumerable and stops enumeration 

:elixir:func:`take_every/2` Creates a stream that takes every ``n`` item from the enumerable 

:elixir:func:`take_while/2` Lazily takes elements of the enumerable while the given function returns ``true`` 

:elixir:func:`transform/3`  Transforms an existing stream 

:elixir:func:`unfold/2`     Emits a sequence of values for the given accumulator 

:elixir:func:`uniq/2`       Creates a stream that only emits elements if they are unique 

:elixir:func:`with_index/1` Creates a stream where each item in the enumerable will be wrapped in a tuple alongside its index 

:elixir:func:`zip/2`        Zips two collections together, lazily 
=========================== =



Types
-----

.. elixir:type:: Stream.t/0

   :elixir:type:`t/0` :: %Stream{enum: term, funs: term, accs: term, done: term}
   

.. elixir:type:: Stream.acc/0

   :elixir:type:`acc/0` :: any
   

.. elixir:type:: Stream.element/0

   :elixir:type:`element/0` :: any
   

.. elixir:type:: Stream.index/0

   :elixir:type:`index/0` :: non_neg_integer
   

.. elixir:type:: Stream.default/0

   :elixir:type:`default/0` :: any
   





Functions
---------

.. elixir:function:: Stream.chunk/2
   :sig: chunk(enum, n)


   Specs:
   
 
   * chunk(:elixir:type:`Enumerable.t/0`, non_neg_integer) :: :elixir:type:`Enumerable.t/0`
 

   
   Shortcut to ``chunk(enum, n, n)``.
   
   

.. elixir:function:: Stream.chunk/4
   :sig: chunk(enum, n, step, pad \\ nil)


   Specs:
   
 
   * chunk(:elixir:type:`Enumerable.t/0`, non_neg_integer, non_neg_integer, :elixir:type:`Enumerable.t/0` | nil) :: :elixir:type:`Enumerable.t/0`
 

   
   Streams the enumerable in chunks, containing ``n`` items each, where
   each new chunk starts ``step`` elements into the enumerable.
   
   ``step`` is optional and, if not passed, defaults to ``n``, i.e. chunks
   do not overlap. If the final chunk does not have ``n`` elements to fill
   the chunk, elements are taken as necessary from ``pad`` if it was
   passed. If ``pad`` is passed and does not have enough elements to fill
   the chunk, then the chunk is returned anyway with less than ``n``
   elements. If ``pad`` is not passed at all or is ``nil``, then the
   partial chunk is discarded from the result.
   
   **Examples**
   
   ::
   
       iex> Stream.chunk([1, 2, 3, 4, 5, 6], 2) |> Enum.to_list
       [[1, 2], [3, 4], [5, 6]]
   
       iex> Stream.chunk([1, 2, 3, 4, 5, 6], 3, 2) |> Enum.to_list
       [[1, 2, 3], [3, 4, 5]]
   
       iex> Stream.chunk([1, 2, 3, 4, 5, 6], 3, 2, [7]) |> Enum.to_list
       [[1, 2, 3], [3, 4, 5], [5, 6, 7]]
   
       iex> Stream.chunk([1, 2, 3, 4, 5, 6], 3, 3, []) |> Enum.to_list
       [[1, 2, 3], [4, 5, 6]]
   
   
   

.. elixir:function:: Stream.chunk_by/2
   :sig: chunk_by(enum, fun)


   Specs:
   
 
   * chunk_by(:elixir:type:`Enumerable.t/0`, (:elixir:type:`element/0` -> any)) :: :elixir:type:`Enumerable.t/0`
 

   
   Chunks the ``enum`` by buffering elements for which ``fun`` returns the
   same value and only emit them when ``fun`` returns a new value or the
   ``enum`` finishes.
   
   **Examples**
   
   ::
   
       iex> stream = Stream.chunk_by([1, 2, 2, 3, 4, 4, 6, 7, 7], &(rem(&1, 2) == 1))
       iex> Enum.to_list(stream)
       [[1], [2, 2], [3], [4, 4, 6], [7, 7]]
   
   
   

.. elixir:function:: Stream.concat/1
   :sig: concat(enumerables)


   Specs:
   
 
   * concat(:elixir:type:`Enumerable.t/0`) :: :elixir:type:`Enumerable.t/0`
 

   
   Creates a stream that enumerates each enumerable in an enumerable.
   
   **Examples**
   
   ::
   
       iex> stream = Stream.concat([1..3, 4..6, 7..9])
       iex> Enum.to_list(stream)
       [1,2,3,4,5,6,7,8,9]
   
   
   

.. elixir:function:: Stream.concat/2
   :sig: concat(first, second)


   Specs:
   
 
   * concat(:elixir:type:`Enumerable.t/0`, :elixir:type:`Enumerable.t/0`) :: :elixir:type:`Enumerable.t/0`
 

   
   Creates a stream that enumerates the first argument, followed by the
   second.
   
   **Examples**
   
   ::
   
       iex> stream = Stream.concat(1..3, 4..6)
       iex> Enum.to_list(stream)
       [1,2,3,4,5,6]
   
       iex> stream1 = Stream.cycle([1, 2, 3])
       iex> stream2 = Stream.cycle([4, 5, 6])
       iex> stream = Stream.concat(stream1, stream2)
       iex> Enum.take(stream, 6)
       [1,2,3,1,2,3]
   
   
   

.. elixir:function:: Stream.cycle/1
   :sig: cycle(enumerable)


   Specs:
   
 
   * cycle(:elixir:type:`Enumerable.t/0`) :: :elixir:type:`Enumerable.t/0`
 

   
   Creates a stream that cycles through the given enumerable, infinitely.
   
   **Examples**
   
   ::
   
       iex> stream = Stream.cycle([1,2,3])
       iex> Enum.take(stream, 5)
       [1,2,3,1,2]
   
   
   

.. elixir:function:: Stream.drop/2
   :sig: drop(enum, n)


   Specs:
   
 
   * drop(:elixir:type:`Enumerable.t/0`, non_neg_integer) :: :elixir:type:`Enumerable.t/0`
 

   
   Lazily drops the next ``n`` items from the enumerable.
   
   If a negative ``n`` is given, it will drop the last ``n`` items from the
   collection. Note that the mechanism by which this is implemented will
   delay the emission of any item until ``n`` additional items have been
   emitted by the enum.
   
   **Examples**
   
   ::
   
       iex> stream = Stream.drop(1..10, 5)
       iex> Enum.to_list(stream)
       [6,7,8,9,10]
   
       iex> stream = Stream.drop(1..10, -5)
       iex> Enum.to_list(stream)
       [1,2,3,4,5]
   
   
   

.. elixir:function:: Stream.drop_while/2
   :sig: drop_while(enum, fun)


   Specs:
   
 
   * drop_while(:elixir:type:`Enumerable.t/0`, (:elixir:type:`element/0` -> as_boolean(term))) :: :elixir:type:`Enumerable.t/0`
 

   
   Lazily drops elements of the enumerable while the given function returns
   ``true``.
   
   **Examples**
   
   ::
   
       iex> stream = Stream.drop_while(1..10, &(&1 <= 5))
       iex> Enum.to_list(stream)
       [6,7,8,9,10]
   
   
   

.. elixir:function:: Stream.each/2
   :sig: each(enum, fun)


   Specs:
   
 
   * each(:elixir:type:`Enumerable.t/0`, (:elixir:type:`element/0` -> term)) :: :elixir:type:`Enumerable.t/0`
 

   
   Execute the given function for each item.
   
   Useful for adding side effects (like printing) to a stream.
   
   **Examples**
   
   ::
   
       iex> stream = Stream.each([1, 2, 3], fn(x) -> send self, x end)
       iex> Enum.to_list(stream)
       iex> receive do: (x when is_integer(x) -> x)
       1
       iex> receive do: (x when is_integer(x) -> x)
       2
       iex> receive do: (x when is_integer(x) -> x)
       3
   
   
   

.. elixir:function:: Stream.filter/2
   :sig: filter(enum, fun)


   Specs:
   
 
   * filter(:elixir:type:`Enumerable.t/0`, (:elixir:type:`element/0` -> as_boolean(term))) :: :elixir:type:`Enumerable.t/0`
 

   
   Creates a stream that filters elements according to the given function
   on enumeration.
   
   **Examples**
   
   ::
   
       iex> stream = Stream.filter([1, 2, 3], fn(x) -> rem(x, 2) == 0 end)
       iex> Enum.to_list(stream)
       [2]
   
   
   

.. elixir:function:: Stream.filter_map/3
   :sig: filter_map(enum, filter, mapper)


   Specs:
   
 
   * filter_map(:elixir:type:`Enumerable.t/0`, (:elixir:type:`element/0` -> as_boolean(term)), (:elixir:type:`element/0` -> any)) :: :elixir:type:`Enumerable.t/0`
 

   
   Creates a stream that filters and then maps elements according to given
   functions.
   
   Exists for symmetry with :elixir:func:`Enum.filter_map/3`.
   
   **Examples**
   
   ::
   
       iex> stream = Stream.filter_map(1..6, fn(x) -> rem(x, 2) == 0 end, &(&1 * 2))
       iex> Enum.to_list(stream)
       [4,8,12]
   
   
   

.. elixir:function:: Stream.flat_map/2
   :sig: flat_map(enum, mapper)


   Specs:
   
 
   * flat_map(:elixir:type:`Enumerable.t/0`, (:elixir:type:`element/0` -> :elixir:type:`Enumerable.t/0`)) :: :elixir:type:`Enumerable.t/0`
 

   
   Creates a stream that will apply the given function on enumeration and
   flatten the result.
   
   **Examples**
   
   ::
   
       iex> stream = Stream.flat_map([1, 2, 3], fn(x) -> [x, x * 2] end)
       iex> Enum.to_list(stream)
       [1, 2, 2, 4, 3, 6]
   
   
   

.. elixir:function:: Stream.into/3
   :sig: into(enum, collectable, transform \\ fn x -> x end)


   
   Injects the stream values into the given collectable as a side-effect.
   
   This function is often used with :elixir:func:`run/1` since any evaluation is
   delayed until the stream is executed. See :elixir:func:`run/1` for an example.
   
   

.. elixir:function:: Stream.iterate/2
   :sig: iterate(start_value, next_fun)


   Specs:
   
 
   * iterate(:elixir:type:`element/0`, (:elixir:type:`element/0` -> :elixir:type:`element/0`)) :: :elixir:type:`Enumerable.t/0`
 

   
   Emit a sequence of values, starting with ``start_value``. Successive
   values are generated by calling ``next_fun`` on the previous value.
   
   **Examples**
   
   ::
   
       iex> Stream.iterate(0, &(&1+1)) |> Enum.take(5)
       [0,1,2,3,4]
   
   
   

.. elixir:function:: Stream.map/2
   :sig: map(enum, fun)


   Specs:
   
 
   * map(:elixir:type:`Enumerable.t/0`, (:elixir:type:`element/0` -> any)) :: :elixir:type:`Enumerable.t/0`
 

   
   Creates a stream that will apply the given function on enumeration.
   
   **Examples**
   
   ::
   
       iex> stream = Stream.map([1, 2, 3], fn(x) -> x * 2 end)
       iex> Enum.to_list(stream)
       [2,4,6]
   
   
   

.. elixir:function:: Stream.reject/2
   :sig: reject(enum, fun)


   Specs:
   
 
   * reject(:elixir:type:`Enumerable.t/0`, (:elixir:type:`element/0` -> as_boolean(term))) :: :elixir:type:`Enumerable.t/0`
 

   
   Creates a stream that will reject elements according to the given
   function on enumeration.
   
   **Examples**
   
   ::
   
       iex> stream = Stream.reject([1, 2, 3], fn(x) -> rem(x, 2) == 0 end)
       iex> Enum.to_list(stream)
       [1,3]
   
   
   

.. elixir:function:: Stream.repeatedly/1
   :sig: repeatedly(generator_fun)


   Specs:
   
 
   * repeatedly((() -> :elixir:type:`element/0`)) :: :elixir:type:`Enumerable.t/0`
 

   
   Returns a stream generated by calling ``generator_fun`` repeatedly.
   
   **Examples**
   
   ::
   
       iex> Stream.repeatedly(&:random.uniform/0) |> Enum.take(3)
       [0.4435846174457203, 0.7230402056221108, 0.94581636451987]
   
   
   

.. elixir:function:: Stream.resource/3
   :sig: resource(start_fun, next_fun, after_fun)


   Specs:
   
 
   * resource((() -> :elixir:type:`acc/0`), (:elixir:type:`acc/0` -> {:elixir:type:`element/0`, :elixir:type:`acc/0`} | nil), (:elixir:type:`acc/0` -> term)) :: :elixir:type:`Enumerable.t/0`
 

   
   Emits a sequence of values for the given resource.
   
   Similar to :elixir:func:`unfold/2` but the initial value is computed lazily via
   ``start_fun`` and executes an ``after_fun`` at the end of enumeration
   (both in cases of success and failure).
   
   Successive values are generated by calling ``next_fun`` with the
   previous accumulator (the initial value being the result returned by
   ``start_fun``) and it must return a tuple with the current and next
   accumulator. The enumeration finishes if it returns ``nil``.
   
   As the name says, this function is useful to stream values from
   resources.
   
   **Examples**
   
   ::
   
       Stream.resource(fn -> File.open!("sample") end,
                       fn file ->
                         case IO.read(file, :line) do
                           data when is_binary(data) -> {data, file}
                           _ -> nil
                         end
                       end,
                       fn file -> File.close(file) end)
   
   
   

.. elixir:function:: Stream.run/1
   :sig: run(stream)


   Specs:
   
 
   * run(:elixir:type:`Enumerable.t/0`) :: :ok
 

   
   Runs the given stream.
   
   This is useful when a stream needs to be run, for side effects, and
   there is no interest in its return result.
   
   **Examples**
   
   Open up a file, replace all ``#`` by ``%`` and stream to another file
   without loading the whole file in memory:
   
   ::
   
       stream = File.stream!("code")
       |> Stream.map(&String.replace(&1, "#", "%"))
       |> Stream.into(File.stream!("new"))
   
   No computation will be done until we call one of the Enum functions or
   :elixir:func:`Stream.run/1`.
   
   

.. elixir:function:: Stream.scan/2
   :sig: scan(enum, fun)


   Specs:
   
 
   * scan(:elixir:type:`Enumerable.t/0`, (:elixir:type:`element/0`, :elixir:type:`acc/0` -> any)) :: :elixir:type:`Enumerable.t/0`
 

   
   Creates a stream that applies the given function to each element, emits
   the result and uses the same result as the accumulator for the next
   computation.
   
   **Examples**
   
   ::
   
       iex> stream = Stream.scan(1..5, &(&1 + &2))
       iex> Enum.to_list(stream)
       [1,3,6,10,15]
   
   
   

.. elixir:function:: Stream.scan/3
   :sig: scan(enum, acc, fun)


   Specs:
   
 
   * scan(:elixir:type:`Enumerable.t/0`, :elixir:type:`acc/0`, (:elixir:type:`element/0`, :elixir:type:`acc/0` -> any)) :: :elixir:type:`Enumerable.t/0`
 

   
   Creates a stream that applies the given function to each element, emits
   the result and uses the same result as the accumulator for the next
   computation. Uses the given ``acc`` as the starting value.
   
   **Examples**
   
   ::
   
       iex> stream = Stream.scan(1..5, 0, &(&1 + &2))
       iex> Enum.to_list(stream)
       [1,3,6,10,15]
   
   
   

.. elixir:function:: Stream.take/2
   :sig: take(enum, n)


   Specs:
   
 
   * take(:elixir:type:`Enumerable.t/0`, non_neg_integer) :: :elixir:type:`Enumerable.t/0`
 

   
   Lazily takes the next ``n`` items from the enumerable and stops
   enumeration.
   
   If a negative ``n`` is given, the last ``n`` values will be taken. For
   such, the collection is fully enumerated keeping up to ``2 * n``
   elements in memory. Once the end of the collection is reached, the last
   ``count`` elements will be executed. Therefore, using a negative ``n``
   on an infinite collection will never return.
   
   **Examples**
   
   ::
   
       iex> stream = Stream.take(1..100, 5)
       iex> Enum.to_list(stream)
       [1,2,3,4,5]
   
       iex> stream = Stream.take(1..100, -5)
       iex> Enum.to_list(stream)
       [96,97,98,99,100]
   
       iex> stream = Stream.cycle([1, 2, 3]) |> Stream.take(5)
       iex> Enum.to_list(stream)
       [1,2,3,1,2]
   
   
   

.. elixir:function:: Stream.take_every/2
   :sig: take_every(enum, n)


   Specs:
   
 
   * take_every(:elixir:type:`Enumerable.t/0`, non_neg_integer) :: :elixir:type:`Enumerable.t/0`
 

   
   Creates a stream that takes every ``n`` item from the enumerable.
   
   The first item is always included, unless ``n`` is 0.
   
   **Examples**
   
   ::
   
       iex> stream = Stream.take_every(1..10, 2)
       iex> Enum.to_list(stream)
       [1,3,5,7,9]
   
   
   

.. elixir:function:: Stream.take_while/2
   :sig: take_while(enum, fun)


   Specs:
   
 
   * take_while(:elixir:type:`Enumerable.t/0`, (:elixir:type:`element/0` -> as_boolean(term))) :: :elixir:type:`Enumerable.t/0`
 

   
   Lazily takes elements of the enumerable while the given function returns
   ``true``.
   
   **Examples**
   
   ::
   
       iex> stream = Stream.take_while(1..100, &(&1 <= 5))
       iex> Enum.to_list(stream)
       [1,2,3,4,5]
   
   
   

.. elixir:function:: Stream.transform/3
   :sig: transform(enum, acc, reducer)


   Specs:
   
 
   * (transform(:elixir:type:`Enumerable.t/0`, acc, fun) :: :elixir:type:`Enumerable.t/0`) when fun: (:elixir:type:`element/0`, acc -> {:elixir:type:`Enumerable.t/0`, acc} | {:halt, acc}), acc: any
 

   
   Transforms an existing stream.
   
   It expects an accumulator and a function that receives each stream item
   and an accumulator, and must return a tuple containing a new stream
   (often a list) with the new accumulator or a tuple with ``:halt`` as
   first element and the accumulator as second.
   
   Note: this function is similar to :elixir:func:`Enum.flat_map_reduce/3` except the
   latter returns both the flat list and accumulator, while this one
   returns only the stream.
   
   **Examples**
   
   :elixir:func:`Stream.transform/3` is a useful as it can be used as basis to
   implement many of the functions defined in this module. For example, we
   can implement ``Stream.take(enum, n)`` as follows:
   
   ::
   
       iex> enum = 1..100
       iex> n = 3
       iex> stream = Stream.transform(enum, 0, fn i, acc ->
       ...>   if acc < n, do: {[i], acc + 1}, else: {:halt, acc}
       ...> end)
       iex> Enum.to_list(stream)
       [1,2,3]
   
   
   

.. elixir:function:: Stream.unfold/2
   :sig: unfold(next_acc, next_fun)


   Specs:
   
 
   * unfold(:elixir:type:`acc/0`, (:elixir:type:`acc/0` -> {:elixir:type:`element/0`, :elixir:type:`acc/0`} | nil)) :: :elixir:type:`Enumerable.t/0`
 

   
   Emits a sequence of values for the given accumulator.
   
   Successive values are generated by calling ``next_fun`` with the
   previous accumulator and it must return a tuple with the current and
   next accumulator. The enumeration finishes if it returns ``nil``.
   
   **Examples**
   
   ::
   
       iex> Stream.unfold(5, fn 0 -> nil; n -> {n, n-1} end) |> Enum.to_list()
       [5, 4, 3, 2, 1]
   
   
   

.. elixir:function:: Stream.uniq/2
   :sig: uniq(enum, fun \\ fn x -> x end)


   Specs:
   
 
   * uniq(:elixir:type:`Enumerable.t/0`, (:elixir:type:`element/0` -> term)) :: :elixir:type:`Enumerable.t/0`
 

   
   Creates a stream that only emits elements if they are unique.
   
   Keep in mind that, in order to know if an element is unique or not, this
   function needs to store all unique values emitted by the stream.
   Therefore, if the stream is infinite, the number of items stored will
   grow infinitely, never being garbage collected.
   
   **Examples**
   
   ::
   
       iex> Stream.uniq([1, 2, 3, 2, 1]) |> Enum.to_list
       [1, 2, 3]
   
       iex> Stream.uniq([{1, :x}, {2, :y}, {1, :z}], fn {x, _} -> x end) |> Enum.to_list
       [{1,:x}, {2,:y}]
   
   
   

.. elixir:function:: Stream.with_index/1
   :sig: with_index(enum)


   Specs:
   
 
   * with_index(:elixir:type:`Enumerable.t/0`) :: :elixir:type:`Enumerable.t/0`
 

   
   Creates a stream where each item in the enumerable will be wrapped in a
   tuple alongside its index.
   
   **Examples**
   
   ::
   
       iex> stream = Stream.with_index([1, 2, 3])
       iex> Enum.to_list(stream)
       [{1,0},{2,1},{3,2}]
   
   
   

.. elixir:function:: Stream.zip/2
   :sig: zip(left, right)


   Specs:
   
 
   * zip(:elixir:type:`Enumerable.t/0`, :elixir:type:`Enumerable.t/0`) :: :elixir:type:`Enumerable.t/0`
 

   
   Zips two collections together, lazily.
   
   The zipping finishes as soon as any enumerable completes.
   
   **Examples**
   
   ::
   
       iex> concat = Stream.concat(1..3, 4..6)
       iex> cycle  = Stream.cycle([:a, :b, :c])
       iex> Stream.zip(concat, cycle) |> Enum.to_list
       [{1,:a},{2,:b},{3,:c},{4,:a},{5,:b},{6,:c}]
   
   
   







