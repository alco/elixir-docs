Record
==============================================================

.. elixir:module:: Record

   :mtype: 

Overview
--------

Module to work, define and import records.

Records are simply tuples where the first element is an atom:

::

    iex> Record.record? {User, "jose", 27}
    true

This module provides conveniences for working with records at
compilation time, where compile-time field names are used to manipulate
the tuples, providing fast operations on top of the tuples compact
structure.

In Elixir, records are used mostly in two situations:

1. To work with short, internal data;
2. To interface with Erlang records;

The macros :elixir:func:`defrecord/3` and :elixir:func:`defrecordp/3` can be used to create
records while :elixir:func:`extract/2` can be used to extract records from Erlang
files.





Summary
-------

============================ =
:elixir:macro:`defrecord/3`  Defines a set of macros to create and access a record 

:elixir:macro:`defrecordp/3` Same as :elixir:func:`defrecord/3` but generates private macros 

:elixir:macro:`extract/2`    Extracts record information from an Erlang file 

:elixir:macro:`record?/1`    Checks if the given ``data`` is a record 

:elixir:macro:`record?/2`    Checks if the given ``data`` is a record of ``kind`` 
============================ =







Macros
------

.. elixir:macro:: Record.defrecord/3
   :sig: defrecord(name, tag \\ nil, kv)


   
   Defines a set of macros to create and access a record.
   
   The macros are going to have ``name``, a tag (which defaults) to the
   name if none is given, and a set of fields given by ``kv``.
   
   **Examples**
   
   ::
   
       defmodule User do
         Record.defrecord :user, [name: "José", age: "25"]
       end
   
   In the example above, a set of macros named ``user`` but with different
   arities will be defined to manipulate the underlying record:
   
   ::
   
       # To create records
       user()        #=> {:user, "José", 25}
       user(age: 26) #=> {:user, "José", 26}
   
       # To get a field from the record
       user(record, :name) #=> "José"
   
       # To update the record
       user(record, age: 26) #=> {:user, "José", 26}
   
   By default, Elixir uses the record name as the first element of the
   tuple (the tag). But it can be changed to something else:
   
   ::
   
       defmodule User do
         Record.defrecord :user, User, name: nil
       end
   
       require User
       User.user() #=> {User, nil}
   
   
   

.. elixir:macro:: Record.defrecordp/3
   :sig: defrecordp(name, tag \\ nil, kv)


   
   Same as :elixir:func:`defrecord/3` but generates private macros.
   
   

.. elixir:macro:: Record.extract/2
   :sig: extract(name, opts)


   
   Extracts record information from an Erlang file.
   
   Returns a quoted expression containing the fields as a list of tuples.
   It expects the record name to be an atom and the library path to be a
   string at expansion time.
   
   **Examples**
   
   ::
   
       iex> Record.extract(:file_info, from_lib: "kernel/include/file.hrl")
       [size: :undefined, type: :undefined, access: :undefined, atime: :undefined,
        mtime: :undefined, ctime: :undefined, mode: :undefined, links: :undefined,
        major_device: :undefined, minor_device: :undefined, inode: :undefined,
        uid: :undefined, gid: :undefined]
   
   
   

.. elixir:macro:: Record.record?/1
   :sig: record?(data)


   
   Checks if the given ``data`` is a record.
   
   This is implemented as a macro so it can be used in guard clauses.
   
   **Examples**
   
   ::
   
       iex> record = {User, "jose", 27}
       iex> Record.record?(record)
       true
       iex> tuple = {}
       iex> Record.record?(tuple)
       false
   
   
   

.. elixir:macro:: Record.record?/2
   :sig: record?(data, kind)


   
   Checks if the given ``data`` is a record of ``kind``.
   
   This is implemented as a macro so it can be used in guard clauses.
   
   **Examples**
   
   ::
   
       iex> record = {User, "jose", 27}
       iex> Record.record?(record, User)
       true
   
   
   





