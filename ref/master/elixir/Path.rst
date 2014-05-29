Path
==============================================================

.. elixir:module:: Path

   :mtype: 

Overview
--------

This module provides conveniences for manipulating or retrieving file
system paths.

The functions in this module may receive a char data as argument (i.e. a
string or a list of characters / string) and will always return a string
(encoded in UTF-8).

The majority of the functions in this module do not interact with the
file system, except for a few functions that require it (like
:elixir:func:`wildcard/1` and :elixir:func:`expand/1`).





Summary
-------

================================ =
:elixir:func:`absname/1`         Converts the given path to an absolute one. Unlike :elixir:func:`expand/1`, no attempt is made to resolve ``..``, ``.`` or ``~`` 

:elixir:func:`absname/2`         Builds a path from ``relative_to`` to ``path``. If ``path`` is already an absolute path, ``relative_to`` is ignored. See also :elixir:func:`relative_to/2` 

:elixir:func:`basename/1`        Returns the last component of the path or the path itself if it does not contain any directory separators 

:elixir:func:`basename/2`        Returns the last component of ``path`` with the ``extension`` stripped. This function should be used to remove a specific extension which may, or may not, be there 

:elixir:func:`dirname/1`         Returns the directory component of ``path`` 

:elixir:func:`expand/1`          Converts the path to an absolute one and expands any ``.`` and ``..`` characters and a leading ``~`` 

:elixir:func:`expand/2`          Expands the path relative to the path given as the second argument expanding any ``.`` and ``..`` characters. If the path is already an absolute path, ``relative_to`` is ignored 

:elixir:func:`extname/1`         Returns the extension of the last component of ``path`` 

:elixir:func:`join/1`            Returns a string with one or more path components joined by the path separator 

:elixir:func:`join/2`            Joins two paths 

:elixir:func:`relative/1`        Forces the path to be a relative path 

:elixir:func:`relative_to/2`     Returns the given ``path`` relative to the given ``from`` path. In other words, it tries to strip the ``from`` prefix from ``path`` 

:elixir:func:`relative_to_cwd/1` Convenience to get the path relative to the current working directory. If, for some reason, the current working directory cannot be retrieved, returns the full path 

:elixir:func:`rootname/1`        Returns the ``path`` with the ``extension`` stripped 

:elixir:func:`rootname/2`        Returns the ``path`` with the ``extension`` stripped. This function should be used to remove a specific extension which might, or might not, be there 

:elixir:func:`split/1`           Returns a list with the path split by the path separator. If an empty string is given, returns the root path 

:elixir:func:`type/1`            Returns the path type 

:elixir:func:`wildcard/1`        Traverses paths according to the given ``glob`` expression 
================================ =



Types
-----

.. elixir:type:: Path.t/0

   :elixir:type:`t/0` :: :unicode.chardata
   





Functions
---------

.. elixir:function:: Path.absname/1
   :sig: absname(path)


   Specs:
   
 
   * absname(:elixir:type:`t/0`) :: binary
 

   
   Converts the given path to an absolute one. Unlike :elixir:func:`expand/1`, no
   attempt is made to resolve ``..``, ``.`` or ``~``.
   
   **Unix examples**
   
   ::
   
       Path.absname("foo")
       #=> "/usr/local/foo"
   
       Path.absname("../x")
       #=> "/usr/local/../x"
   
   **Windows**
   
   ::
   
       Path.absname("foo").
       "D:/usr/local/foo"
       Path.absname("../x").
       "D:/usr/local/../x"
   
   
   

.. elixir:function:: Path.absname/2
   :sig: absname(path, relative_to)


   Specs:
   
 
   * absname(:elixir:type:`t/0`, :elixir:type:`t/0`) :: binary
 

   
   Builds a path from ``relative_to`` to ``path``. If ``path`` is already
   an absolute path, ``relative_to`` is ignored. See also
   :elixir:func:`relative_to/2`.
   
   Unlike :elixir:func:`expand/2`, no attempt is made to resolve ``..``, ``.`` or
   ``~``.
   
   **Examples**
   
   ::
   
       iex> Path.absname("foo", "bar")
       "bar/foo"
   
       iex> Path.absname("../x", "bar")
       "bar/../x"
   
   
   

.. elixir:function:: Path.basename/1
   :sig: basename(path)


   Specs:
   
 
   * basename(:elixir:type:`t/0`) :: binary
 

   
   Returns the last component of the path or the path itself if it does not
   contain any directory separators.
   
   **Examples**
   
   ::
   
       iex> Path.basename("foo")
       "foo"
   
       iex> Path.basename("foo/bar")
       "bar"
   
       iex> Path.basename("/")
       ""
   
   
   

.. elixir:function:: Path.basename/2
   :sig: basename(path, extension)


   Specs:
   
 
   * basename(:elixir:type:`t/0`, :elixir:type:`t/0`) :: binary
 

   
   Returns the last component of ``path`` with the ``extension`` stripped.
   This function should be used to remove a specific extension which may,
   or may not, be there.
   
   **Examples**
   
   ::
   
       iex> Path.basename("~/foo/bar.ex", ".ex")
       "bar"
   
       iex> Path.basename("~/foo/bar.exs", ".ex")
       "bar.exs"
   
       iex> Path.basename("~/foo/bar.old.ex", ".ex")
       "bar.old"
   
   
   

.. elixir:function:: Path.dirname/1
   :sig: dirname(path)


   Specs:
   
 
   * dirname(:elixir:type:`t/0`) :: binary
 

   
   Returns the directory component of ``path``.
   
   **Examples**
   
   ::
   
       Path.dirname("/foo/bar.ex")
       #=> "/foo"
       Path.dirname("/foo/bar/baz.ex")
       #=> "/foo/bar"
   
   
   

.. elixir:function:: Path.expand/1
   :sig: expand(path)


   Specs:
   
 
   * expand(:elixir:type:`t/0`) :: binary
 

   
   Converts the path to an absolute one and expands any ``.`` and ``..``
   characters and a leading ``~``.
   
   **Examples**
   
   ::
   
       Path.expand("/foo/bar/../bar")
       "/foo/bar"
   
   
   

.. elixir:function:: Path.expand/2
   :sig: expand(path, relative_to)


   Specs:
   
 
   * expand(:elixir:type:`t/0`, :elixir:type:`t/0`) :: binary
 

   
   Expands the path relative to the path given as the second argument
   expanding any ``.`` and ``..`` characters. If the path is already an
   absolute path, ``relative_to`` is ignored.
   
   Note, that this function treats ``path`` with a leading ``~`` as an
   absolute one.
   
   The second argument is first expanded to an absolute path.
   
   **Examples**
   
   ::
   
       # Assuming that the absolute path to baz is /quux/baz
       Path.expand("foo/bar/../bar", "baz")
       #=> "/quux/baz/foo/bar"
   
       Path.expand("foo/bar/../bar", "/baz")
       "/baz/foo/bar"
       Path.expand("/foo/bar/../bar", "/baz")
       "/foo/bar"
   
   
   

.. elixir:function:: Path.extname/1
   :sig: extname(path)


   Specs:
   
 
   * extname(:elixir:type:`t/0`) :: binary
 

   
   Returns the extension of the last component of ``path``.
   
   **Examples**
   
   ::
   
       iex> Path.extname("foo.erl")
       ".erl"
   
       iex> Path.extname("~/foo/bar")
       ""
   
   
   

.. elixir:function:: Path.join/1
   :sig: join(list1)


   Specs:
   
 
   * join([:elixir:type:`t/0`]) :: binary
 

   
   Returns a string with one or more path components joined by the path
   separator.
   
   This function should be used to convert a list of strings to a path.
   Note that any trailing slash is removed on join.
   
   **Examples**
   
   ::
   
       iex> Path.join(["~", "foo"])
       "~/foo"
   
       iex> Path.join(["foo"])
       "foo"
   
       iex> Path.join(["/", "foo", "bar/"])
       "/foo/bar"
   
   
   

.. elixir:function:: Path.join/2
   :sig: join(left, right)


   Specs:
   
 
   * join(:elixir:type:`t/0`, :elixir:type:`t/0`) :: binary
 

   
   Joins two paths.
   
   **Examples**
   
   ::
   
       iex> Path.join("foo", "bar")
       "foo/bar"
   
   
   

.. elixir:function:: Path.relative/1
   :sig: relative(name)


   Specs:
   
 
   * relative(:elixir:type:`t/0`) :: binary
 

   
   Forces the path to be a relative path.
   
   **Unix examples**
   
   ::
   
       Path.relative("/usr/local/bin")   #=> "usr/local/bin"
       Path.relative("usr/local/bin")    #=> "usr/local/bin"
       Path.relative("../usr/local/bin") #=> "../usr/local/bin"
   
   **Windows examples**
   
   ::
   
       Path.relative("D:/usr/local/bin") #=> "usr/local/bin"
       Path.relative("usr/local/bin")    #=> "usr/local/bin"
       Path.relative("D:bar.ex")         #=> "bar.ex"
       Path.relative("/bar/foo.ex")      #=> "bar/foo.ex"
   
   
   

.. elixir:function:: Path.relative_to/2
   :sig: relative_to(path, from)


   Specs:
   
 
   * relative_to(:elixir:type:`t/0`, :elixir:type:`t/0`) :: binary
 

   
   Returns the given ``path`` relative to the given ``from`` path. In other
   words, it tries to strip the ``from`` prefix from ``path``.
   
   This function does not query the file system, so it assumes no symlinks
   in between the paths.
   
   In case a direct relative path cannot be found, it returns the original
   path.
   
   **Examples**
   
   ::
   
       iex> Path.relative_to("/usr/local/foo", "/usr/local")
       "foo"
   
       iex> Path.relative_to("/usr/local/foo", "/")
       "usr/local/foo"
   
       iex> Path.relative_to("/usr/local/foo", "/etc")
       "/usr/local/foo"
   
   
   

.. elixir:function:: Path.relative_to_cwd/1
   :sig: relative_to_cwd(path)


   Specs:
   
 
   * relative_to_cwd(:elixir:type:`t/0`) :: binary
 

   
   Convenience to get the path relative to the current working directory.
   If, for some reason, the current working directory cannot be retrieved,
   returns the full path.
   
   

.. elixir:function:: Path.rootname/1
   :sig: rootname(path)


   Specs:
   
 
   * rootname(:elixir:type:`t/0`) :: binary
 

   
   Returns the ``path`` with the ``extension`` stripped.
   
   **Examples**
   
   ::
   
       iex> Path.rootname("/foo/bar")
       "/foo/bar"
   
       iex> Path.rootname("/foo/bar.ex")
       "/foo/bar"
   
   
   

.. elixir:function:: Path.rootname/2
   :sig: rootname(path, extension)


   Specs:
   
 
   * rootname(:elixir:type:`t/0`, :elixir:type:`t/0`) :: binary
 

   
   Returns the ``path`` with the ``extension`` stripped. This function
   should be used to remove a specific extension which might, or might not,
   be there.
   
   **Examples**
   
   ::
   
       iex> Path.rootname("/foo/bar.erl", ".erl")
       "/foo/bar"
   
       iex> Path.rootname("/foo/bar.erl", ".ex")
       "/foo/bar.erl"
   
   
   

.. elixir:function:: Path.split/1
   :sig: split(path)


   Specs:
   
 
   * split(:elixir:type:`t/0`) :: [binary]
 

   
   Returns a list with the path split by the path separator. If an empty
   string is given, returns the root path.
   
   **Examples**
   
   ::
   
        iex> Path.split("")
        []
   
        iex> Path.split("foo")
        ["foo"]
   
        iex> Path.split("/foo/bar")
        ["/", "foo", "bar"]
   
   
   

.. elixir:function:: Path.type/1
   :sig: type(name)


   Specs:
   
 
   * type(:elixir:type:`t/0`) :: :absolute | :relative | :volumerelative
 

   
   Returns the path type.
   
   **Unix examples**
   
   ::
   
       Path.type("/usr/local/bin")   #=> :absolute
       Path.type("usr/local/bin")    #=> :relative
       Path.type("../usr/local/bin") #=> :relative
       Path.type("~/file")           #=> :relative
   
   **Windows examples**
   
   ::
   
       Path.type("D:/usr/local/bin") #=> :absolute
       Path.type("usr/local/bin")    #=> :relative
       Path.type("D:bar.ex")         #=> :volumerelative
       Path.type("/bar/foo.ex")      #=> :volumerelative
   
   
   

.. elixir:function:: Path.wildcard/1
   :sig: wildcard(glob)


   Specs:
   
 
   * wildcard(:elixir:type:`t/0`) :: [binary]
 

   
   Traverses paths according to the given ``glob`` expression.
   
   The wildcard looks like an ordinary path, except that certain "wildcard
   characters" are interpreted in a special way. The following characters
   are special:
   
   -  ``?`` - Matches one character.
   -  ``*`` - Matches any number of characters up to the end of the
      filename, the next dot, or the next slash.
   -  ``**`` - Two adjacent \*'s used as a single pattern will match all
      files and zero or more directories and subdirectories.
   -  ``[char1,char2,...]`` - Matches any of the characters listed. Two
      characters separated by a hyphen will match a range of characters.
   -  ``{item1,item2,...}`` - Matches one of the alternatives.
   
   Other characters represent themselves. Only paths that have exactly the
   same character in the same position will match. Note that matching is
   case-sensitive; i.e. "a" will not match "A".
   
   **Examples**
   
   Imagine you have a directory called ``projects`` with three Elixir
   projects inside of it: ``elixir``, ``ex_doc`` and ``dynamo``. You can
   find all ``.beam`` files inside the ``ebin`` directory of each project
   as follows:
   
   ::
   
       Path.wildcard("projects/*/ebin/**/*.beam")
   
   If you want to search for both ``.beam`` and ``.app`` files, you could
   do:
   
   ::
   
       Path.wildcard("projects/*/ebin/**/*.{beam,app}")
   
   
   







