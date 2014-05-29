IO
==============================================================

.. elixir:module:: IO

   :mtype: 

Overview
--------

Functions handling IO.

Many functions in this module expects an IO device as argument. An IO
device must be a pid or an atom representing a process. For convenience,
Elixir provides ``:stdio`` and ``:stderr`` as shortcuts to Erlang's
``:standard_io`` and ``:standard_error``.

The majority of the functions expect char data, i.e. strings or lists of
characters and strings. In case another type is given, it will do a
conversion to string via the :elixir:mod:`String.Chars` protocol (as shown in
typespecs).

The functions starting with ``bin*`` expects iodata as argument, i.e.
binaries or lists of bytes and binaries.

IO devices
~~~~~~~~~~

An IO device may be an atom or a pid. In case it is an atom, the atom
must be the name of a registered process. However, there are three
exceptions for this rule:

-  ``:standard_io`` - when the ``:standard_io`` atom is given, it is
   treated as a shortcut for ``Process.group_leader``

-  ``:stdio`` - is a shortcut for ``:standard_io``

-  ``:stderr`` - is a shortcut for ``:standard_error``







Summary
-------

=================================== =
:elixir:func:`binread/2`            Reads ``count`` bytes from the IO device or until the end of the line if ``:line`` is given. It returns: 

:elixir:func:`binstream/2`          Converts the IO device into a :elixir:mod:`IO.Stream` 

:elixir:func:`binwrite/2`           Writes the given argument to the given device as a binary, no unicode conversion happens 

:elixir:func:`chardata_to_string/1` Converts chardata (a list of integers representing codepoints, lists and strings) into a string 

:elixir:func:`getn/2`               Gets a number of bytes from the io device. If the io device is a unicode device, ``count`` implies the number of unicode codepoints to be retrieved. Otherwise, ``count`` is the number of raw bytes to be retrieved. It returns: 

:elixir:func:`getn/3`               Gets a number of bytes from the io device. If the io device is a unicode device, ``count`` implies the number of unicode codepoints to be retrieved. Otherwise, ``count`` is the number of raw bytes to be retrieved 

:elixir:func:`gets/2`               Reads a line from the IO device. It returns: 

:elixir:func:`inspect/2`            Inspects and writes the given argument to the device 

:elixir:func:`inspect/3`            Inspects the item with options using the given device 

:elixir:func:`iodata_length/1`      Returns the size of an iodata 

:elixir:func:`iodata_to_binary/1`   Converts iodata (a list of integers representing bytes, lists and binaries) into a binary 

:elixir:func:`puts/2`               Writes the argument to the device, similar to :elixir:func:`write/2`, but adds a newline at the end. The argument is expected to be a chardata 

:elixir:func:`read/2`               Reads ``count`` characters from the IO device or until the end of the line if ``:line`` is given. It returns: 

:elixir:func:`stream/2`             Converts the io device into a :elixir:mod:`IO.Stream` 

:elixir:func:`write/2`              Writes the given argument to the given device 
=================================== =



Types
-----

.. elixir:type:: IO.device/0

   :elixir:type:`device/0` :: atom | pid
   

.. elixir:type:: IO.nodata/0

   :elixir:type:`nodata/0` :: {:error, term} | :eof
   

.. elixir:type:: IO.chardata/0

   :elixir:type:`chardata/0` :: :unicode.chardata
   





Functions
---------

.. elixir:function:: IO.binread/2
   :sig: binread(device \\ :erlang.group_leader(), chars_or_line)


   Specs:
   
 
   * binread(:elixir:type:`device/0`, :line | non_neg_integer) :: iodata | :elixir:type:`nodata/0`
 

   
   Reads ``count`` bytes from the IO device or until the end of the line if
   ``:line`` is given. It returns:
   
   -  ``data`` - The input characters.
   
   -  ``:eof`` - End of file was encountered.
   
   -  ``{:error, reason}`` - Other (rare) error condition, for instance
      ``{:error, :estale}`` if reading from an NFS file system.
   
   
   
   

.. elixir:function:: IO.binstream/2
   :sig: binstream(device, line_or_bytes)


   Specs:
   
 
   * binstream(:elixir:type:`device/0`, :line | pos_integer) :: :elixir:type:`Enumerable.t/0`
 

   
   Converts the IO device into a :elixir:mod:`IO.Stream`.
   
   An :elixir:mod:`IO.Stream` implements both :elixir:mod:`Enumerable` and :elixir:mod:`Collectable`,
   allowing it to be used for both read and write.
   
   The device is iterated line by line or by a number of bytes. This reads
   the IO device as a raw binary.
   
   Note that an IO stream has side effects and every time you go over the
   stream you may get different results.
   
   

.. elixir:function:: IO.binwrite/2
   :sig: binwrite(device \\ :erlang.group_leader(), item)


   Specs:
   
 
   * binwrite(:elixir:type:`device/0`, iodata) :: :ok | {:error, term}
 

   
   Writes the given argument to the given device as a binary, no unicode
   conversion happens.
   
   Check :elixir:func:`write/2` for more information.
   
   

.. elixir:function:: IO.chardata_to_string/1
   :sig: chardata_to_string(string)


   Specs:
   
 
   * chardata_to_string(:elixir:type:`chardata/0`) :: :elixir:type:`String.t/0` | no_return
 

   
   Converts chardata (a list of integers representing codepoints, lists and
   strings) into a string.
   
   In case the conversion fails, it raises a :elixir:mod:`UnicodeConversionError`. If
   a string is given, returns the string itself.
   
   **Examples**
   
   ::
   
       iex> IO.chardata_to_string([0x00E6, 0x00DF])
       "æß"
   
       iex> IO.chardata_to_string([0x0061, "bc"])
       "abc"
   
   
   

.. elixir:function:: IO.getn/2
   :sig: getn(prompt, count \\ 1)


   Specs:
   
 
   * getn(:elixir:type:`device/0`, :elixir:type:`chardata/0` | :elixir:type:`String.Chars.t/0`) :: :elixir:type:`chardata/0` | :elixir:type:`nodata/0`
 
   * getn(:elixir:type:`chardata/0` | :elixir:type:`String.Chars.t/0`, pos_integer) :: :elixir:type:`chardata/0` | :elixir:type:`nodata/0`
 

   
   Gets a number of bytes from the io device. If the io device is a unicode
   device, ``count`` implies the number of unicode codepoints to be
   retrieved. Otherwise, ``count`` is the number of raw bytes to be
   retrieved. It returns:
   
   -  ``data`` - The input characters.
   
   -  ``:eof`` - End of file was encountered.
   
   -  ``{:error, reason}`` - Other (rare) error condition, for instance
      ``{:error, :estale}`` if reading from an NFS file system.
   
   
   
   

.. elixir:function:: IO.getn/3
   :sig: getn(device, prompt, count)


   Specs:
   
 
   * getn(:elixir:type:`device/0`, :elixir:type:`chardata/0` | :elixir:type:`String.Chars.t/0`, pos_integer) :: :elixir:type:`chardata/0` | :elixir:type:`nodata/0`
 

   
   Gets a number of bytes from the io device. If the io device is a unicode
   device, ``count`` implies the number of unicode codepoints to be
   retrieved. Otherwise, ``count`` is the number of raw bytes to be
   retrieved.
   
   

.. elixir:function:: IO.gets/2
   :sig: gets(device \\ :erlang.group_leader(), prompt)


   Specs:
   
 
   * gets(:elixir:type:`device/0`, :elixir:type:`chardata/0` | :elixir:type:`String.Chars.t/0`) :: :elixir:type:`chardata/0` | :elixir:type:`nodata/0`
 

   
   Reads a line from the IO device. It returns:
   
   -  ``data`` - The characters in the line terminated by a LF (or end of
      file).
   
   -  ``:eof`` - End of file was encountered.
   
   -  ``{:error, reason}`` - Other (rare) error condition, for instance
      ``{:error, :estale}`` if reading from an NFS file system.
   
   
   
   

.. elixir:function:: IO.inspect/2
   :sig: inspect(item, opts \\ [])


   Specs:
   
 
   * inspect(term, :elixir:type:`Keyword.t/0`) :: term
 

   
   Inspects and writes the given argument to the device.
   
   It sets by default pretty printing to true and returns the item itself.
   
   Note this function does not use the IO device width because some IO
   devices does not implement the appropriate functions. Setting the width
   must be done explicitly by passing the ``:width`` option.
   
   **Examples**
   
   ::
   
       IO.inspect Process.list
   
   
   

.. elixir:function:: IO.inspect/3
   :sig: inspect(device, item, opts)


   Specs:
   
 
   * inspect(:elixir:type:`device/0`, term, :elixir:type:`Keyword.t/0`) :: term
 

   
   Inspects the item with options using the given device.
   
   

.. elixir:function:: IO.iodata_length/1
   :sig: iodata_length(item)


   Specs:
   
 
   * iodata_length(iodata) :: non_neg_integer
 

   
   Returns the size of an iodata.
   
   Inlined by the compiler.
   
   **Examples**
   
   ::
   
       iex> IO.iodata_length([1, 2|<<3, 4>>])
       4
   
   
   

.. elixir:function:: IO.iodata_to_binary/1
   :sig: iodata_to_binary(item)


   Specs:
   
 
   * iodata_to_binary(iodata) :: binary
 

   
   Converts iodata (a list of integers representing bytes, lists and
   binaries) into a binary.
   
   Notice that this function treats lists of integers as raw bytes and does
   not perform any kind of encoding conversion. If you want to convert from
   a char list to a string (UTF-8 encoded), please use
   :elixir:func:`chardata_to_string/1` instead.
   
   If this function receives a binary, the same binary is returned.
   
   Inlined by the compiler.
   
   **Examples**
   
   ::
   
       iex> bin1 = <<1, 2, 3>>
       iex> bin2 = <<4, 5>>
       iex> bin3 = <<6>>
       iex> IO.iodata_to_binary([bin1, 1, [2, 3, bin2], 4|bin3])
       <<1,2,3,1,2,3,4,5,4,6>>
   
       iex> bin = <<1, 2, 3>>
       iex> IO.iodata_to_binary(bin)
       <<1,2,3>>
   
   
   

.. elixir:function:: IO.puts/2
   :sig: puts(device \\ :erlang.group_leader(), item)


   Specs:
   
 
   * puts(:elixir:type:`device/0`, :elixir:type:`chardata/0` | :elixir:type:`String.Chars.t/0`) :: :ok
 

   
   Writes the argument to the device, similar to :elixir:func:`write/2`, but adds a
   newline at the end. The argument is expected to be a chardata.
   
   

.. elixir:function:: IO.read/2
   :sig: read(device \\ :erlang.group_leader(), chars_or_line)


   Specs:
   
 
   * read(:elixir:type:`device/0`, :line | non_neg_integer) :: :elixir:type:`chardata/0` | :elixir:type:`nodata/0`
 

   
   Reads ``count`` characters from the IO device or until the end of the
   line if ``:line`` is given. It returns:
   
   -  ``data`` - The input characters.
   
   -  ``:eof`` - End of file was encountered.
   
   -  ``{:error, reason}`` - Other (rare) error condition, for instance
      ``{:error, :estale}`` if reading from an NFS file system.
   
   
   
   

.. elixir:function:: IO.stream/2
   :sig: stream(device, line_or_codepoints)


   Specs:
   
 
   * stream(:elixir:type:`device/0`, :line | pos_integer) :: :elixir:type:`Enumerable.t/0`
 

   
   Converts the io device into a :elixir:mod:`IO.Stream`.
   
   An :elixir:mod:`IO.Stream` implements both :elixir:mod:`Enumerable` and :elixir:mod:`Collectable`,
   allowing it to be used for both read and write.
   
   The device is iterated line by line if ``:line`` is given or by a given
   number of codepoints.
   
   This reads the IO as utf-8. Check out :elixir:func:`IO.binstream/2` to handle the
   IO as a raw binary.
   
   Note that an IO stream has side effects and every time you go over the
   stream you may get different results.
   
   **Examples**
   
   Here is an example on how we mimic an echo server from the command line:
   
   ::
   
       Enum.each IO.stream(:stdio, :line), &IO.write(&1)
   
   
   

.. elixir:function:: IO.write/2
   :sig: write(device \\ :erlang.group_leader(), item)


   Specs:
   
 
   * write(:elixir:type:`device/0`, :elixir:type:`chardata/0` | :elixir:type:`String.Chars.t/0`) :: :ok
 

   
   Writes the given argument to the given device.
   
   By default the device is the standard output. It returns ``:ok`` if it
   succeeds.
   
   **Examples**
   
   ::
   
       IO.write "sample"
       #=> "sample"
   
       IO.write :stderr, "error"
       #=> "error"
   
   
   







