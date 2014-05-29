Inspect.Algebra
==============================================================

.. elixir:module:: Inspect.Algebra

   :mtype: 

Overview
--------

A set of functions for creating and manipulating algebra documents, as
described in `"Strictly Pretty" (2000) by Christian
Lindig <http://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.34.2200>`__.

An algebra document is represented by an
```Inspect.Algebra`` <Inspect.Algebra.html>`__ node or a regular string.

::

    iex> Inspect.Algebra.empty
    :doc_nil

    iex> "foo"
    "foo"

With the functions in this module, we can concatenate different elements
together and render them:

::

    iex> doc = Inspect.Algebra.concat(Inspect.Algebra.empty, "foo")
    iex> Inspect.Algebra.pretty(doc, 80)
    "foo"

The functions ```nest/2`` <#nest/2>`__, ```space/2`` <#space/2>`__ and
```line/2`` <#line/2>`__ help you put the document together into a rigid
structure. However, the document algebra gets interesting when using
functions like ``break/2``, which converts the given string into a line
break depending on how much space there is to print. Let's glue two docs
together with a break and then render it:

::

    iex> doc = Inspect.Algebra.glue("a", " ", "b")
    iex> Inspect.Algebra.pretty(doc, 80)
    "a b"

Notice the break was represented as is, because we haven't reached a
line limit. Once we do, it is replaced by a newline:

::

    iex> doc = Inspect.Algebra.glue(String.duplicate("a", 20), " ", "b")
    iex> Inspect.Algebra.pretty(doc, 10)
    "aaaaaaaaaaaaaaaaaaaa\nb"

Finally, this module also contains Elixir related functions, a bit tied
to Elixir formatting, namely ```surround/3`` <#surround/3>`__ and
``surround_many/5``.

Implementation details
~~~~~~~~~~~~~~~~~~~~~~

The original Haskell implementation of the algorithm by
`Wadler <http://homepages.inf.ed.ac.uk/wadler/papers/prettier/prettier.pdf>`__
relies on lazy evaluation to unfold document groups on two alternatives:
``:flat`` (breaks as spaces) and ``:break`` (breaks as newlines).
Implementing the same logic in a strict language such as Elixir leads to
an exponential growth of possible documents, unless document groups are
encoded explictly as ``:flat`` or ``:break``. Those groups are then
reduced to a simple document, where the layout is already decided, per
`Lindig <http://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.34.2200>`__.

This implementation slightly changes the semantic of Lindig's algorithm
to allow elements that belong to the same group to be printed together
in the same line, even if they do not fit the line fully. This was
achieved by changing ``:break`` to mean a possible break and ``:flat``
to force a flat structure. Then deciding if a break works as a newline
is just a matter of checking if we have enough space until the next
break that is not inside a group (which is still flat).

Custom pretty printers can be implemented using the documents returned
by this module and by providing their own rendering functions.





Summary
-------

============================== =
:elixir:func:`break/0`         

:elixir:func:`break/1`         Document entity representing a break. This break can be rendered as a linebreak or as spaces, depending on the ``mode`` of the chosen layout or the provided separator 

:elixir:func:`concat/1`        Concatenates a list of documents 

:elixir:func:`concat/2`        Concatenates two document entities. Takes two arguments: left doc and right doc. Returns a DocCons doc 

:elixir:func:`empty/0`         Returns ``:doc_nil`` which is a document entity used to represent nothingness. Takes no arguments 

:elixir:func:`folddoc/2`       Folds a list of document entities into a document entity using a function that is passed as the first argument 

:elixir:func:`glue/2`          Inserts a break between two docs. See ```break/1`` <#break/1>`__ for more info 

:elixir:func:`glue/3`          Inserts a break, passed as the second argument, between two docs, the first and the third arguments 

:elixir:func:`group/1`         Returns a group containing the specified document 

:elixir:func:`line/2`          Inserts a mandatory linebreak between two document entities 

:elixir:func:`nest/2`          Nests document entity ``x`` positions deep. Nesting will be appended to the line breaks 

:elixir:func:`pretty/2`        The pretty printing function 

:elixir:func:`space/2`         Inserts a mandatory single space between two document entities 

:elixir:func:`surround/3`      Surrounds a document with characters 

:elixir:func:`surround_many/6` Maps and glues a collection of items together using the given separator and surrounds them. A limit can be passed which, once reached, stops gluing and outputs "..." instead 

:elixir:func:`to_doc/2`        Converts an Elixir structure to an algebra document according to the inspect protocol 
============================== =



Types
-----

.. elixir:type:: Inspect.Algebra.t/0

   :elixir:type:`t/0` :: :doc_nil | :doc_line | doc_cons | doc_nest | doc_break | doc_group | binary
   





Functions
---------

.. elixir:function:: Inspect.Algebra.break/0
   :sig: break()


   Specs:
   
 
   * break :: doc_break
 

   
   
   

.. elixir:function:: Inspect.Algebra.break/1
   :sig: break(s)


   Specs:
   
 
   * break(binary) :: doc_break
 

   
   Document entity representing a break. This break can be rendered as a
   linebreak or as spaces, depending on the ``mode`` of the chosen layout
   or the provided separator.
   
   **Examples**
   
   Let's glue two docs together with a break and then render it:
   
   ::
   
       iex> doc = Inspect.Algebra.glue("a", " ", "b")
       iex> Inspect.Algebra.pretty(doc, 80)
       "a b"
   
   Notice the break was represented as is, because we haven't reached a
   line limit. Once we do, it is replaced by a newline:
   
   ::
   
       iex> doc = Inspect.Algebra.glue(String.duplicate("a", 20), " ", "b")
       iex> Inspect.Algebra.pretty(doc, 10)
       "aaaaaaaaaaaaaaaaaaaa\nb"
   
   
   

.. elixir:function:: Inspect.Algebra.concat/1
   :sig: concat(docs)


   Specs:
   
 
   * concat([:elixir:type:`t/0`]) :: doc_cons
 

   
   Concatenates a list of documents.
   
   

.. elixir:function:: Inspect.Algebra.concat/2
   :sig: concat(x, y)


   Specs:
   
 
   * concat(:elixir:type:`t/0`, :elixir:type:`t/0`) :: doc_cons
 

   
   Concatenates two document entities. Takes two arguments: left doc and
   right doc. Returns a DocCons doc
   
   **Examples**
   
   ::
   
       iex> doc = Inspect.Algebra.concat "Tasteless", "Artosis"
       iex> Inspect.Algebra.pretty(doc, 80)
       "TastelessArtosis"
   
   
   

.. elixir:function:: Inspect.Algebra.empty/0
   :sig: empty()


   Specs:
   
 
   * empty :: :doc_nil
 

   
   Returns ``:doc_nil`` which is a document entity used to represent
   nothingness. Takes no arguments.
   
   **Examples**
   
   ::
   
       iex> Inspect.Algebra.empty
       :doc_nil
   
   
   

.. elixir:function:: Inspect.Algebra.folddoc/2
   :sig: folddoc(list1, f)


   Specs:
   
 
   * folddoc([:elixir:type:`t/0`], (:elixir:type:`t/0`, :elixir:type:`t/0` -> :elixir:type:`t/0`)) :: :elixir:type:`t/0`
 

   
   Folds a list of document entities into a document entity using a
   function that is passed as the first argument.
   
   **Examples**
   
   ::
   
       iex> doc = ["A", "B"]
       iex> doc = Inspect.Algebra.folddoc(doc, fn(x,y) ->
       ...>   Inspect.Algebra.concat [x, "!", y]
       ...> end)
       iex> Inspect.Algebra.pretty(doc, 80)
       "A!B"
   
   
   

.. elixir:function:: Inspect.Algebra.glue/2
   :sig: glue(x, y)


   Specs:
   
 
   * glue(:elixir:type:`t/0`, :elixir:type:`t/0`) :: doc_cons
 

   
   Inserts a break between two docs. See ```break/1`` <#break/1>`__ for
   more info.
   
   

.. elixir:function:: Inspect.Algebra.glue/3
   :sig: glue(x, g, y)


   Specs:
   
 
   * glue(:elixir:type:`t/0`, binary, :elixir:type:`t/0`) :: doc_cons
 

   
   Inserts a break, passed as the second argument, between two docs, the
   first and the third arguments.
   
   

.. elixir:function:: Inspect.Algebra.group/1
   :sig: group(d)


   Specs:
   
 
   * group(:elixir:type:`t/0`) :: doc_group
 

   
   Returns a group containing the specified document.
   
   **Examples**
   
   ::
   
       iex> doc = Inspect.Algebra.group(
       ...>   Inspect.Algebra.concat(
       ...>     Inspect.Algebra.group(
       ...>       Inspect.Algebra.concat(
       ...>         "Hello,",
       ...>         Inspect.Algebra.concat(
       ...>           Inspect.Algebra.break,
       ...>           "A"
       ...>         )
       ...>       )
       ...>     ),
       ...>     Inspect.Algebra.concat(
       ...>       Inspect.Algebra.break,
       ...>       "B"
       ...>     )
       ...> ))
       iex> Inspect.Algebra.pretty(doc, 80)
       "Hello, A B"
       iex> Inspect.Algebra.pretty(doc, 6)
       "Hello,\nA B"
   
   
   

.. elixir:function:: Inspect.Algebra.line/2
   :sig: line(x, y)


   Specs:
   
 
   * line(:elixir:type:`t/0`, :elixir:type:`t/0`) :: doc_cons
 

   
   Inserts a mandatory linebreak between two document entities.
   
   **Examples**
   
   ::
   
       iex> doc = Inspect.Algebra.line "Hughes", "Wadler"
       iex> Inspect.Algebra.pretty(doc, 80)
       "Hughes\nWadler"
   
   
   

.. elixir:function:: Inspect.Algebra.nest/2
   :sig: nest(x, i)


   Specs:
   
 
   * nest(:elixir:type:`t/0`, non_neg_integer) :: doc_nest
 

   
   Nests document entity ``x`` positions deep. Nesting will be appended to
   the line breaks.
   
   **Examples**
   
   ::
   
       iex> doc = Inspect.Algebra.nest(Inspect.Algebra.concat(Inspect.Algebra.break, "6"), 5)
       iex> Inspect.Algebra.pretty(doc, 80)
       " 6"
   
   
   

.. elixir:function:: Inspect.Algebra.pretty/2
   :sig: pretty(d, w)


   Specs:
   
 
   * pretty(:elixir:type:`t/0`, non_neg_integer | :infinity) :: binary
 

   
   The pretty printing function.
   
   Takes the maximum width and a document to print as its arguments and
   returns the string representation of the best layout for the document to
   fit in the given width.
   
   

.. elixir:function:: Inspect.Algebra.space/2
   :sig: space(x, y)


   Specs:
   
 
   * space(:elixir:type:`t/0`, :elixir:type:`t/0`) :: doc_cons
 

   
   Inserts a mandatory single space between two document entities.
   
   **Examples**
   
   ::
   
       iex> doc = Inspect.Algebra.space "Hughes", "Wadler"
       iex> Inspect.Algebra.pretty(doc, 80)
       "Hughes Wadler"
   
   
   

.. elixir:function:: Inspect.Algebra.surround/3
   :sig: surround(left, doc, right)


   Specs:
   
 
   * surround(binary, :elixir:type:`t/0`, binary) :: :elixir:type:`t/0`
 

   
   Surrounds a document with characters.
   
   Puts the document between left and right enclosing and nesting it. The
   document is marked as a group, to show the maximum as possible concisely
   together.
   
   **Examples**
   
   ::
   
       iex> doc = Inspect.Algebra.surround "[", Inspect.Algebra.glue("a", "b"), "]"
       iex> Inspect.Algebra.pretty(doc, 3)
       "[a\n b]"
   
   
   

.. elixir:function:: Inspect.Algebra.surround_many/6
   :sig: surround_many(left, docs, right, limit, fun, separator \\ ",")


   Specs:
   
 
   * surround_many(binary, [any], binary, integer | :infinity, (term -> :elixir:type:`t/0`), binary) :: :elixir:type:`t/0`
 

   
   Maps and glues a collection of items together using the given separator
   and surrounds them. A limit can be passed which, once reached, stops
   gluing and outputs "..." instead.
   
   **Examples**
   
   ::
   
       iex> doc = Inspect.Algebra.surround_many("[", Enum.to_list(1..5), "]", :infinity, &Integer.to_string(&1))
       iex> Inspect.Algebra.pretty(doc, 5)
       "[1,\n 2,\n 3,\n 4,\n 5]"
   
       iex> doc = Inspect.Algebra.surround_many("[", Enum.to_list(1..5), "]", 3, &Integer.to_string(&1))
       iex> Inspect.Algebra.pretty(doc, 20)
       "[1, 2, 3, ...]"
   
       iex> doc = Inspect.Algebra.surround_many("[", Enum.to_list(1..5), "]", 3, &Integer.to_string(&1), "!")
       iex> Inspect.Algebra.pretty(doc, 20)
       "[1! 2! 3! ...]"
   
   
   

.. elixir:function:: Inspect.Algebra.to_doc/2
   :sig: to_doc(map, opts)


   Specs:
   
 
   * to_doc(any, :elixir:type:`Inspect.Opts.t/0`) :: :elixir:type:`t/0`
 

   
   Converts an Elixir structure to an algebra document according to the
   inspect protocol.
   
   







