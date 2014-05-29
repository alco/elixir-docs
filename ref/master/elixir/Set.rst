Set
==============================================================

.. elixir:module:: Set

   :mtype: behaviour

Overview
--------

This module specifies the Set API expected to be implemented by
different representations.

It also provides functions that redirect to the underlying Set, allowing
a developer to work with different Set implementations using one API.

To create a new set, use the ``new`` functions defined by each set type:

::

    HashSet.new  #=> creates an empty HashSet

In the examples below, ``set_impl`` means a specific
```Set`` <Set.html>`__ implementation, for example
```HashSet`` <HashSet.html>`__.

Protocols
~~~~~~~~~

Sets are required to implement both ```Enumerable`` <Enumerable.html>`__
and ```Collectable`` <Collectable.html>`__ protocols.

Match
~~~~~

Sets are required to implement all operations using the match (``===``)
operator.





Summary
-------

============================= =
:elixir:func:`delete/2`       Deletes ``value`` from ``set`` 

:elixir:func:`difference/2`   Returns a set that is ``set1`` without the members of ``set2`` 

:elixir:func:`disjoint?/2`    Checks if ``set1`` and ``set2`` have no members in common 

:elixir:func:`equal?/2`       Check if two sets are equal using ``===`` 

:elixir:func:`intersection/2` Returns a set containing only members in common between ``set1`` and ``set2`` 

:elixir:func:`member?/2`      Checks if ``set`` contains ``value`` 

:elixir:func:`put/2`          Inserts ``value`` into ``set`` if it does not already contain it 

:elixir:func:`size/1`         Returns the number of elements in ``set`` 

:elixir:func:`subset?/2`      Checks if ``set1``'s members are all contained in ``set2`` 

:elixir:func:`to_list/1`      Converts ``set`` to a list 

:elixir:func:`union/2`        Returns a set containing all members of ``set1`` and ``set2`` 
============================= =



Types
-----

.. elixir:type:: Set.value/0

   :elixir:type:`value/0` :: any
   

.. elixir:type:: Set.values/0

   :elixir:type:`values/0` :: [:elixir:type:`value/0`]
   

.. elixir:type:: Set.t/0

   :elixir:type:`t/0` :: %{}
   





Functions
---------

.. elixir:function:: Set.delete/2
   :sig: delete(set, value)


   Specs:
   
 
   * delete(:elixir:type:`t/0`, :elixir:type:`value/0`) :: :elixir:type:`t/0`
 

   
   Deletes ``value`` from ``set``.
   
   **Examples**
   
   ::
   
       iex> s = Enum.into([1, 2, 3], set_impl.new)
       iex> Set.delete(s, 4) |> Enum.sort
       [1, 2, 3]
   
       iex> s = Enum.into([1, 2, 3], set_impl.new)
       iex> Set.delete(s, 2) |> Enum.sort
       [1, 3]
   
   
   

.. elixir:function:: Set.difference/2
   :sig: difference(set1, set2)


   Specs:
   
 
   * difference(:elixir:type:`t/0`, :elixir:type:`t/0`) :: :elixir:type:`t/0`
 

   
   Returns a set that is ``set1`` without the members of ``set2``.
   
   Notice this function is polymorphic as it calculates the difference for
   of any type. Each set implementation also provides a ``difference``
   function, but they can only work with sets of the same type.
   
   **Examples**
   
   ::
   
       iex> Set.difference(Enum.into([1,2], set_impl.new), Enum.into([2,3,4], set_impl.new)) |> Enum.sort
       [1]
   
   
   

.. elixir:function:: Set.disjoint?/2
   :sig: disjoint?(set1, set2)


   Specs:
   
 
   * disjoint?(:elixir:type:`t/0`, :elixir:type:`t/0`) :: boolean
 

   
   Checks if ``set1`` and ``set2`` have no members in common.
   
   Notice this function is polymorphic as it checks for disjoint sets of
   any type. Each set implementation also provides a ``disjoint?``
   function, but they can only work with sets of the same type.
   
   **Examples**
   
   ::
   
       iex> Set.disjoint?(Enum.into([1, 2], set_impl.new), Enum.into([3, 4], set_impl.new))
       true
   
       iex> Set.disjoint?(Enum.into([1, 2], set_impl.new), Enum.into([2, 3], set_impl.new))
       false
   
   
   

.. elixir:function:: Set.equal?/2
   :sig: equal?(set1, set2)


   Specs:
   
 
   * equal?(:elixir:type:`t/0`, :elixir:type:`t/0`) :: boolean
 

   
   Check if two sets are equal using ``===``.
   
   Notice this function is polymorphic as it compares sets of any type.
   Each set implementation also provides an ``equal?`` function, but they
   can only work with sets of the same type.
   
   **Examples**
   
   ::
   
       iex> Set.equal?(Enum.into([1, 2], set_impl.new), Enum.into([2, 1, 1], set_impl.new))
       true
   
       iex> Set.equal?(Enum.into([1, 2], set_impl.new), Enum.into([3, 4], set_impl.new))
       false
   
   
   

.. elixir:function:: Set.intersection/2
   :sig: intersection(set1, set2)


   Specs:
   
 
   * intersection(:elixir:type:`t/0`, :elixir:type:`t/0`) :: :elixir:type:`t/0`
 

   
   Returns a set containing only members in common between ``set1`` and
   ``set2``.
   
   Notice this function is polymorphic as it calculates the intersection of
   any type. Each set implementation also provides a ``intersection``
   function, but they can only work with sets of the same type.
   
   **Examples**
   
   ::
   
       iex> Set.intersection(Enum.into([1,2], set_impl.new), Enum.into([2,3,4], set_impl.new)) |> Enum.sort
       [2]
   
       iex> Set.intersection(Enum.into([1,2], set_impl.new), Enum.into([3,4], set_impl.new)) |> Enum.sort
       []
   
   
   

.. elixir:function:: Set.member?/2
   :sig: member?(set, value)


   Specs:
   
 
   * member?(:elixir:type:`t/0`, :elixir:type:`value/0`) :: boolean
 

   
   Checks if ``set`` contains ``value``.
   
   **Examples**
   
   ::
   
       iex> Set.member?(Enum.into([1, 2, 3], set_impl.new), 2)
       true
   
       iex> Set.member?(Enum.into([1, 2, 3], set_impl.new), 4)
       false
   
   
   

.. elixir:function:: Set.put/2
   :sig: put(set, value)


   Specs:
   
 
   * put(:elixir:type:`t/0`, :elixir:type:`value/0`) :: :elixir:type:`t/0`
 

   
   Inserts ``value`` into ``set`` if it does not already contain it.
   
   **Examples**
   
   ::
   
       iex> Set.put(Enum.into([1, 2, 3], set_impl.new), 3) |> Enum.sort
       [1, 2, 3]
   
       iex> Set.put(Enum.into([1, 2, 3], set_impl.new), 4) |> Enum.sort
       [1, 2, 3, 4]
   
   
   

.. elixir:function:: Set.size/1
   :sig: size(set)


   Specs:
   
 
   * size(:elixir:type:`t/0`) :: non_neg_integer
 

   
   Returns the number of elements in ``set``.
   
   **Examples**
   
   ::
   
       iex> Set.size(Enum.into([1, 2, 3], set_impl.new))
       3
   
   
   

.. elixir:function:: Set.subset?/2
   :sig: subset?(set1, set2)


   Specs:
   
 
   * subset?(:elixir:type:`t/0`, :elixir:type:`t/0`) :: boolean
 

   
   Checks if ``set1``'s members are all contained in ``set2``.
   
   Notice this function is polymorphic as it checks the subset for any
   type. Each set implementation also provides a ``subset?`` function, but
   they can only work with sets of the same type.
   
   **Examples**
   
   ::
   
       iex> Set.subset?(Enum.into([1, 2], set_impl.new), Enum.into([1, 2, 3], set_impl.new))
       true
   
       iex> Set.subset?(Enum.into([1, 2, 3], set_impl.new), Enum.into([1, 2], set_impl.new))
       false
   
   
   

.. elixir:function:: Set.to_list/1
   :sig: to_list(set)


   Specs:
   
 
   * to_list(:elixir:type:`t/0`) :: []
 

   
   Converts ``set`` to a list.
   
   **Examples**
   
   ::
   
       iex> set_impl.to_list(Enum.into([1, 2, 3], set_impl.new)) |> Enum.sort
       [1,2,3]
   
   
   

.. elixir:function:: Set.union/2
   :sig: union(set1, set2)


   Specs:
   
 
   * union(:elixir:type:`t/0`, :elixir:type:`t/0`) :: :elixir:type:`t/0`
 

   
   Returns a set containing all members of ``set1`` and ``set2``.
   
   Notice this function is polymorphic as it calculates the union of any
   type. Each set implementation also provides a ``union`` function, but
   they can only work with sets of the same type.
   
   **Examples**
   
   ::
   
       iex> Set.union(Enum.into([1,2], set_impl.new), Enum.into([2,3,4], set_impl.new)) |> Enum.sort
       [1,2,3,4]
   
   
   







Callbacks
---------

.. elixir:callback:: Set.delete/2
   :sig: delete/2


   Specs:
   
 
   * delete(:elixir:type:`t/0`, :elixir:type:`value/0`) :: :elixir:type:`t/0`
 

   
   
   

.. elixir:callback:: Set.difference/2
   :sig: difference/2


   Specs:
   
 
   * difference(:elixir:type:`t/0`, :elixir:type:`t/0`) :: :elixir:type:`t/0`
 

   
   
   

.. elixir:callback:: Set.disjoint?/2
   :sig: disjoint?/2


   Specs:
   
 
   * disjoint?(:elixir:type:`t/0`, :elixir:type:`t/0`) :: boolean
 

   
   
   

.. elixir:callback:: Set.equal?/2
   :sig: equal?/2


   Specs:
   
 
   * equal?(:elixir:type:`t/0`, :elixir:type:`t/0`) :: boolean
 

   
   
   

.. elixir:callback:: Set.intersection/2
   :sig: intersection/2


   Specs:
   
 
   * intersection(:elixir:type:`t/0`, :elixir:type:`t/0`) :: :elixir:type:`t/0`
 

   
   
   

.. elixir:callback:: Set.member?/2
   :sig: member?/2


   Specs:
   
 
   * member?(:elixir:type:`t/0`, :elixir:type:`value/0`) :: boolean
 

   
   
   

.. elixir:callback:: Set.new/0
   :sig: new/0


   Specs:
   
 
   * new :: :elixir:type:`t/0`
 

   
   
   

.. elixir:callback:: Set.put/2
   :sig: put/2


   Specs:
   
 
   * put(:elixir:type:`t/0`, :elixir:type:`value/0`) :: :elixir:type:`t/0`
 

   
   
   

.. elixir:callback:: Set.size/1
   :sig: size/1


   Specs:
   
 
   * size(:elixir:type:`t/0`) :: non_neg_integer
 

   
   
   

.. elixir:callback:: Set.subset?/2
   :sig: subset?/2


   Specs:
   
 
   * subset?(:elixir:type:`t/0`, :elixir:type:`t/0`) :: boolean
 

   
   
   

.. elixir:callback:: Set.to_list/1
   :sig: to_list/1


   Specs:
   
 
   * to_list(:elixir:type:`t/0`) :: []
 

   
   
   

.. elixir:callback:: Set.union/2
   :sig: union/2


   Specs:
   
 
   * union(:elixir:type:`t/0`, :elixir:type:`t/0`) :: :elixir:type:`t/0`
 

   
   
   



