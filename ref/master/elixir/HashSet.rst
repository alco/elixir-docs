HashSet
==============================================================

.. elixir:module:: HashSet

   :mtype: 

Overview
--------

A set store.

The ```HashSet`` <HashSet.html>`__ is represented internally as a
struct, therefore ``%HashSet{}`` can be used whenever there is a need to
match on any ```HashSet`` <HashSet.html>`__. Note though the struct
fields are private and must not be accessed directly. Instead, use the
functions on this or in the ```Set`` <Set.html>`__ module.

The ```HashSet`` <HashSet.html>`__ is implemented using tries, which
grows in space as the number of keys grows, working well with both small
and large set of keys. For more information about the functions and
their APIs, please consult the ```Set`` <Set.html>`__ module.





Summary
-------

============================= =
:elixir:func:`delete/2`       Callback implementation of ```Set.delete/2`` <Set.html#delete/2>`__ 

:elixir:func:`difference/2`   Callback implementation of ```Set.difference/2`` <Set.html#difference/2>`__ 

:elixir:func:`disjoint?/2`    Callback implementation of ```Set.disjoint?/2`` <Set.html#disjoint?/2>`__ 

:elixir:func:`equal?/2`       Callback implementation of ```Set.equal?/2`` <Set.html#equal?/2>`__ 

:elixir:func:`intersection/2` Callback implementation of ```Set.intersection/2`` <Set.html#intersection/2>`__ 

:elixir:func:`member?/2`      Callback implementation of ```Set.member?/2`` <Set.html#member?/2>`__ 

:elixir:func:`new/0`          Creates a new empty set 

:elixir:func:`put/2`          Callback implementation of ```Set.put/2`` <Set.html#put/2>`__ 

:elixir:func:`size/1`         Callback implementation of ```Set.size/1`` <Set.html#size/1>`__ 

:elixir:func:`subset?/2`      Callback implementation of ```Set.subset?/2`` <Set.html#subset?/2>`__ 

:elixir:func:`to_list/1`      Callback implementation of ```Set.to_list/1`` <Set.html#to_list/1>`__ 

:elixir:func:`union/2`        Callback implementation of ```Set.union/2`` <Set.html#union/2>`__ 
============================= =



Types
-----

.. elixir:type:: HashSet.t/0

   :elixir:type:`t/0`
   





Functions
---------

.. elixir:function:: HashSet.delete/2
   :sig: delete(set, term)


   
   Callback implementation of ```Set.delete/2`` <Set.html#delete/2>`__.
   
   

.. elixir:function:: HashSet.difference/2
   :sig: difference(set1, set2)


   
   Callback implementation of
   ```Set.difference/2`` <Set.html#difference/2>`__.
   
   

.. elixir:function:: HashSet.disjoint?/2
   :sig: disjoint?(set1, set2)


   
   Callback implementation of
   ```Set.disjoint?/2`` <Set.html#disjoint?/2>`__.
   
   

.. elixir:function:: HashSet.equal?/2
   :sig: equal?(set1, set2)


   
   Callback implementation of ```Set.equal?/2`` <Set.html#equal?/2>`__.
   
   

.. elixir:function:: HashSet.intersection/2
   :sig: intersection(set1, set2)


   
   Callback implementation of
   ```Set.intersection/2`` <Set.html#intersection/2>`__.
   
   

.. elixir:function:: HashSet.member?/2
   :sig: member?(hashset, term)


   
   Callback implementation of ```Set.member?/2`` <Set.html#member?/2>`__.
   
   

.. elixir:function:: HashSet.new/0
   :sig: new()


   Specs:
   
 
   * new :: :elixir:type:`Set.t/0`
 

   
   Creates a new empty set.
   
   

.. elixir:function:: HashSet.put/2
   :sig: put(hashset, term)


   
   Callback implementation of ```Set.put/2`` <Set.html#put/2>`__.
   
   

.. elixir:function:: HashSet.size/1
   :sig: size(hashset)


   
   Callback implementation of ```Set.size/1`` <Set.html#size/1>`__.
   
   

.. elixir:function:: HashSet.subset?/2
   :sig: subset?(set1, set2)


   
   Callback implementation of ```Set.subset?/2`` <Set.html#subset?/2>`__.
   
   

.. elixir:function:: HashSet.to_list/1
   :sig: to_list(set)


   
   Callback implementation of ```Set.to_list/1`` <Set.html#to_list/1>`__.
   
   

.. elixir:function:: HashSet.union/2
   :sig: union(set1, set2)


   
   Callback implementation of ```Set.union/2`` <Set.html#union/2>`__.
   
   







