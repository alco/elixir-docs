File.Stat
==============================================================

.. elixir:module:: File.Stat

   :mtype: 

Overview
--------

A struct responsible to hold file information.

In Erlang, this struct is represented by a ``:file_info`` record.
Therefore this module also provides functions for converting in between
the Erlang record and the Elixir struct.

Its fields are:

-  ``size`` - Size of file in bytes.
-  ``type`` - ``:device``, ``:directory``, ``:regular``, ``:other``. The
   type of the file.
-  ``access`` - ``:read``, ``:write``, ``:read_write``, ``:none``. The
   current system access to the file.
-  ``atime`` - The last time the file was read.
-  ``mtime`` - The last time the file was written.
-  ``ctime`` - The interpretation of this time field depends on the
   operating system. On Unix, it is the last time the file or the inode
   was changed. In Windows, it is the create time.
-  ``mode`` - The file permissions.
-  ``links`` - The number of links to this file. This is always 1 for
   file systems which have no concept of links.
-  ``major_device`` - Identifies the file system where the file is
   located. In windows, the number indicates a drive as follows: 0 means
   A:, 1 means B:, and so on.
-  ``minor_device`` - Only valid for character devices on Unix. In all
   other cases, this field is zero.
-  ``inode`` - Gives the inode number. On non-Unix file systems, this
   field will be zero.
-  ``uid`` - Indicates the owner of the file.
-  ``gid`` - Gives the group that the owner of the file belongs to. Will
   be zero for non-Unix file systems.

The time type returned in ``atime``, ``mtime``, and ``ctime`` is
dependent on the time type set in options. ``{:time, type}`` where type
can be ``:local``, ``:universal``, or ``:posix``. Default is ``:local``.





Summary
-------

============================ =
:elixir:func:`from_record/1` Converts a ``:file_info`` record into a ```File.Stat`` <File.Stat.html>`__ 

:elixir:func:`to_record/1`   Converts a ```File.Stat`` <File.Stat.html>`__ struct to a ``:file_info`` record 
============================ =



Types
-----

.. elixir:type:: File.Stat.t/0

   :elixir:type:`t/0` :: %File.Stat{size: term, type: term, access: term, atime: term, mtime: term, ctime: term, mode: term, links: term, major_device: term, minor_device: term, inode: term, uid: term, gid: term}
   





Functions
---------

.. elixir:function:: File.Stat.from_record/1
   :sig: from_record(arg1)


   
   Converts a ``:file_info`` record into a
   ```File.Stat`` <File.Stat.html>`__.
   
   

.. elixir:function:: File.Stat.to_record/1
   :sig: to_record(stat)


   
   Converts a ```File.Stat`` <File.Stat.html>`__ struct to a ``:file_info``
   record.
   
   







