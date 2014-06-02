ExUnit.Assertions
==============================================================

.. elixir:module:: ExUnit.Assertions

   :mtype: 

Overview
--------

This module contains a set of assertion functions that are imported by
default into your test cases.

In general, a developer will want to use the general ``assert`` macro in
tests. This macro tries to be smart and provide good reporting whenever
there is a failure. For example, ``assert some_fun() == 10`` will fail
(assuming ``some_fun()`` returns 13):

Comparison (using ==) failed in: code: some\_fun() == 10 lhs: 13 rhs: 10

This module also provides other convenience functions like
``assert_in_delta`` and ``assert_raise`` to easily handle other common
cases such as checking a floating point number or handling exceptions.





Summary
-------

================================ =
:elixir:func:`assert/1`          Asserts its argument is true 

:elixir:func:`assert/2`          Asserts ``value`` is true, displaying the given ``message`` otherwise 

:elixir:func:`assert/4`          Asserts ``value`` is true. If it fails, it raises an expectation error using the given ``left`` and ``right`` values 

:elixir:func:`assert_in_delta/4` Asserts that ``val1`` and ``val2`` differ by no more than ``delta`` 

:elixir:func:`assert_raise/2`    Asserts the ``exception`` is raised during ``function`` execution. Returns the rescued exception, fails otherwise 

:elixir:func:`assert_raise/3`    Asserts the ``exception`` is raised during ``function`` execution with the ``expected_message``. Returns the rescued exception, fails otherwise 

:elixir:func:`assert_receive/3`  Asserts a message was or is going to be received. Unlike ``assert_received``, it has a default timeout of 100 milliseconds 

:elixir:func:`assert_received/2` Asserts a message was received and is in the current process' mailbox. Timeout is set to 0, so there is no waiting time 

:elixir:func:`catch_error/1`     Asserts ``expression`` will cause an error. Returns the error or fails otherwise 

:elixir:func:`catch_exit/1`      Asserts ``expression`` will exit. Returns the exit status/message or fails otherwise 

:elixir:func:`catch_throw/1`     Asserts ``expression`` will throw a value. Returns the thrown value or fails otherwise 

:elixir:func:`flunk/1`           Fails with a message 

:elixir:func:`refute/1`          This is a negative assertion, failing if its parameter is truthy 

:elixir:func:`refute/2`          Asserts ``value`` is ``nil`` or ``false`` (that is, ``value`` is not truthy) 

:elixir:func:`refute_in_delta/4` Asserts ``val1`` and ``val2`` are not within ``delta`` 

:elixir:func:`refute_receive/3`  refute\_receive message, timeout Â 100, message Â nil 

:elixir:func:`refute_received/2` Asserts a message was not received (i.e. it is not in the current process mailbox). The ``not_expected`` argument must be a match pattern 
================================ =





Functions
---------

.. elixir:function:: ExUnit.Assertions.assert/2
   :sig: assert(value, message)


   
   Asserts ``value`` is true, displaying the given ``message`` otherwise.
   
   **Examples**
   
   ::
   
       assert false, "it will never be true"
   
   
   

.. elixir:function:: ExUnit.Assertions.assert/4
   :sig: assert(value, left, right, message)


   
   Asserts ``value`` is true. If it fails, it raises an expectation error
   using the given ``left`` and ``right`` values.
   
   You probably don't need to use this—the regular ``assert`` function
   handles this for you.
   
   **Examples**
   
   ::
   
       assert this > that, this, that, "more than"
   
   
   

.. elixir:function:: ExUnit.Assertions.assert_in_delta/4
   :sig: assert_in_delta(val1, val2, delta, message \\ nil)


   
   Asserts that ``val1`` and ``val2`` differ by no more than ``delta``.
   
   **Examples**
   
   ::
   
       assert_in_delta 1.1, 1.5, 0.2
       assert_in_delta 10, 15, 4
   
   
   

.. elixir:function:: ExUnit.Assertions.assert_raise/2
   :sig: assert_raise(exception, function)


   
   Asserts the ``exception`` is raised during ``function`` execution.
   Returns the rescued exception, fails otherwise.
   
   **Examples**
   
   ::
   
       assert_raise ArithmeticError, fn ->
         1 + "test"
       end
   
   
   

.. elixir:function:: ExUnit.Assertions.assert_raise/3
   :sig: assert_raise(exception, message, function)


   
   Asserts the ``exception`` is raised during ``function`` execution with
   the ``expected_message``. Returns the rescued exception, fails
   otherwise.
   
   **Examples**
   
   ::
   
       assert_raise ArithmeticError, "bad argument in arithmetic expression", fn ->
         1 + "test"
       end
   
   
   

.. elixir:function:: ExUnit.Assertions.flunk/1
   :sig: flunk(message \\ "Flunked!")


   Specs:
   
 
   * flunk(:elixir:type:`String.t/0`) :: no_return
 

   
   Fails with a message.
   
   **Examples**
   
   ::
   
       flunk "This should raise an error"
   
   
   

.. elixir:function:: ExUnit.Assertions.refute/2
   :sig: refute(value, message)


   
   Asserts ``value`` is ``nil`` or ``false`` (that is, ``value`` is not
   truthy).
   
   **Examples**
   
   ::
   
       refute true, "This will obviously fail"
   
   
   

.. elixir:function:: ExUnit.Assertions.refute_in_delta/4
   :sig: refute_in_delta(val1, val2, delta, message \\ nil)


   
   Asserts ``val1`` and ``val2`` are not within ``delta``.
   
   If you supply ``message``, information about the values will
   automatically be appended to it.
   
   **Examples**
   
   ::
   
       refute_in_delta 1.1, 1.2, 0.2
       refute_in_delta 10, 11, 2
   
   
   





Macros
------

.. elixir:macro:: ExUnit.Assertions.assert/1
   :sig: assert(assertion)


   
   Asserts its argument is true.
   
   ``assert`` tries to be smart and provide good reporting whenever there
   is a failure. In particular, if given a match expression, it will report
   any failure in terms of that match. Given
   
   ::
   
       assert [one] = [two]
   
   you'll see:
   
   ::
   
       match (=) failed
       code: [one] = [two]
       rhs:  [2]
   
   If the expression is a comparison operator, the message will show the
   values of the two sides. The assertion
   
   ::
   
       assert 1+2+3+4 > 15
   
   will fail with the message:
   
   ::
   
       Assertion with > failed
       code: 1+2+3+4 > 15
       lhs:  10
       rhs:  15
   
   
   

.. elixir:macro:: ExUnit.Assertions.assert_receive/3
   :sig: assert_receive(expected, timeout \\ 100, message \\ nil)


   
   Asserts a message was or is going to be received. Unlike
   ``assert_received``, it has a default timeout of 100 milliseconds.
   
   The ``expected`` argument is a pattern.
   
   **Examples**
   
   ::
   
       assert_receive :hello
   
   Asserts against a larger timeout:
   
   ::
   
       assert_receive :hello, 20_000
   
   You can also match against specific patterns:
   
   ::
   
       assert_receive {:hello, _}
   
       x = 5
       assert_receive {:count, ^x}
   
   
   

.. elixir:macro:: ExUnit.Assertions.assert_received/2
   :sig: assert_received(expected, message \\ nil)


   
   Asserts a message was received and is in the current process' mailbox.
   Timeout is set to 0, so there is no waiting time.
   
   The ``expected`` argument is a pattern.
   
   **Examples**
   
   ::
   
       send self, :hello
       assert_received :hello
   
   You can also match against specific patterns:
   
   ::
   
       send self, {:hello, "world"}
       assert_received {:hello, _}
   
   
   

.. elixir:macro:: ExUnit.Assertions.catch_error/1
   :sig: catch_error(expression)


   
   Asserts ``expression`` will cause an error. Returns the error or fails
   otherwise.
   
   **Examples**
   
   ::
   
       assert catch_error(error 1) == 1
   
   
   

.. elixir:macro:: ExUnit.Assertions.catch_exit/1
   :sig: catch_exit(expression)


   
   Asserts ``expression`` will exit. Returns the exit status/message or
   fails otherwise.
   
   **Examples**
   
   ::
   
       assert catch_exit(exit 1) == 1
   
   
   

.. elixir:macro:: ExUnit.Assertions.catch_throw/1
   :sig: catch_throw(expression)


   
   Asserts ``expression`` will throw a value. Returns the thrown value or
   fails otherwise.
   
   **Examples**
   
   ::
   
       assert catch_throw(throw 1) == 1
   
   
   

.. elixir:macro:: ExUnit.Assertions.refute/1
   :sig: refute(assertion)


   
   This is a negative assertion, failing if its parameter is truthy.
   
   **Examples**
   
   ::
   
       refute age < 0
   
   
   

.. elixir:macro:: ExUnit.Assertions.refute_receive/3
   :sig: refute_receive(not_expected, timeout \\ 100, message \\ nil)


   
   ::
   
       refute_receive message, timeout \ 100, message \ nil
   
   Asserts ``message`` was not received (and won't be received) within the
   ``timeout`` period.
   
   The ``not_expected`` argument is a match pattern.
   
   **Examples**
   
   ::
   
       refute_receive :bye
   
   Refute received with a explicit timeout:
   
   ::
   
       refute_receive :bye, 1000
   
   
   

.. elixir:macro:: ExUnit.Assertions.refute_received/2
   :sig: refute_received(not_expected, message \\ nil)


   
   Asserts a message was not received (i.e. it is not in the current
   process mailbox). The ``not_expected`` argument must be a match pattern.
   
   Timeout is set to 0, so there is no waiting time.
   
   **Examples**
   
   ::
   
       send self, :hello
       refute_received :bye
   
   
   





