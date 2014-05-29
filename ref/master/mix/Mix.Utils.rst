Mix.Utils
==============================================================

.. elixir:module:: Mix.Utils

   :mtype: 

Overview
--------

Utilities used throughout Mix and tasks.





Summary
-------

======================================= =
:elixir:func:`camelize/1`               Converts the given string to CamelCase format 

:elixir:func:`command_to_module/2`      Take a ``command`` name and attempts to load a module with the command name converted to a module name in the given ``at`` scope 

:elixir:func:`command_to_module_name/1` Takes a command and converts it to the module name format 

:elixir:func:`extract_files/2`          Extract files from a list of paths 

:elixir:func:`extract_stale/2`          Extract all stale ``sources`` compared to the given ``targets`` 

:elixir:func:`last_modified/1`          Returns the date the given path was last modified 

:elixir:func:`mix_home/0`               Get the mix home 

:elixir:func:`mix_paths/0`              Get all paths defined in the MIX\_PATH env variable 

:elixir:func:`module_name_to_command/2` Takes a module and converts it to a command 

:elixir:func:`read_manifest/1`          Reads the given file as a manifest and returns each entry as a list 

:elixir:func:`read_path!/1`             Opens and reads content from either a URL or a local filesystem path 

:elixir:func:`stale?/2`                 Returns ``true`` if any of the ``sources`` are stale compared to the given ``targets`` 

:elixir:func:`symlink_or_copy/2`        Symlink directory ``source`` to ``target`` or copy it recursively in case symlink fails 

:elixir:func:`underscore/1`             Converts the given atom or binary to underscore format 

:elixir:func:`write_manifest/2`         Writes a manifest file with the given ``entries`` list 
======================================= =





Functions
---------

.. elixir:function:: Mix.Utils.camelize/1
   :sig: camelize(arg1)


   
   Converts the given string to CamelCase format.
   
   **Examples**
   
   ::
   
       iex> Mix.Utils.camelize "foo_bar"
       "FooBar"
   
   
   

.. elixir:function:: Mix.Utils.command_to_module/2
   :sig: command_to_module(command, at \\ Elixir)


   
   Take a ``command`` name and attempts to load a module with the command
   name converted to a module name in the given ``at`` scope.
   
   Returns ``{:module, module}`` in case a module exists and is loaded,
   ``{:error, reason}`` otherwise.
   
   **Examples**
   
   ::
   
       iex> Mix.Utils.command_to_module("compile", Mix.Tasks)
       {:module, Mix.Tasks.Compile}
   
   
   

.. elixir:function:: Mix.Utils.command_to_module_name/1
   :sig: command_to_module_name(s)


   
   Takes a command and converts it to the module name format.
   
   **Examples**
   
   ::
   
       iex> Mix.Utils.command_to_module_name("compile.elixir")
       "Compile.Elixir"
   
   
   

.. elixir:function:: Mix.Utils.extract_files/2
   :sig: extract_files(paths, exts_or_pattern)


   
   Extract files from a list of paths.
   
   ``exts_or_pattern`` may be a list of extensions or a ``Path.wildcard/1``
   pattern.
   
   If the path in ``paths`` is a file, it is included in the return result.
   If it is a directory, it is searched recursively for files with the
   given extensions or matching the given patterns.
   
   Any file starting with ``"."`` is ignored.
   
   

.. elixir:function:: Mix.Utils.extract_stale/2
   :sig: extract_stale(sources, targets)


   
   Extract all stale ``sources`` compared to the given ``targets``.
   
   

.. elixir:function:: Mix.Utils.last_modified/1
   :sig: last_modified(path)


   
   Returns the date the given path was last modified.
   
   If the path does not exist, it returns the unix epoch (1970-01-01
   00:00:00).
   
   

.. elixir:function:: Mix.Utils.mix_home/0
   :sig: mix_home()


   
   Get the mix home.
   
   It defaults to ``~/.mix`` unless the ``MIX_HOME`` environment variable
   is set.
   
   

.. elixir:function:: Mix.Utils.mix_paths/0
   :sig: mix_paths()


   
   Get all paths defined in the MIX\_PATH env variable.
   
   ``MIX_PATH`` may contain multiple paths. If on Windows, those paths
   should be separated by ``;``, if on unix systems, use ``:``.
   
   

.. elixir:function:: Mix.Utils.module_name_to_command/2
   :sig: module_name_to_command(module, nesting \\ 0)


   
   Takes a module and converts it to a command.
   
   The nesting argument can be given in order to remove the nesting of a
   module.
   
   **Examples**
   
   ::
   
       iex> Mix.Utils.module_name_to_command(Mix.Tasks.Compile, 2)
       "compile"
   
       iex> Mix.Utils.module_name_to_command("Mix.Tasks.Compile.Elixir", 2)
       "compile.elixir"
   
   
   

.. elixir:function:: Mix.Utils.read_manifest/1
   :sig: read_manifest(file)


   
   Reads the given file as a manifest and returns each entry as a list.
   
   A manifest is a tabular file where each line is a row and each entry in
   a row is separated by "". The first entry must always be a path to a
   compiled artifact.
   
   In case there is no manifest file, returns an empty list.
   
   

.. elixir:function:: Mix.Utils.read_path!/1
   :sig: read_path!(path)


   
   Opens and reads content from either a URL or a local filesystem path.
   
   Used by tasks like ``local.install`` and ``local.rebar`` that support
   installation either from a URL or a local file.
   
   Raises if the given path is not a url, nor a file or if the file or url
   are invalid.
   
   

.. elixir:function:: Mix.Utils.stale?/2
   :sig: stale?(sources, targets)


   
   Returns ``true`` if any of the ``sources`` are stale compared to the
   given ``targets``.
   
   

.. elixir:function:: Mix.Utils.symlink_or_copy/2
   :sig: symlink_or_copy(source, target)


   
   Symlink directory ``source`` to ``target`` or copy it recursively in
   case symlink fails.
   
   Expect source and target to be absolute paths as it generates a relative
   symlink.
   
   

.. elixir:function:: Mix.Utils.underscore/1
   :sig: underscore(atom)


   
   Converts the given atom or binary to underscore format.
   
   If an atom is given, it is assumed to be an Elixir module, so it is
   converted to a binary and then processed.
   
   **Examples**
   
   ::
   
       iex> Mix.Utils.underscore "FooBar"
       "foo_bar"
   
       iex> Mix.Utils.underscore "Foo.Bar"
       "foo/bar"
   
       iex> Mix.Utils.underscore Foo.Bar
       "foo/bar"
   
   In general, ``underscore`` can be thought of as the reverse of
   ``camelize``, however, in some cases formatting may be lost:
   
   ::
   
       Mix.Utils.underscore "SAPExample"  #=> "sap_example"
       Mix.Utils.camelize   "sap_example" #=> "SapExample"
   
   
   

.. elixir:function:: Mix.Utils.write_manifest/2
   :sig: write_manifest(file, entries)


   
   Writes a manifest file with the given ``entries`` list.
   
   







