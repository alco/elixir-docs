File
==============================================================

.. elixir:module:: File

   :mtype: 

Overview
--------

This module contains functions to manipulate files.

Some of those functions are low-level, allowing the user to interact
with the file or IO devices, like ```open/2`` <#open/2>`__,
```copy/3`` <#copy/3>`__ and others. This module also provides higher
level functions that work with filenames and have their naming based on
UNIX variants. For example, one can copy a file via ```cp/3`` <#cp/3>`__
and remove files and directories recursively via
```rm_rf/1`` <#rm_rf/1>`__

Encoding
~~~~~~~~

In order to write and read files, one must use the functions in the
```IO`` <IO.html>`__ module. By default, a file is opened in binary mode
which requires the functions ```IO.binread/2`` <IO.html#binread/2>`__
and ```IO.binwrite/2`` <IO.html#binwrite/2>`__ to interact with the
file. A developer may pass ``:utf8`` as an option when opening the file,
then the slower ```IO.read/2`` <IO.html#read/2>`__ and
```IO.write/2`` <IO.html#write/2>`__ functions must be used as they are
responsible for doing the proper conversions and data guarantees.

Note that filenames when given as char lists in Elixir are always
treated as UTF-8. In particular, we expect that the shell and the
operating system are configured to use UTF8 encoding. Binary filenames
are considering raw and passed to the OS as is.

API
~~~

Most of the functions in this module return ``:ok`` or ``{:ok, result}``
in case of success, ``{:error, reason}`` otherwise. Those function are
also followed by a variant that ends with ``!`` which returns the result
(without the ``{:ok, result}`` tuple) in case of success or raises an
exception in case it fails. For example:

::

    File.read("hello.txt")
    #=> {:ok, "World"}

    File.read("invalid.txt")
    #=> {:error, :enoent}

    File.read!("hello.txt")
    #=> "World"

    File.read!("invalid.txt")
    #=> raises File.Error

In general, a developer should use the former in case he wants to react
if the file does not exist. The latter should be used when the developer
expects his software to fail in case the file cannot be read (i.e. it is
literally an exception).

Processes and raw files
~~~~~~~~~~~~~~~~~~~~~~~

Every time a file is opened, Elixir spawns a new process. Writing to a
file is equivalent to sending messages to that process that writes to
the file descriptor.

This means files can be passed between nodes and message passing
guarantees they can write to the same file in a network.

However, you may not always want to pay the price for this abstraction.
In such cases, a file can be opened in ``:raw`` mode. The options
``:read_ahead`` and ``:delayed_write`` are also useful when operating
large files or working with files in tight loops.

Check http://www.erlang.org/doc/man/file.html#open-2 for more
information about such options and other performance considerations.





Summary
-------

============================ =
:elixir:func:`cd!/1`         The same as ```cd/1`` <#cd/1>`__, but raises an exception if it fails 

:elixir:func:`cd!/2`         Changes the current directory to the given ``path``, executes the given function and then revert back to the previous path regardless if there is an exception 

:elixir:func:`cd/1`          Sets the current working directory 

:elixir:func:`chgrp!/2`      Same as ```chgrp/2`` <#chgrp/2>`__, but raises an exception in case of failure. Otherwise ``:ok`` 

:elixir:func:`chgrp/2`       Changes the user group given by the group id ``gid`` for a given ``file``. Returns ``:ok`` on success, or ``{:error, reason}`` on failure 

:elixir:func:`chmod!/2`      Same as ```chmod/2`` <#chmod/2>`__, but raises an exception in case of failure. Otherwise ``:ok`` 

:elixir:func:`chmod/2`       Changes the unix file ``mode`` for a given ``file``. Returns ``:ok`` on success, or ``{:error, reason}`` on failure 

:elixir:func:`chown!/2`      Same as ```chown/2`` <#chown/2>`__, but raises an exception in case of failure. Otherwise ``:ok`` 

:elixir:func:`chown/2`       Changes the owner given by the user id ``uid`` for a given ``file``. Returns ``:ok`` on success, or ``{:error, reason}`` on failure 

:elixir:func:`close/1`       Closes the file referenced by ``io_device``. It mostly returns ``:ok``, except for some severe errors such as out of memory 

:elixir:func:`copy!/3`       The same as ```copy/3`` <#copy/3>`__ but raises an ```File.CopyError`` <File.CopyError.html>`__ if it fails. Returns the ``bytes_copied`` otherwise 

:elixir:func:`copy/3`        Copies the contents of ``source`` to ``destination`` 

:elixir:func:`cp!/3`         The same as ```cp/3`` <#cp/3>`__, but raises ```File.CopyError`` <File.CopyError.html>`__ if it fails. Returns the list of copied files otherwise 

:elixir:func:`cp/3`          Copies the contents in ``source`` to ``destination`` preserving its mode 

:elixir:func:`cp_r!/3`       The same as ```cp_r/3`` <#cp_r/3>`__, but raises ```File.CopyError`` <File.CopyError.html>`__ if it fails. Returns the list of copied files otherwise 

:elixir:func:`cp_r/3`        Copies the contents in source to destination 

:elixir:func:`cwd!/0`        The same as ```cwd/0`` <#cwd/0>`__, but raises an exception if it fails 

:elixir:func:`cwd/0`         Gets the current working directory 

:elixir:func:`dir?/1`        Returns ``true`` if the path is a directory 

:elixir:func:`exists?/1`     Returns ``true`` if the given path exists. It can be regular file, directory, socket, symbolic link, named pipe or device file 

:elixir:func:`ln_s/2`        Creates a symbolic link ``new`` to the file or directory ``existing`` 

:elixir:func:`ls!/1`         The same as ```ls/1`` <#ls/1>`__ but raises ```File.Error`` <File.Error.html>`__ in case of an error 

:elixir:func:`ls/1`          Returns list of files in the given directory 

:elixir:func:`mkdir!/1`      Same as ```mkdir/1`` <#mkdir/1>`__, but raises an exception in case of failure. Otherwise ``:ok`` 

:elixir:func:`mkdir/1`       Tries to create the directory ``path``. Missing parent directories are not created. Returns ``:ok`` if successful, or ``{:error, reason}`` if an error occurs 

:elixir:func:`mkdir_p!/1`    Same as ```mkdir_p/1`` <#mkdir_p/1>`__, but raises an exception in case of failure. Otherwise ``:ok`` 

:elixir:func:`mkdir_p/1`     Tries to create the directory ``path``. Missing parent directories are created. Returns ``:ok`` if successful, or ``{:error, reason}`` if an error occurs 

:elixir:func:`open!/2`       Same as ```open/2`` <#open/2>`__ but raises an error if file could not be opened. Returns the ``io_device`` otherwise 

:elixir:func:`open!/3`       Same as ```open/3`` <#open/3>`__ but raises an error if file could not be opened. Returns the function result otherwise 

:elixir:func:`open/2`        Opens the given ``path`` according to the given list of modes 

:elixir:func:`open/3`        Similar to ```open/2`` <#open/2>`__ but expects a function as last argument 

:elixir:func:`read!/1`       Returns binary with the contents of the given filename or raises ```File.Error`` <File.Error.html>`__ if an error occurs 

:elixir:func:`read/1`        Returns ``{:ok, binary}``, where ``binary`` is a binary data object that contains the contents of ``path``, or ``{:error, reason}`` if an error occurs 

:elixir:func:`regular?/1`    Returns ``true`` if the path is a regular file 

:elixir:func:`rm!/1`         Same as ```rm/1`` <#rm/1>`__, but raises an exception in case of failure. Otherwise ``:ok`` 

:elixir:func:`rm/1`          Tries to delete the file ``path``. Returns ``:ok`` if successful, or ``{:error, reason}`` if an error occurs 

:elixir:func:`rm_rf!/1`      Same as ```rm_rf/1`` <#rm_rf/1>`__ but raises ```File.Error`` <File.Error.html>`__ in case of failures, otherwise the list of files or directories removed 

:elixir:func:`rm_rf/1`       Remove files and directories recursively at the given ``path``. Symlinks are not followed but simply removed, non-existing files are simply ignored (i.e. doesn't make this function fail) 

:elixir:func:`rmdir!/1`      Same as ```rmdir/1`` <#rmdir/1>`__, but raises an exception in case of failure. Otherwise ``:ok`` 

:elixir:func:`rmdir/1`       Tries to delete the dir at ``path``. Returns ``:ok`` if successful, or ``{:error, reason}`` if an error occurs 

:elixir:func:`stat!/2`       Same as ```stat/2`` <#stat/2>`__ but returns the ```File.Stat`` <File.Stat.html>`__ directly and throws ```File.Error`` <File.Error.html>`__ if an error is returned 

:elixir:func:`stat/2`        Returns information about the ``path``. If it exists, it returns a ``{:ok, info}`` tuple, where info is a ```File.Stat`` <File.Stat.html>`__ struct. Returns ``{:error, reason}`` with the same reasons as ```read/1`` <#read/1>`__ if a failure occurs 

:elixir:func:`stream!/3`     Returns a ```File.Stream`` <File.Stream.html>`__ for the given ``path`` with the given ``modes`` 

:elixir:func:`touch!/2`      Same as ```touch/2`` <#touch/2>`__ but raises an exception if it fails. Returns ``:ok`` otherwise 

:elixir:func:`touch/2`       Updates modification time (mtime) and access time (atime) of the given file. File is created if it doesnât exist 

:elixir:func:`write!/3`      Same as ```write/3`` <#write/3>`__ but raises an exception if it fails, returns ``:ok`` otherwise 

:elixir:func:`write/3`       Writes ``content`` to the file ``path`` 

:elixir:func:`write_stat!/3` Same as ```write_stat/3`` <#write_stat/3>`__ but raises an exception if it fails. Returns ``:ok`` otherwise 

:elixir:func:`write_stat/3`  Writes the given ```File.Stat`` <File.Stat.html>`__ back to the filesystem at the given path. Returns ``:ok`` or ``{:error, reason}`` 
============================ =



Types
-----

.. elixir:type:: File.posix/0

   :elixir:type:`posix/0` :: :file.posix
   

.. elixir:type:: File.io_device/0

   :elixir:type:`io_device/0` :: :file.io_device
   

.. elixir:type:: File.stat_options/0

   :elixir:type:`stat_options/0` :: [{:time, :local | :universal | :posix}]
   





Functions
---------

.. elixir:function:: File.cd/1
   :sig: cd(path)


   Specs:
   
 
   * cd(:elixir:type:`Path.t/0`) :: :ok | {:error, :elixir:type:`posix/0`}
 

   
   Sets the current working directory.
   
   Returns ``:ok`` if successful, ``{:error, reason}`` otherwise.
   
   

.. elixir:function:: File.cd!/1
   :sig: cd!(path)


   Specs:
   
 
   * cd!(:elixir:type:`Path.t/0`) :: :ok | no_return
 

   
   The same as ```cd/1`` <#cd/1>`__, but raises an exception if it fails.
   
   

.. elixir:function:: File.cd!/2
   :sig: cd!(path, function)


   Specs:
   
 
   * (cd!(:elixir:type:`Path.t/0`, (() -> res)) :: res | no_return) when res: var
 

   
   Changes the current directory to the given ``path``, executes the given
   function and then revert back to the previous path regardless if there
   is an exception.
   
   Raises an error if retrieving or changing the current directory fails.
   
   

.. elixir:function:: File.chgrp/2
   :sig: chgrp(path, gid)


   Specs:
   
 
   * chgrp(:elixir:type:`Path.t/0`, integer) :: :ok | {:error, :elixir:type:`posix/0`}
 

   
   Changes the user group given by the group id ``gid`` for a given
   ``file``. Returns ``:ok`` on success, or ``{:error, reason}`` on
   failure.
   
   

.. elixir:function:: File.chgrp!/2
   :sig: chgrp!(path, gid)


   Specs:
   
 
   * chgrp!(:elixir:type:`Path.t/0`, integer) :: :ok | no_return
 

   
   Same as ```chgrp/2`` <#chgrp/2>`__, but raises an exception in case of
   failure. Otherwise ``:ok``.
   
   

.. elixir:function:: File.chmod/2
   :sig: chmod(path, mode)


   Specs:
   
 
   * chmod(:elixir:type:`Path.t/0`, integer) :: :ok | {:error, :elixir:type:`posix/0`}
 

   
   Changes the unix file ``mode`` for a given ``file``. Returns ``:ok`` on
   success, or ``{:error, reason}`` on failure.
   
   

.. elixir:function:: File.chmod!/2
   :sig: chmod!(path, mode)


   Specs:
   
 
   * chmod!(:elixir:type:`Path.t/0`, integer) :: :ok | no_return
 

   
   Same as ```chmod/2`` <#chmod/2>`__, but raises an exception in case of
   failure. Otherwise ``:ok``.
   
   

.. elixir:function:: File.chown/2
   :sig: chown(path, uid)


   Specs:
   
 
   * chown(:elixir:type:`Path.t/0`, integer) :: :ok | {:error, :elixir:type:`posix/0`}
 

   
   Changes the owner given by the user id ``uid`` for a given ``file``.
   Returns ``:ok`` on success, or ``{:error, reason}`` on failure.
   
   

.. elixir:function:: File.chown!/2
   :sig: chown!(path, uid)


   Specs:
   
 
   * chown!(:elixir:type:`Path.t/0`, integer) :: :ok | no_return
 

   
   Same as ```chown/2`` <#chown/2>`__, but raises an exception in case of
   failure. Otherwise ``:ok``.
   
   

.. elixir:function:: File.close/1
   :sig: close(io_device)


   Specs:
   
 
   * close(:elixir:type:`io_device/0`) :: :ok | {:error, :elixir:type:`posix/0` | :badarg | :terminated}
 

   
   Closes the file referenced by ``io_device``. It mostly returns ``:ok``,
   except for some severe errors such as out of memory.
   
   Note that if the option ``:delayed_write`` was used when opening the
   file, ```close/1`` <#close/1>`__ might return an old write error and not
   even try to close the file. See ```open/2`` <#open/2>`__.
   
   

.. elixir:function:: File.copy/3
   :sig: copy(source, destination, bytes_count \\ :infinity)


   Specs:
   
 
   * copy(:elixir:type:`Path.t/0`, :elixir:type:`Path.t/0`, pos_integer | :infinity) :: {:ok, non_neg_integer} | {:error, :elixir:type:`posix/0`}
 

   
   Copies the contents of ``source`` to ``destination``.
   
   Both parameters can be a filename or an io device opened with
   ```open/2`` <#open/2>`__. ``bytes_count`` specifies the number of bytes
   to copy, the default being ``:infinity``.
   
   If file ``destination`` already exists, it is overwritten by the
   contents in ``source``.
   
   Returns ``{:ok, bytes_copied}`` if successful, ``{:error, reason}``
   otherwise.
   
   Compared to the ```cp/3`` <#cp/3>`__, this function is more low-level,
   allowing a copy from device to device limited by a number of bytes. On
   the other hand, ```cp/3`` <#cp/3>`__ performs more extensive checks on
   both source and destination and it also preserves the file mode after
   copy.
   
   Typical error reasons are the same as in ```open/2`` <#open/2>`__,
   ```read/1`` <#read/1>`__ and ```write/3`` <#write/3>`__.
   
   

.. elixir:function:: File.copy!/3
   :sig: copy!(source, destination, bytes_count \\ :infinity)


   Specs:
   
 
   * copy!(:elixir:type:`Path.t/0`, :elixir:type:`Path.t/0`, pos_integer | :infinity) :: non_neg_integer | no_return
 

   
   The same as ```copy/3`` <#copy/3>`__ but raises an
   ```File.CopyError`` <File.CopyError.html>`__ if it fails. Returns the
   ``bytes_copied`` otherwise.
   
   

.. elixir:function:: File.cp/3
   :sig: cp(source, destination, callback \\ fn _, _ -> true end)


   Specs:
   
 
   * cp(:elixir:type:`Path.t/0`, :elixir:type:`Path.t/0`, (:elixir:type:`Path.t/0`, :elixir:type:`Path.t/0` -> boolean)) :: :ok | {:error, :elixir:type:`posix/0`}
 

   
   Copies the contents in ``source`` to ``destination`` preserving its
   mode.
   
   If a file already exists in the destination, it invokes a callback which
   should return ``true`` if the existing file should be overwritten,
   ``false`` otherwise. It defaults to return ``true``.
   
   It returns ``:ok`` in case of success, returns ``{:error, reason}``
   otherwise.
   
   If you want to copy contents from an io device to another device or do a
   straight copy from a source to a destination without preserving modes,
   check ```copy/3`` <#copy/3>`__ instead.
   
   Note: The command ``cp`` in Unix systems behaves differently depending
   if ``destination`` is an existing directory or not. We have chosen to
   explicitly disallow this behaviour. If destination is a directory, an
   error will be returned.
   
   

.. elixir:function:: File.cp!/3
   :sig: cp!(source, destination, callback \\ fn _, _ -> true end)


   Specs:
   
 
   * cp!(:elixir:type:`Path.t/0`, :elixir:type:`Path.t/0`, (:elixir:type:`Path.t/0`, :elixir:type:`Path.t/0` -> boolean)) :: :ok | no_return
 

   
   The same as ```cp/3`` <#cp/3>`__, but raises
   ```File.CopyError`` <File.CopyError.html>`__ if it fails. Returns the
   list of copied files otherwise.
   
   

.. elixir:function:: File.cp_r/3
   :sig: cp_r(source, destination, callback \\ fn _, _ -> true end)


   Specs:
   
 
   * cp_r(:elixir:type:`Path.t/0`, :elixir:type:`Path.t/0`, (:elixir:type:`Path.t/0`, :elixir:type:`Path.t/0` -> boolean)) :: {:ok, [binary]} | {:error, :elixir:type:`posix/0`, binary}
 

   
   Copies the contents in source to destination.
   
   If the source is a file, it copies ``source`` to ``destination``. If the
   source is a directory, it copies the contents inside source into the
   destination.
   
   If a file already exists in the destination, it invokes a callback which
   should return ``true`` if the existing file should be overwritten,
   ``false`` otherwise. It defaults to return ``true``.
   
   If a directory already exists in the destination where a file is meant
   to be (or otherwise), this function will fail.
   
   This function may fail while copying files, in such cases, it will leave
   the destination directory in a dirty state, where already copied files
   won't be removed.
   
   It returns ``{:ok, files_and_directories}`` in case of success with all
   files and directories copied in no specific order,
   ``{:error, reason, file}`` otherwise.
   
   Note: The command ``cp`` in Unix systems behaves differently depending
   if ``destination`` is an existing directory or not. We have chosen to
   explicitly disallow this behaviour.
   
   **Examples**
   
   ::
   
       # Copies "a.txt" to "tmp"
       File.cp_r "a.txt", "tmp.txt"
   
       # Copies all files in "samples" to "tmp"
       File.cp_r "samples", "tmp"
   
       # Same as before, but asks the user how to proceed in case of conflicts
       File.cp_r "samples", "tmp", fn(source, destination) ->
         IO.gets("Overwriting #{destination} by #{source}. Type y to confirm.") == "y"
       end
   
   
   

.. elixir:function:: File.cp_r!/3
   :sig: cp_r!(source, destination, callback \\ fn _, _ -> true end)


   Specs:
   
 
   * cp_r!(:elixir:type:`Path.t/0`, :elixir:type:`Path.t/0`, (:elixir:type:`Path.t/0`, :elixir:type:`Path.t/0` -> boolean)) :: [binary] | no_return
 

   
   The same as ```cp_r/3`` <#cp_r/3>`__, but raises
   ```File.CopyError`` <File.CopyError.html>`__ if it fails. Returns the
   list of copied files otherwise.
   
   

.. elixir:function:: File.cwd/0
   :sig: cwd()


   Specs:
   
 
   * cwd :: {:ok, binary} | {:error, :elixir:type:`posix/0`}
 

   
   Gets the current working directory.
   
   In rare circumstances, this function can fail on Unix. It may happen if
   read permission does not exist for the parent directories of the current
   directory. For this reason, returns ``{:ok, cwd}`` in case of success,
   ``{:error, reason}`` otherwise.
   
   

.. elixir:function:: File.cwd!/0
   :sig: cwd!()


   Specs:
   
 
   * cwd! :: binary | no_return
 

   
   The same as ```cwd/0`` <#cwd/0>`__, but raises an exception if it fails.
   
   

.. elixir:function:: File.dir?/1
   :sig: dir?(path)


   Specs:
   
 
   * dir?(:elixir:type:`Path.t/0`) :: boolean
 

   
   Returns ``true`` if the path is a directory.
   
   

.. elixir:function:: File.exists?/1
   :sig: exists?(path)


   Specs:
   
 
   * exists?(:elixir:type:`Path.t/0`) :: boolean
 

   
   Returns ``true`` if the given path exists. It can be regular file,
   directory, socket, symbolic link, named pipe or device file.
   
   **Examples**
   
   ::
   
       File.exists?("test/")
       #=> true
   
       File.exists?("missing.txt")
       #=> false
   
       File.exists?("/dev/null")
       #=> true
   
   
   

.. elixir:function:: File.ln_s/2
   :sig: ln_s(existing, new)


   
   Creates a symbolic link ``new`` to the file or directory ``existing``.
   
   Returns ``:ok`` if successful, ``{:error, reason}`` otherwise. If the
   operating system does not support symlinks, returns
   ``{:error, :enotsup}``.
   
   

.. elixir:function:: File.ls/1
   :sig: ls(path \\ ".")


   Specs:
   
 
   * ls(:elixir:type:`Path.t/0`) :: {:ok, [binary]} | {:error, :elixir:type:`posix/0`}
 

   
   Returns list of files in the given directory.
   
   It returns ``{:ok, [files]}`` in case of success, ``{:error, reason}``
   otherwise.
   
   

.. elixir:function:: File.ls!/1
   :sig: ls!(path \\ ".")


   Specs:
   
 
   * ls!(:elixir:type:`Path.t/0`) :: [binary] | no_return
 

   
   The same as ```ls/1`` <#ls/1>`__ but raises
   ```File.Error`` <File.Error.html>`__ in case of an error.
   
   

.. elixir:function:: File.mkdir/1
   :sig: mkdir(path)


   Specs:
   
 
   * mkdir(:elixir:type:`Path.t/0`) :: :ok | {:error, :elixir:type:`posix/0`}
 

   
   Tries to create the directory ``path``. Missing parent directories are
   not created. Returns ``:ok`` if successful, or ``{:error, reason}`` if
   an error occurs.
   
   Typical error reasons are:
   
   -  :eacces - Missing search or write permissions for the parent
      directories of ``path``.
   -  :eexist - There is already a file or directory named ``path``.
   -  :enoent - A component of ``path`` does not exist.
   -  :enospc - There is a no space left on the device.
   -  :enotdir - A component of ``path`` is not a directory On some
      platforms, ``:enoent`` is returned instead.
   
   
   

.. elixir:function:: File.mkdir!/1
   :sig: mkdir!(path)


   Specs:
   
 
   * mkdir!(:elixir:type:`Path.t/0`) :: :ok | no_return
 

   
   Same as ```mkdir/1`` <#mkdir/1>`__, but raises an exception in case of
   failure. Otherwise ``:ok``.
   
   

.. elixir:function:: File.mkdir_p/1
   :sig: mkdir_p(path)


   Specs:
   
 
   * mkdir_p(:elixir:type:`Path.t/0`) :: :ok | {:error, :elixir:type:`posix/0`}
 

   
   Tries to create the directory ``path``. Missing parent directories are
   created. Returns ``:ok`` if successful, or ``{:error, reason}`` if an
   error occurs.
   
   Typical error reasons are:
   
   -  :eacces - Missing search or write permissions for the parent
      directories of ``path``.
   -  :enospc - There is a no space left on the device.
   -  :enotdir - A component of ``path`` is not a directory.
   
   
   

.. elixir:function:: File.mkdir_p!/1
   :sig: mkdir_p!(path)


   Specs:
   
 
   * mkdir_p!(:elixir:type:`Path.t/0`) :: :ok | no_return
 

   
   Same as ```mkdir_p/1`` <#mkdir_p/1>`__, but raises an exception in case
   of failure. Otherwise ``:ok``.
   
   

.. elixir:function:: File.open/2
   :sig: open(path, modes \\ [])


   Specs:
   
 
   * open(:elixir:type:`Path.t/0`, []) :: {:ok, :elixir:type:`io_device/0`} | {:error, :elixir:type:`posix/0`}
 

   
   Opens the given ``path`` according to the given list of modes.
   
   In order to write and read files, one must use the functions in the
   ```IO`` <IO.html>`__ module. By default, a file is opened in binary mode
   which requires the functions ```IO.binread/2`` <IO.html#binread/2>`__
   and ```IO.binwrite/2`` <IO.html#binwrite/2>`__ to interact with the
   file. A developer may pass ``:utf8`` as an option when opening the file
   and then all other functions from ```IO`` <IO.html>`__ are available,
   since they work directly with Unicode data.
   
   The allowed modes:
   
   -  ``:read`` - The file, which must exist, is opened for reading.
   
   -  ``:write`` - The file is opened for writing. It is created if it does
      not exist. If the file exists, and if write is not combined with
      read, the file will be truncated.
   
   -  ``:append`` - The file will be opened for writing, and it will be
      created if it does not exist. Every write operation to a file opened
      with append will take place at the end of the file.
   
   -  ``:exclusive`` - The file, when opened for writing, is created if it
      does not exist. If the file exists, open will return
      ``{:error, :eexist}``.
   
   -  ``:char_list`` - When this term is given, read operations on the file
      will return char lists rather than binaries;
   
   -  ``:compressed`` - Makes it possible to read or write gzip compressed
      files. The compressed option must be combined with either read or
      write, but not both. Note that the file size obtained with ``stat/1``
      will most probably not match the number of bytes that can be read
      from a compressed file.
   
   -  ``:utf8`` - This option denotes how data is actually stored in the
      disk file and makes the file perform automatic translation of
      characters to and from utf-8. If data is sent to a file in a format
      that cannot be converted to the utf-8 or if data is read by a
      function that returns data in a format that cannot cope with the
      character range of the data, an error occurs and the file will be
      closed.
   
   Check http://www.erlang.org/doc/man/file.html#open-2 for more
   information about other options like ``:read_ahead`` and
   ``:delayed_write``.
   
   This function returns:
   
   -  ``{:ok, io_device}`` - The file has been opened in the requested
      mode. ``io_device`` is actually the pid of the process which handles
      the file. This process is linked to the process which originally
      opened the file. If any process to which the ``io_device`` is linked
      terminates, the file will be closed and the process itself will be
      terminated. An ``io_device`` returned from this call can be used as
      an argument to the ```IO`` <IO.html>`__ module functions.
   
   -  ``{:error, reason}`` - The file could not be opened.
   
   **Examples**
   
   ::
   
       {:ok, file} = File.open("foo.tar.gz", [:read, :compressed])
       IO.read(file, :line)
       File.close(file)
   
   
   

.. elixir:function:: File.open/3
   :sig: open(path, modes, function)


   Specs:
   
 
   * (open(:elixir:type:`Path.t/0`, [], (:elixir:type:`io_device/0` -> res)) :: {:ok, res} | {:error, :elixir:type:`posix/0`}) when res: var
 

   
   Similar to ```open/2`` <#open/2>`__ but expects a function as last
   argument.
   
   The file is opened, given to the function as argument and automatically
   closed after the function returns, regardless if there was an error or
   not.
   
   It returns ``{:ok, function_result}`` in case of success,
   ``{:error, reason}`` otherwise.
   
   Do not use this function with ``:delayed_write`` option since
   automatically closing the file may fail (as writes are delayed).
   
   **Examples**
   
   ::
   
       File.open("file.txt", [:read, :write], fn(file) ->
         IO.read(file, :line)
       end)
   
   
   

.. elixir:function:: File.open!/2
   :sig: open!(path, modes \\ [])


   Specs:
   
 
   * open!(:elixir:type:`Path.t/0`, []) :: :elixir:type:`io_device/0` | no_return
 

   
   Same as ```open/2`` <#open/2>`__ but raises an error if file could not
   be opened. Returns the ``io_device`` otherwise.
   
   

.. elixir:function:: File.open!/3
   :sig: open!(path, modes, function)


   Specs:
   
 
   * (open!(:elixir:type:`Path.t/0`, [], (:elixir:type:`io_device/0` -> res)) :: res | no_return) when res: var
 

   
   Same as ```open/3`` <#open/3>`__ but raises an error if file could not
   be opened. Returns the function result otherwise.
   
   

.. elixir:function:: File.read/1
   :sig: read(path)


   Specs:
   
 
   * read(:elixir:type:`Path.t/0`) :: {:ok, binary} | {:error, :elixir:type:`posix/0`}
 

   
   Returns ``{:ok, binary}``, where ``binary`` is a binary data object that
   contains the contents of ``path``, or ``{:error, reason}`` if an error
   occurs.
   
   Typical error reasons:
   
   -  :enoent - The file does not exist.
   -  :eacces - Missing permission for reading the file, or for searching
      one of the parent directories.
   -  :eisdir - The named file is a directory.
   -  :enotdir - A component of the file name is not a directory. On some
      platforms, ``:enoent`` is returned instead.
   -  :enomem - There is not enough memory for the contents of the file.
   
   You can use
   ```:file.format_error/1`` <http://www.erlang.org/doc/man/file.html#format_error-1>`__
   to get a descriptive string of the error.
   
   

.. elixir:function:: File.read!/1
   :sig: read!(path)


   Specs:
   
 
   * read!(:elixir:type:`Path.t/0`) :: binary | no_return
 

   
   Returns binary with the contents of the given filename or raises
   ```File.Error`` <File.Error.html>`__ if an error occurs.
   
   

.. elixir:function:: File.regular?/1
   :sig: regular?(path)


   Specs:
   
 
   * regular?(:elixir:type:`Path.t/0`) :: boolean
 

   
   Returns ``true`` if the path is a regular file.
   
   **Examples**
   
   ::
   
       File.regular? __ENV__.file #=> true
   
   
   

.. elixir:function:: File.rm/1
   :sig: rm(path)


   Specs:
   
 
   * rm(:elixir:type:`Path.t/0`) :: :ok | {:error, :elixir:type:`posix/0`}
 

   
   Tries to delete the file ``path``. Returns ``:ok`` if successful, or
   ``{:error, reason}`` if an error occurs.
   
   Typical error reasons are:
   
   -  :enoent - The file does not exist.
   -  :eacces - Missing permission for the file or one of its parents.
   -  :eperm - The file is a directory and user is not super-user.
   -  :enotdir - A component of the file name is not a directory. On some
      platforms, enoent is returned instead.
   -  :einval - Filename had an improper type, such as tuple.
   
   **Examples**
   
   ::
   
       File.rm('file.txt')
       #=> :ok
   
       File.rm('tmp_dir/')
       #=> {:error, :eperm}
   
   
   

.. elixir:function:: File.rm!/1
   :sig: rm!(path)


   Specs:
   
 
   * rm!(:elixir:type:`Path.t/0`) :: :ok | no_return
 

   
   Same as ```rm/1`` <#rm/1>`__, but raises an exception in case of
   failure. Otherwise ``:ok``.
   
   

.. elixir:function:: File.rm_rf/1
   :sig: rm_rf(path)


   Specs:
   
 
   * rm_rf(:elixir:type:`Path.t/0`) :: {:ok, [binary]} | {:error, :elixir:type:`posix/0`, binary}
 

   
   Remove files and directories recursively at the given ``path``. Symlinks
   are not followed but simply removed, non-existing files are simply
   ignored (i.e. doesn't make this function fail).
   
   Returns ``{:ok, files_and_directories}`` with all files and directories
   removed in no specific order, ``{:error, reason, file}`` otherwise.
   
   **Examples**
   
   ::
   
       File.rm_rf "samples"
       #=> {:ok, ["samples", "samples/1.txt"]}
   
       File.rm_rf "unknown"
       #=> {:ok, []}
   
   
   

.. elixir:function:: File.rm_rf!/1
   :sig: rm_rf!(path)


   Specs:
   
 
   * rm_rf!(:elixir:type:`Path.t/0`) :: [binary] | no_return
 

   
   Same as ```rm_rf/1`` <#rm_rf/1>`__ but raises
   ```File.Error`` <File.Error.html>`__ in case of failures, otherwise the
   list of files or directories removed.
   
   

.. elixir:function:: File.rmdir/1
   :sig: rmdir(path)


   Specs:
   
 
   * rmdir(:elixir:type:`Path.t/0`) :: :ok | {:error, :elixir:type:`posix/0`}
 

   
   Tries to delete the dir at ``path``. Returns ``:ok`` if successful, or
   ``{:error, reason}`` if an error occurs.
   
   **Examples**
   
   ::
   
       File.rmdir('tmp_dir')
       #=> :ok
   
       File.rmdir('file.txt')
       #=> {:error, :enotdir}
   
   
   

.. elixir:function:: File.rmdir!/1
   :sig: rmdir!(path)


   Specs:
   
 
   * rmdir!(:elixir:type:`Path.t/0`) :: :ok | {:error, :elixir:type:`posix/0`}
 

   
   Same as ```rmdir/1`` <#rmdir/1>`__, but raises an exception in case of
   failure. Otherwise ``:ok``.
   
   

.. elixir:function:: File.stat/2
   :sig: stat(path, opts \\ [])


   Specs:
   
 
   * stat(:elixir:type:`Path.t/0`, :elixir:type:`stat_options/0`) :: {:ok, :elixir:type:`File.Stat.t/0`} | {:error, :elixir:type:`posix/0`}
 

   
   Returns information about the ``path``. If it exists, it returns a
   ``{:ok, info}`` tuple, where info is a
   ```File.Stat`` <File.Stat.html>`__ struct. Returns ``{:error, reason}``
   with the same reasons as ```read/1`` <#read/1>`__ if a failure occurs.
   
   **Options**
   
   The accepted options are:
   
   -  ``:time`` if the time should be ``:local``, ``:universal`` or
      ``:posix``. Default is ``:local``.
   
   
   

.. elixir:function:: File.stat!/2
   :sig: stat!(path, opts \\ [])


   Specs:
   
 
   * stat!(:elixir:type:`Path.t/0`, :elixir:type:`stat_options/0`) :: :elixir:type:`File.Stat.t/0` | no_return
 

   
   Same as ```stat/2`` <#stat/2>`__ but returns the
   ```File.Stat`` <File.Stat.html>`__ directly and throws
   ```File.Error`` <File.Error.html>`__ if an error is returned.
   
   

.. elixir:function:: File.stream!/3
   :sig: stream!(path, modes \\ [], line_or_bytes \\ :line)


   
   Returns a ```File.Stream`` <File.Stream.html>`__ for the given ``path``
   with the given ``modes``.
   
   The stream implements both ```Enumerable`` <Enumerable.html>`__ and
   ```Collectable`` <Collectable.html>`__ protocols, which means it can be
   used both for read and write.
   
   The ``line_or_byte`` argument configures how the file is read when
   streaming, by ``:line`` (default) or by a given number of bytes.
   
   Operating the stream can fail on open for the same reasons as
   ```File.open!/2`` <File.html#open!/2>`__. Note that the file is
   automatically opened only and every time streaming begins. There is no
   need to pass ``:read`` and ``:write`` modes, as those are automatically
   set by Elixir.
   
   **Raw files**
   
   Since Elixir controls when the streamed file is opened, the underlying
   device cannot be shared and as such it is convenient to open the file in
   raw mode for performance reasons. Therefore, Elixir **will** open
   streams in ``:raw`` mode with the ``:read_ahead`` option unless an
   encoding is specified.
   
   One may also consider passing the ``:delayed_write`` option if the
   stream is meant to be written to under a tight loop.
   
   

.. elixir:function:: File.touch/2
   :sig: touch(path, time \\ :calendar.local_time())


   Specs:
   
 
   * touch(:elixir:type:`Path.t/0`, :calendar.datetime) :: :ok | {:error, :elixir:type:`posix/0`}
 

   
   Updates modification time (mtime) and access time (atime) of the given
   file. File is created if it doesn’t exist.
   
   

.. elixir:function:: File.touch!/2
   :sig: touch!(path, time \\ :calendar.local_time())


   Specs:
   
 
   * touch!(:elixir:type:`Path.t/0`, :calendar.datetime) :: :ok | no_return
 

   
   Same as ```touch/2`` <#touch/2>`__ but raises an exception if it fails.
   Returns ``:ok`` otherwise.
   
   

.. elixir:function:: File.write/3
   :sig: write(path, content, modes \\ [])


   Specs:
   
 
   * write(:elixir:type:`Path.t/0`, iodata, []) :: :ok | {:error, :elixir:type:`posix/0`}
 

   
   Writes ``content`` to the file ``path``.
   
   The file is created if it does not exist. If it exists, the previous
   contents are overwritten. Returns ``:ok`` if successful, or
   ``{:error, reason}`` if an error occurs.
   
   **Warning:** Every time this function is invoked, a file descriptor is
   opened and a new process is spawned to write to the file. For this
   reason, if you are doing multiple writes in a loop, opening the file via
   ```File.open/2`` <File.html#open/2>`__ and using the functions in
   ```IO`` <IO.html>`__ to write to the file will yield much better
   performance then calling this function multiple times.
   
   Typical error reasons are:
   
   -  :enoent - A component of the file name does not exist.
   -  :enotdir - A component of the file name is not a directory. On some
      platforms, enoent is returned instead.
   -  :enospc - There is a no space left on the device.
   -  :eacces - Missing permission for writing the file or searching one of
      the parent directories.
   -  :eisdir - The named file is a directory.
   
   The writing is automatically done in ``:raw`` mode. Check
   ```File.open/2`` <File.html#open/2>`__ for other available options.
   
   

.. elixir:function:: File.write!/3
   :sig: write!(path, content, modes \\ [])


   Specs:
   
 
   * write!(:elixir:type:`Path.t/0`, iodata, []) :: :ok | no_return
 

   
   Same as ```write/3`` <#write/3>`__ but raises an exception if it fails,
   returns ``:ok`` otherwise.
   
   

.. elixir:function:: File.write_stat/3
   :sig: write_stat(path, stat, opts \\ [])


   Specs:
   
 
   * write_stat(:elixir:type:`Path.t/0`, :elixir:type:`File.Stat.t/0`, :elixir:type:`stat_options/0`) :: :ok | {:error, :elixir:type:`posix/0`}
 

   
   Writes the given ```File.Stat`` <File.Stat.html>`__ back to the
   filesystem at the given path. Returns ``:ok`` or ``{:error, reason}``.
   
   

.. elixir:function:: File.write_stat!/3
   :sig: write_stat!(path, stat, opts \\ [])


   Specs:
   
 
   * write_stat!(:elixir:type:`Path.t/0`, :elixir:type:`File.Stat.t/0`, :elixir:type:`stat_options/0`) :: :ok | no_return
 

   
   Same as ```write_stat/3`` <#write_stat/3>`__ but raises an exception if
   it fails. Returns ``:ok`` otherwise.
   
   







