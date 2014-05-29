Enumerable
==============================================================

.. elixir:module:: Enumerable

   :mtype: protocol

Overview
--------

Enumerable protocol used by :elixir:mod:`Enum` and :elixir:mod:`Stream` modules.

When you invoke a function in the :elixir:mod:`Enum` module, the first argument is
usually a collection that must implement this protocol. For example, the
expression

::

    Enum.map([1, 2, 3], &(&1 * 2))

invokes underneath :elixir:func:`Enumerable.reduce/3` to perform the reducing
operation that builds a mapped list by calling the mapping function
``&(&1 * 2)`` on every element in the collection and cons'ing the
element with an accumulated list.

Internally, :elixir:func:`Enum.map/2` is implemented as follows:

::

    def map(enum, fun) do
      reducer = fn x, acc -> {:cont, [fun.(x)|acc]} end
      Enumerable.reduce(enum, {:cont, []}, reducer) |> elem(1) |> :lists.reverse()
    end

Notice the user given function is wrapped into a ``reducer`` function.
The ``reducer`` function must return a tagged tuple after each step, as
described in the ``acc/0`` type.

The reason the accumulator requires a tagged tuple is to allow the
reducer function to communicate to the underlying enumerable the end of
enumeration, allowing any open resource to be properly closed. It also
allows suspension of the enumeration, which is useful when interleaving
between many enumerables is required (as in zip).

Finally, :elixir:func:`Enumerable.reduce/3` will return another tagged tuple, as
represented by the ``result/0`` type.





Summary
-------

======================== =
:elixir:func:`count/1`   Retrieves the collection's size 

:elixir:func:`member?/2` Checks if a value exists within the collection 

:elixir:func:`reduce/3`  Reduces the collection into a value 
======================== =



Types
-----

.. elixir:type:: Enumerable.acc/0

   :elixir:type:`acc/0` :: {:cont, term} | {:halt, term} | {:suspend, term}
   

   The accumulator value for each step.
   
   It must be a tagged tuple with one of the following "tags":
   
   -  ``:cont`` - the enumeration should continue
   -  ``:halt`` - the enumeration should halt immediately
   -  ``:suspend`` - the enumeration should be suspended immediately
   
   Depending on the accumulator value, the result returned by
   :elixir:func:`Enumerable.reduce/3` will change. Please check the ``result`` type
   docs for more information.
   
   In case a reducer function returns a ``:suspend`` accumulator, it must
   be explicitly handled by the caller and never leak.
   

.. elixir:type:: Enumerable.reducer/0

   :elixir:type:`reducer/0` :: (term, term -> :elixir:type:`acc/0`)
   

   The reducer function.
   
   Should be called with the collection element and the accumulator
   contents. Returns the accumulator for the next enumeration step.
   

.. elixir:type:: Enumerable.result/0

   :elixir:type:`result/0` :: {:done, term} | {:halted, term} | {:suspended, term, :elixir:type:`continuation/0`}
   

   The result of the reduce operation.
   
   It may be *done* when the enumeration is finished by reaching its end,
   or *halted*/*suspended* when the enumeration was halted or suspended by
   the reducer function.
   
   In case a reducer function returns the ``:suspend`` accumulator, the
   ``:suspended`` tuple must be explicitly handled by the caller and never
   leak. In practice, this means regular enumeration functions just need to
   be concerned about ``:done`` and ``:halted`` results.
   
   Furthermore, a ``:suspend`` call must always be followed by another
   call, eventually halting or continuing until the end.
   

.. elixir:type:: Enumerable.continuation/0

   :elixir:type:`continuation/0` :: (:elixir:type:`acc/0` -> :elixir:type:`result/0`)
   

   A partially applied reduce function.
   
   The continuation is the closure returned as a result when the
   enumeration is suspended. When invoked, it expects a new accumulator and
   it returns the result.
   
   A continuation is easily implemented as long as the reduce function is
   defined in a tail recursive fashion. If the function is tail recursive,
   all the state is passed as arguments, so the continuation would simply
   be the reducing function partially applied.
   

.. elixir:type:: Enumerable.t/0

   :elixir:type:`t/0` :: term
   





Functions
---------

.. elixir:function:: Enumerable.count/1
   :sig: count(collection)


   Specs:
   
 
   * count(:elixir:type:`t/0`) :: {:ok, non_neg_integer} | {:error, module}
 

   
   Retrieves the collection's size.
   
   It should return ``{:ok, size}``.
   
   If ``{:error, __MODULE__}`` is returned a default algorithm using
   ``reduce`` and the match (``===``) operator is used. This algorithm runs
   in linear time.
   
   Please force use of the default algorithm unless you can implement an
   algorithm that is significantly faster.
   
   

.. elixir:function:: Enumerable.member?/2
   :sig: member?(collection, value)


   Specs:
   
 
   * member?(:elixir:type:`t/0`, term) :: {:ok, boolean} | {:error, module}
 

   
   Checks if a value exists within the collection.
   
   It should return ``{:ok, boolean}``.
   
   If ``{:error, __MODULE__}`` is returned a default algorithm using
   ``reduce`` and the match (``===``) operator is used. This algorithm runs
   in linear time.
   
   Please force use of the default algorithm unless you can implement an
   algorithm that is significantly faster.
   
   

.. elixir:function:: Enumerable.reduce/3
   :sig: reduce(collection, acc, fun)


   Specs:
   
 
   * reduce(:elixir:type:`t/0`, :elixir:type:`acc/0`, :elixir:type:`reducer/0`) :: :elixir:type:`result/0`
 

   
   Reduces the collection into a value.
   
   Most of the operations in :elixir:mod:`Enum` are implemented in terms of reduce.
   This function should apply the given ``reducer`` function to each item
   in the collection and proceed as expected by the returned accumulator.
   
   As an example, here is the implementation of ``reduce`` for lists:
   
   ::
   
       def reduce(_,     {:halt, acc}, _fun),   do: {:halted, acc}
       def reduce(list,  {:suspend, acc}, fun), do: {:suspended, acc, &reduce(list, &1, fun)}
       def reduce([],    {:cont, acc}, _fun),   do: {:done, acc}
       def reduce([h|t], {:cont, acc}, fun),    do: reduce(t, fun.(h, acc), fun)
   
   
   







