Bitwise
==============================================================

.. elixir:module:: Bitwise

   :mtype: 

Overview
--------

This module provides macros and operators for bitwise operators. These
macros can be used in guards.

The easiest way to use is to simply import them into your module:

::

    iex> use Bitwise
    iex> bnot 1
    -2
    iex> 1 &&& 1
    1

You can select to include only or skip operators by passing options:

::

    iex> use Bitwise, only_operators: true
    iex> 1 &&& 1
    1






Summary
-------

=========================== =
:elixir:macro:`&&&/2`       Bitwise and as operator 

:elixir:macro:`<<</2`       Arithmetic bitshift left as operator 

:elixir:macro:`>>>/2`       Arithmetic bitshift right as operator 

:elixir:macro:`^^^/2`       Bitwise xor as operator 

:elixir:macro:`__using__/1` Allow a developer to use this module in their programs with the following options: 

:elixir:macro:`band/2`      Bitwise and 

:elixir:macro:`bnot/1`      Bitwise not 

:elixir:macro:`bor/2`       Bitwise or 

:elixir:macro:`bsl/2`       Arithmetic bitshift left 

:elixir:macro:`bsr/2`       Arithmetic bitshift right 

:elixir:macro:`bxor/2`      Bitwise xor 

:elixir:macro:`|||/2`       Bitwise or as operator 

:elixir:macro:`~~~/1`       Bitwise not as operator 
=========================== =







Macros
------

.. elixir:macro:: Bitwise.&&&/2
   :sig: left &&& right


   
   Bitwise and as operator.
   
   

.. elixir:macro:: Bitwise.<<</2
   :sig: left <<< right


   
   Arithmetic bitshift left as operator.
   
   

.. elixir:macro:: Bitwise.>>>/2
   :sig: left >>> right


   
   Arithmetic bitshift right as operator.
   
   

.. elixir:macro:: Bitwise.^^^/2
   :sig: left ^^^ right


   
   Bitwise xor as operator.
   
   

.. elixir:macro:: Bitwise.__using__/1
   :sig: __using__(options)


   
   Allow a developer to use this module in their programs with the
   following options:
   
   -  ``:only_operators`` - Include only operators;
   -  ``:skip_operators`` - Skip operators;
   
   
   

.. elixir:macro:: Bitwise.band/2
   :sig: band(left, right)


   
   Bitwise and.
   
   

.. elixir:macro:: Bitwise.bnot/1
   :sig: bnot(expr)


   
   Bitwise not.
   
   

.. elixir:macro:: Bitwise.bor/2
   :sig: bor(left, right)


   
   Bitwise or.
   
   

.. elixir:macro:: Bitwise.bsl/2
   :sig: bsl(left, right)


   
   Arithmetic bitshift left.
   
   

.. elixir:macro:: Bitwise.bsr/2
   :sig: bsr(left, right)


   
   Arithmetic bitshift right.
   
   

.. elixir:macro:: Bitwise.bxor/2
   :sig: bxor(left, right)


   
   Bitwise xor.
   
   

.. elixir:macro:: Bitwise.|||/2
   :sig: left \|\|\| right


   
   Bitwise or as operator.
   
   

.. elixir:macro:: Bitwise.~~~/1
   :sig: ~~~expr


   
   Bitwise not as operator.
   
   





