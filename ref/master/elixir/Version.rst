Version
==============================================================

.. elixir:module:: Version

   :mtype: 

Overview
--------

Functions for parsing and matching versions against requirements.

A version is a string in a specific format or a
```Version`` <Version.html>`__ generated after parsing via
```Version.parse/1`` <Version.html#parse/1>`__.

```Version`` <Version.html>`__ parsing and requirements follow `SemVer
2.0 schema <http://semver.org/>`__.

Versions
~~~~~~~~

In a nutshell, a version is given by three numbers:

::

    MAJOR.MINOR.PATCH

Pre-releases are supported by appending ``-[0-9A-Za-z-\.]``:

::

    "1.0.0-alpha.3"

Build information can be added by appending ``+[0-9A-Za-z-\.]``:

::

    "1.0.0-alpha.3+20130417140000"

Struct
~~~~~~

The version is represented by the Version struct and it has its fields
named according to Semver: ``:major``, ``:minor``, ``:patch``, ``:pre``
and ``:build``.

Requirements
~~~~~~~~~~~~

Requirements allow you to specify which versions of a given dependency
you are willing to work against. It supports common operators like
``>=``, ``<=``, ``>``, ``==`` and friends that work as one would expect:

::

    # Only version 2.0.0
    "== 2.0.0"

    # Anything later than 2.0.0
    "> 2.0.0"

Requirements also support ``and`` and ``or`` for complex conditions:

::

    # 2.0.0 and later until 2.1.0
    ">= 2.0.0 and < 2.1.0"

Since the example above is such a common requirement, it can be
expressed as:

::

    "~> 2.0.0"






Summary
-------

================================== =
:elixir:func:`compare/2`           Compares two versions. Returns ``:gt`` if first version is greater than the second and ``:lt`` for vice versa. If the two versions are equal ``:eq`` is returned 

:elixir:func:`match?/2`            Check if the given version matches the specification 

:elixir:func:`parse/1`             Parse a version string into a ```Version`` <Version.html>`__ 

:elixir:func:`parse_requirement/1` Parse a version requirement string into a ``Version.Requirement`` 
================================== =



Types
-----

.. elixir:type:: Version.t/0

   :elixir:type:`t/0` :: %Version{major: term, minor: term, patch: term, pre: term, build: term}
   

.. elixir:type:: Version.version/0

   :elixir:type:`version/0` :: :elixir:type:`String.t/0` | :elixir:type:`t/0`
   

.. elixir:type:: Version.requirement/0

   :elixir:type:`requirement/0` :: :elixir:type:`String.t/0` | :elixir:type:`Version.Requirement.t/0`
   

.. elixir:type:: Version.matchable/0

   :elixir:type:`matchable/0` :: {major :: :elixir:type:`String.t/0` | non_neg_integer, minor :: non_neg_integer | nil, patch :: non_neg_integer | nil, pre :: [:elixir:type:`String.t/0`]}
   





Functions
---------

.. elixir:function:: Version.compare/2
   :sig: compare(vsn1, vsn2)


   Specs:
   
 
   * compare(:elixir:type:`version/0`, :elixir:type:`version/0`) :: :gt | :eq | :lt
 

   
   Compares two versions. Returns ``:gt`` if first version is greater than
   the second and ``:lt`` for vice versa. If the two versions are equal
   ``:eq`` is returned
   
   Raises a
   ```Version.InvalidVersionError`` <Version.InvalidVersionError.html>`__
   exception if ``version`` is not parseable. If given an already parsed
   version this function won't raise.
   
   **Examples**
   
   ::
   
       iex> Version.compare("2.0.1-alpha1", "2.0.0")
       :gt
   
       iex> Version.compare("2.0.1+build0", "2.0.1")
       :eq
   
       iex> Version.compare("invalid", "2.0.1")
       ** (Version.InvalidVersionError) invalid
   
   
   

.. elixir:function:: Version.match?/2
   :sig: match?(vsn, req)


   Specs:
   
 
   * match?(:elixir:type:`version/0`, :elixir:type:`requirement/0`) :: boolean
 

   
   Check if the given version matches the specification.
   
   Returns ``true`` if ``version`` satisfies ``requirement``, ``false``
   otherwise. Raises a
   ```Version.InvalidRequirementError`` <Version.InvalidRequirementError.html>`__
   exception if ``requirement`` is not parseable, or
   ```Version.InvalidVersionError`` <Version.InvalidVersionError.html>`__
   if ``version`` is not parseable. If given an already parsed version and
   requirement this function won't raise.
   
   **Examples**
   
   ::
   
       iex> Version.match?("2.0.0", ">1.0.0")
       true
   
       iex> Version.match?("2.0.0", "==1.0.0")
       false
   
       iex> Version.match?("foo", "==1.0.0")
       ** (Version.InvalidVersionError) foo
   
       iex> Version.match?("2.0.0", "== ==1.0.0")
       ** (Version.InvalidRequirementError) == ==1.0.0
   
   
   

.. elixir:function:: Version.parse/1
   :sig: parse(string)


   Specs:
   
 
   * parse(:elixir:type:`String.t/0`) :: {:ok, :elixir:type:`t/0`} | :error
 

   
   Parse a version string into a ```Version`` <Version.html>`__.
   
   **Examples**
   
   ::
   
       iex> Version.parse("2.0.1-alpha1") |> elem(1)
       #Version<2.0.1-alpha1>
   
       iex> Version.parse("2.0-alpha1")
       :error
   
   
   

.. elixir:function:: Version.parse_requirement/1
   :sig: parse_requirement(string)


   Specs:
   
 
   * parse_requirement(:elixir:type:`String.t/0`) :: {:ok, :elixir:type:`Version.Requirement.t/0`} | :error
 

   
   Parse a version requirement string into a ``Version.Requirement``.
   
   **Examples**
   
   ::
   
       iex> Version.parse_requirement("== 2.0.1") |> elem(1)
       #Version.Requirement<== 2.0.1>
   
       iex> Version.parse_requirement("== == 2.0.1")
       :error
   
   
   







