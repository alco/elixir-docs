Mix.Tasks.Compile.Erlang
==============================================================

.. elixir:module:: Mix.Tasks.Compile.Erlang

   :mtype: 

Overview
--------

Compile Erlang source files.

When this task runs, it will first check the modification times of all
files to be compiled and if they haven't been changed since the last
compilation, it will not compile them. If any of them have changed, it
compiles everything.

For this reason, the task touches your ``:compile_path`` directory and
sets the modification time to the current time and date at the end of
each compilation. You can force compilation regardless of modification
times by passing the ``--force`` option.

Command line options
~~~~~~~~~~~~~~~~~~~~

-  ``--force`` - forces compilation regardless of modification times

Configuration
~~~~~~~~~~~~~

-  ``ERL_COMPILER_OPTIONS`` - can be used to give default compile
   options. The value must be a valid Erlang term. If the value is a
   list, it will be used as is. If it is not a list, it will be put into
   a list.

-  ``:erlc_paths`` - directories to find source files. Defaults to
   ``["src"]``, can be configured as:

``[erlc_paths: ["src", "other"]]``

-  ``:erlc_include_path`` - directory for adding include files. Defaults
   to ``"include"``, can be configured as:

``[erlc_include_path: "other"]``

-  ``:erlc_options`` - compilation options that apply to Erlang's
   compiler. ``:debug_info`` is enabled by default.

There are many available options here:
http://www.erlang.org/doc/man/compile.html#file-2





Summary
-------

================================= =
:elixir:func:`compile_mappings/6` Extracts the extensions from the mappings, automatically invoking the callback for each stale input and output pair (or for all if ``force`` is true) and removing files that no longer have a source, while keeping the manifest up to date 

:elixir:func:`manifests/0`        Returns Erlang manifests 

:elixir:func:`run/1`              Runs this task 

:elixir:func:`to_erl_file/1`      Converts the given file to a format accepted by the Erlang compilation tools 
================================= =





Functions
---------

.. elixir:function:: Mix.Tasks.Compile.Erlang.compile_mappings/6
   :sig: compile_mappings(manifest, mappings, src_ext, dest_ext, force, callback)


   
   Extracts the extensions from the mappings, automatically invoking the
   callback for each stale input and output pair (or for all if ``force``
   is true) and removing files that no longer have a source, while keeping
   the manifest up to date.
   
   **Examples**
   
   For example, a simple compiler for Lisp Flavored Erlang would be
   implemented like:
   
   ::
   
       compile_mappings ".compile.lfe",
                        [{"src", "ebin"}],
                        :lfe, :beam, opts[:force], fn
         input, output ->
           :lfe_comp.file(to_erl_file(input),
                          [output_dir: Path.dirname(output)])
       end
   
   The command above will:
   
   1. Look for files ending with the ``lfe`` extension in ``src`` and their
      ``beam`` counterpart in ``ebin``;
   2. For each stale file (or for all if ``force`` is true), invoke the
      callback passing the calculated input and output;
   3. Update the manifest with the newly compiled outputs;
   4. Remove any output in the manifest that that does not have an
      equivalent source;
   
   The callback must return ``{:ok, mod}`` or ``:error`` in case of error.
   An error is raised at the end if any of the files failed to compile.
   
   

.. elixir:function:: Mix.Tasks.Compile.Erlang.manifests/0
   :sig: manifests()


   
   Returns Erlang manifests.
   
   

.. elixir:function:: Mix.Tasks.Compile.Erlang.run/1
   :sig: run(args)


   
   Runs this task.
   
   

.. elixir:function:: Mix.Tasks.Compile.Erlang.to_erl_file/1
   :sig: to_erl_file(file)


   
   Converts the given file to a format accepted by the Erlang compilation
   tools.
   
   







