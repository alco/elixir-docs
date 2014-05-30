Code
==============================================================

.. elixir:module:: Code

   :mtype: 

Overview
--------

Utilities for managing code compilation, code evaluation and code
loading.

This module complements `Erlang's code
module <http://www.erlang.org/doc/man/code.html>`__ to add behaviour
which is specific to Elixir.





Summary
-------

=================================== =
:elixir:func:`append_path/1`        Append a path to the Erlang VM code path 

:elixir:func:`compile_quoted/2`     Compiles the quoted expression 

:elixir:func:`compile_string/2`     Compiles the given string 

:elixir:func:`compiler_options/0`   Gets the compilation options from the code server 

:elixir:func:`compiler_options/1`   Sets compilation options 

:elixir:func:`delete_path/1`        Delete a path from the Erlang VM code path 

:elixir:func:`ensure_compiled/1`    Ensures the given module is compiled and loaded 

:elixir:func:`ensure_compiled?/1`   Ensures the given module is compiled and loaded 

:elixir:func:`ensure_loaded/1`      Ensures the given module is loaded 

:elixir:func:`ensure_loaded?/1`     Ensures the given module is loaded 

:elixir:func:`eval_file/2`          Evals the given file 

:elixir:func:`eval_quoted/3`        Evaluate the quoted contents 

:elixir:func:`eval_string/3`        Evaluate the contents given by ``string`` 

:elixir:func:`get_docs/2`           Returns the docs for the given module 

:elixir:func:`load_file/2`          Load the given file 

:elixir:func:`loaded_files/0`       List all loaded files 

:elixir:func:`prepend_path/1`       Prepend a path to the Erlang VM code path 

:elixir:func:`require_file/2`       Requires the given ``file`` 

:elixir:func:`string_to_quoted\!/2` Convert the given string to its quoted form 

:elixir:func:`string_to_quoted/2`   Convert the given string to its quoted form 

:elixir:func:`unload_files/1`       Remove files from the loaded files list 
=================================== =





Functions
---------

.. elixir:function:: Code.append_path/1
   :sig: append_path(path)


   
   Append a path to the Erlang VM code path.
   
   The path is expanded with :elixir:func:`Path.expand/1` before being appended.
   
   

.. elixir:function:: Code.compile_quoted/2
   :sig: compile_quoted(quoted, file \\ "nofile")


   
   Compiles the quoted expression.
   
   Returns a list of tuples where the first element is the module name and
   the second one is its byte code (as a binary).
   
   

.. elixir:function:: Code.compile_string/2
   :sig: compile_string(string, file \\ "nofile")


   
   Compiles the given string.
   
   Returns a list of tuples where the first element is the module name and
   the second one is its byte code (as a binary).
   
   For compiling many files at once, check
   :elixir:func:`Kernel.ParallelCompiler.files/2`.
   
   

.. elixir:function:: Code.compiler_options/0
   :sig: compiler_options()


   
   Gets the compilation options from the code server.
   
   Check :elixir:func:`compiler_options/1` for more information.
   
   

.. elixir:function:: Code.compiler_options/1
   :sig: compiler_options(opts)


   
   Sets compilation options.
   
   These options are global since they are stored by Elixir's Code Server.
   
   Available options are:
   
   -  ``:docs`` - when ``true``, retain documentation in the compiled
      module, ``true`` by default;
   
   -  ``:debug_info`` - when ``true``, retain debug information in the
      compiled module. This allows a developer to reconstruct the original
      source code, ``false`` by default;
   
   -  ``:ignore_module_conflict`` - when ``true``, override modules that
      were already defined without raising errors, ``false`` by default;
   
   -  ``:warnings_as_errors`` - cause compilation to fail when warnings are
      generated;
   
   
   
   

.. elixir:function:: Code.delete_path/1
   :sig: delete_path(path)


   
   Delete a path from the Erlang VM code path.
   
   The path is expanded with :elixir:func:`Path.expand/1` before being deleted.
   
   

.. elixir:function:: Code.ensure_compiled/1
   :sig: ensure_compiled(module)


   
   Ensures the given module is compiled and loaded.
   
   If the module is already loaded, it works as no-op. If the module was
   not loaded yet, it checks if it needs to be compiled first and then
   tries to load it.
   
   If it succeeds loading the module, it returns ``{:module, module}``. If
   not, returns ``{:error, reason}`` with the error reason.
   
   Check :elixir:func:`ensure_loaded/1` for more information on module loading and
   when to use :elixir:func:`ensure_loaded/1` or :elixir:func:`ensure_compiled/1`.
   
   

.. elixir:function:: Code.ensure_compiled?/1
   :sig: ensure_compiled?(module)


   
   Ensures the given module is compiled and loaded.
   
   Similar to :elixir:func:`ensure_compiled/1`, but returns ``true`` if the module is
   already loaded or was successfully loaded and compiled. Returns
   ``false`` otherwise.
   
   

.. elixir:function:: Code.ensure_loaded/1
   :sig: ensure_loaded(module)


   
   Ensures the given module is loaded.
   
   If the module is already loaded, this works as no-op. If the module was
   not yet loaded, it tries to load it.
   
   If it succeeds loading the module, it returns ``{:module, module}``. If
   not, returns ``{:error, reason}`` with the error reason.
   
   **Code loading on the Erlang VM**
   
   Erlang has two modes to load code: interactive and embedded.
   
   By default, the Erlang VM runs in interactive mode, where modules are
   loaded as needed. In embedded mode the opposite happens, as all modules
   need to be loaded upfront or explicitly.
   
   Therefore, this function is used to check if a module is loaded before
   using it and allows one to react accordingly. For example, the :elixir:mod:`URI`
   module uses this function to check if a specific parser exists for a
   given URI scheme.
   
   **:elixir:func:`Code.ensure_compiled/1`**
   
   Elixir also contains an :elixir:func:`ensure_compiled/1` function that is a
   superset of :elixir:func:`ensure_loaded/1`.
   
   Since Elixir's compilation happens in parallel, in some situations you
   may need to use a module that was not yet compiled, therefore it can't
   even be loaded.
   
   :elixir:func:`ensure_compiled/1` halts the current process until the module we are
   depending on is available.
   
   In most cases, :elixir:func:`ensure_loaded/1` is enough. :elixir:func:`ensure_compiled/1` must
   be used in rare cases, usually involving macros that need to invoke a
   module for callback information.
   
   

.. elixir:function:: Code.ensure_loaded?/1
   :sig: ensure_loaded?(module)


   
   Ensures the given module is loaded.
   
   Similar to :elixir:func:`ensure_loaded/1`, but returns ``true`` if the module is
   already loaded or was successfully loaded. Returns ``false`` otherwise.
   
   

.. elixir:function:: Code.eval_file/2
   :sig: eval_file(file, relative_to \\ nil)


   
   Evals the given file.
   
   Accepts ``relative_to`` as an argument to tell where the file is
   located.
   
   While ``load_file`` loads a file and returns the loaded modules and
   their byte code, ``eval_file`` simply evalutes the file contents and
   returns the evaluation result and its bindings.
   
   

.. elixir:function:: Code.eval_quoted/3
   :sig: eval_quoted(quoted, binding \\ [], opts \\ [])


   
   Evaluate the quoted contents.
   
   See :elixir:func:`eval_string/3` for a description of arguments and return values.
   
   **Examples**
   
   ::
   
       iex> contents = quote(do: var!(a) + var!(b))
       iex> Code.eval_quoted(contents, [a: 1, b: 2], file: __ENV__.file, line: __ENV__.line)
       {3, [a: 1, b: 2]}
   
   For convenience, you can pass ``__ENV__`` as the ``opts`` argument and
   all options will be automatically extracted from the current
   environment:
   
   ::
   
       iex> contents = quote(do: var!(a) + var!(b))
       iex> Code.eval_quoted(contents, [a: 1, b: 2], __ENV__)
       {3, [a: 1, b: 2]}
   
   
   

.. elixir:function:: Code.eval_string/3
   :sig: eval_string(string, binding \\ [], opts \\ [])


   
   Evaluate the contents given by ``string``.
   
   The ``binding`` argument is a keyword list of variable bindings. The
   ``opts`` argument is a keyword list of environment options.
   
   Those options can be:
   
   -  ``:file`` - the file to be considered in the evaluation
   -  ``:line`` - the line on which the script starts
   -  ``:delegate_locals_to`` - delegate local calls to the given module,
      the default is to not delegate
   
   Additionally, the following scope values can be configured:
   
   -  ``:aliases`` - a list of tuples with the alias and its target
   -  ``:requires`` - a list of modules required
   -  ``:functions`` - a list of tuples where the first element is a module
      and the second a list of imported function names and arity. The list
      of function names and arity must be sorted
   -  ``:macros`` - a list of tuples where the first element is a module
      and the second a list of imported macro names and arity. The list of
      function names and arity must be sorted
   
   Notice that setting any of the values above overrides Elixir's default
   values. For example, setting ``:requires`` to ``[]``, will no longer
   automatically require the :elixir:mod:`Kernel` module; in the same way setting
   ``:macros`` will no longer auto-import :elixir:mod:`Kernel` macros like ``if``,
   ``case``, etc.
   
   Returns a tuple of the form ``{value, binding}``, where ``value`` is the
   value returned from evaluating ``string``. If an error occurs while
   evaluating ``string`` an exception will be raised.
   
   ``binding`` is a keyword list with the value of all variable bindings
   after evaluating ``string``. The binding key is usually an atom, but it
   may be a tuple for variables defined in a different context.
   
   **Examples**
   
   ::
   
       iex> Code.eval_string("a + b", [a: 1, b: 2], file: __ENV__.file, line: __ENV__.line)
       {3, [a: 1, b: 2]}
   
       iex> Code.eval_string("c = a + b", [a: 1, b: 2], __ENV__)
       {3, [a: 1, b: 2, c: 3]}
   
       iex> Code.eval_string("a = a + b", [a: 1, b: 2])
       {3, [a: 3, b: 2]}
   
   For convenience, you can pass ``__ENV__`` as the ``opts`` argument and
   all imports, requires and aliases defined in the current environment
   will be automatically carried over:
   
   ::
   
       iex> Code.eval_string("a + b", [a: 1, b: 2], __ENV__)
       {3, [a: 1, b: 2]}
   
   
   

.. elixir:function:: Code.get_docs/2
   :sig: get_docs(module, kind)


   
   Returns the docs for the given module.
   
   When given a module name, it finds its BEAM code and reads the docs from
   it.
   
   When given a path to a .beam file, it will load the docs directly from
   that file.
   
   The return value depends on the ``kind`` value:
   
   -  ``:docs`` - list of all docstrings attached to functions and macros
      using the ``@doc`` attribute
   
   -  ``:moduledoc`` - tuple ``{<line>, <doc>}`` where ``line`` is the line
      on which module definition starts and ``doc`` is the string attached
      to the module using the ``@moduledoc`` attribute
   
   -  ``:all`` - a keyword list with both ``:docs`` and ``:moduledoc``
   
   
   
   

.. elixir:function:: Code.load_file/2
   :sig: load_file(file, relative_to \\ nil)


   
   Load the given file.
   
   Accepts ``relative_to`` as an argument to tell where the file is
   located. If the file was already required/loaded, loads it again.
   
   It returns a list of tuples ``{ModuleName, <<byte_code>>}``, one tuple
   for each module defined in the file.
   
   Notice that if ``load_file`` is invoked by different processes
   concurrently, the target file will be loaded concurrently many times.
   Check :elixir:func:`require_file/2` if you don't want a file to be loaded
   concurrently.
   
   

.. elixir:function:: Code.loaded_files/0
   :sig: loaded_files()


   
   List all loaded files.
   
   

.. elixir:function:: Code.prepend_path/1
   :sig: prepend_path(path)


   
   Prepend a path to the Erlang VM code path.
   
   The path is expanded with :elixir:func:`Path.expand/1` before being prepended.
   
   

.. elixir:function:: Code.require_file/2
   :sig: require_file(file, relative_to \\ nil)


   
   Requires the given ``file``.
   
   Accepts ``relative_to`` as an argument to tell where the file is
   located. The return value is the same as that of :elixir:func:`load_file/2`. If the
   file was already required/loaded, doesn't do anything and returns
   ``nil``.
   
   Notice that if ``require_file`` is invoked by different processes
   concurrently, the first process to invoke ``require_file`` acquires a
   lock and the remaining ones will block until the file is available. I.e.
   if ``require_file`` is called N times with a given file, it will be
   loaded only once. The first process to call ``require_file`` will get
   the list of loaded modules, others will get ``nil``.
   
   Check :elixir:func:`load_file/2` if you want a file to be loaded multiple times.
   
   

.. elixir:function:: Code.string_to_quoted/2
   :sig: string_to_quoted(string, opts \\ [])


   
   Convert the given string to its quoted form.
   
   Returns ``{:ok, quoted_form}`` if it succeeds,
   ``{:error, {line, error, token}}`` otherwise.
   
   **Options**
   
   -  ``:file`` - The filename to be used in stacktraces and the file
      reported in the ``__ENV__`` variable.
   
   -  ``:line`` - The line reported in the ``__ENV__`` variable.
   
   -  ``:existing_atoms_only`` - When ``true``, raises an error when
      non-existing atoms are found by the tokenizer.
   
   **Macro.to\_string/2**
   
   The opposite of converting a string to its quoted form is
   :elixir:func:`Macro.to_string/2`, which converts a quoted form to a string/binary
   representation.
   
   

.. elixir:function:: Code.string_to_quoted!/2
   :sig: string_to_quoted!(string, opts \\ [])


   
   Convert the given string to its quoted form.
   
   It returns the ast if it succeeds, raises an exception otherwise. The
   exception is a :elixir:mod:`TokenMissingError` in case a token is missing (usually
   because the expression is incomplete), :elixir:mod:`SyntaxError` otherwise.
   
   Check :elixir:func:`string_to_quoted/2` for options information.
   
   

.. elixir:function:: Code.unload_files/1
   :sig: unload_files(files)


   
   Remove files from the loaded files list.
   
   The modules defined in the file are not removed; calling this function
   only removes them from the list, allowing them to be required again.
   
   







