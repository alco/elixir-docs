Mix.Archive
==============================================================

.. elixir:module:: Mix.Archive

   :mtype: 

Overview
--------

Module responsible for managing
`archives <http://www.erlang.org/doc/man/code.html>`__.

An archive is a zip file containing the app and beam files. A valid
archive must be named with the name of the application and it should
contain the relative paths beginning with the application name, e.g. the
root of the zip file should be ``my_app/ebin/Elixir.My.App.beam``.





Summary
-------

======================= =
:elixir:func:`create/2` Creates an application archive 

:elixir:func:`dir/1`    Returns the archive internal directory from its ``path`` 

:elixir:func:`ebin/1`   Returns the ebin directory inside the given archive path 

:elixir:func:`name/2`   Returns the archive name based on ``app`` and ``version`` 
======================= =





Functions
---------

.. elixir:function:: Mix.Archive.create/2
   :sig: create(source, target)


   
   Creates an application archive.
   
   It receives the archive file in the format
   ``path/to/archive/app-vsn.ez`` and the path to the root of the project
   to be archived. Everything in the ``ebin`` and ``priv`` directories is
   archived. Dependencies are not archived.
   
   

.. elixir:function:: Mix.Archive.dir/1
   :sig: dir(path)


   
   Returns the archive internal directory from its ``path``.
   
   **Examples**
   
   ::
   
       iex> Mix.Archive.dir("foo/bar/baz-0.1.0.ez")
       "baz-0.1.0"
   
   
   

.. elixir:function:: Mix.Archive.ebin/1
   :sig: ebin(path)


   
   Returns the ebin directory inside the given archive path.
   
   **Examples**
   
   ::
   
       iex> Mix.Archive.ebin("foo/bar/baz-0.1.0.ez")
       "foo/bar/baz-0.1.0.ez/baz-0.1.0/ebin"
   
   
   

.. elixir:function:: Mix.Archive.name/2
   :sig: name(app, vsn)


   
   Returns the archive name based on ``app`` and ``version``.
   
   **Examples**
   
   ::
   
       iex> Mix.Archive.name("foo", nil)
       "foo.ez"
   
       iex> Mix.Archive.name("foo", "0.1.0")
       "foo-0.1.0.ez"
   
   
   







