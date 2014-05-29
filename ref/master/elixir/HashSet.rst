HashSet
==============================================================

.. elixir:module:: HashSet

   :mtype: 

Overview
--------

A set store.

The :elixir:mod:`HashSet` is represented internally as a struct, therefore
``%HashSet{}`` can be used whenever there is a need to match on any
:elixir:mod:`HashSet`. Note though the struct fields are private and must not be
accessed directly. Instead, use the functions on this or in the :elixir:mod:`Set`
module.

The :elixir:mod:`HashSet` is implemented using tries, which grows in space as the
number of keys grows, working well with both small and large set of
keys. For more information about the functions and their APIs, please
consult the :elixir:mod:`Set` module.





Summary
-------

============================= =
:elixir:func:`delete/2`       Callback implementation of :elixir:func:`Set.delete/2` 

:elixir:func:`difference/2`   Callback implementation of :elixir:func:`Set.difference/2` 

:elixir:func:`disjoint?/2`    Callback implementation of :elixir:func:`Set.disjoint?/2` 

:elixir:func:`equal?/2`       Callback implementation of :elixir:func:`Set.equal?/2` 

:elixir:func:`intersection/2` Callback implementation of :elixir:func:`Set.intersection/2` 

:elixir:func:`member?/2`      Callback implementation of :elixir:func:`Set.member?/2` 

:elixir:func:`new/0`          Creates a new empty set 

:elixir:func:`put/2`          Callback implementation of :elixir:func:`Set.put/2` 

:elixir:func:`size/1`         Callback implementation of :elixir:func:`Set.size/1` 

:elixir:func:`subset?/2`      Callback implementation of :elixir:func:`Set.subset?/2` 

:elixir:func:`to_list/1`      Callback implementation of :elixir:func:`Set.to_list/1` 

:elixir:func:`union/2`        Callback implementation of :elixir:func:`Set.union/2` 
============================= =



Types
-----

.. elixir:type:: HashSet.t/0

   :elixir:type:`t/0`
   





Functions
---------

.. elixir:function:: HashSet.delete/2
   :sig: delete(set, term)


   
   Callback implementation of :elixir:func:`Set.delete/2`.
   
   

.. elixir:function:: HashSet.difference/2
   :sig: difference(set1, set2)


   
   Callback implementation of :elixir:func:`Set.difference/2`.
   
   

.. elixir:function:: HashSet.disjoint?/2
   :sig: disjoint?(set1, set2)


   
   Callback implementation of :elixir:func:`Set.disjoint?/2`.
   
   

.. elixir:function:: HashSet.equal?/2
   :sig: equal?(set1, set2)


   
   Callback implementation of :elixir:func:`Set.equal?/2`.
   
   

.. elixir:function:: HashSet.intersection/2
   :sig: intersection(set1, set2)


   
   Callback implementation of :elixir:func:`Set.intersection/2`.
   
   

.. elixir:function:: HashSet.member?/2
   :sig: member?(hashset, term)


   
   Callback implementation of :elixir:func:`Set.member?/2`.
   
   

.. elixir:function:: HashSet.new/0
   :sig: new()


   Specs:
   
 
   * new :: :elixir:type:`Set.t/0`
 

   
   Creates a new empty set.
   
   

.. elixir:function:: HashSet.put/2
   :sig: put(hashset, term)


   
   Callback implementation of :elixir:func:`Set.put/2`.
   
   

.. elixir:function:: HashSet.size/1
   :sig: size(hashset)


   
   Callback implementation of :elixir:func:`Set.size/1`.
   
   

.. elixir:function:: HashSet.subset?/2
   :sig: subset?(set1, set2)


   
   Callback implementation of :elixir:func:`Set.subset?/2`.
   
   

.. elixir:function:: HashSet.to_list/1
   :sig: to_list(set)


   
   Callback implementation of :elixir:func:`Set.to_list/1`.
   
   

.. elixir:function:: HashSet.union/2
   :sig: union(set1, set2)


   
   Callback implementation of :elixir:func:`Set.union/2`.
   
   







