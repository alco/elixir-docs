System
==============================================================

.. elixir:module:: System

   :mtype: 

Overview
--------

The System module provides access to variables used or maintained by the
VM and to functions that interact directly with the VM or the host
system.





Summary
-------

================================ =
:elixir:func:`argv/0`            List command line arguments 

:elixir:func:`argv/1`            Modify command line arguments 

:elixir:func:`at_exit/1`         Register a program exit handler function 

:elixir:func:`build_info/0`      Elixir build information 

:elixir:func:`cmd/1`             Execute a system command 

:elixir:func:`cwd!/0`            Current working directory, exception on error 

:elixir:func:`cwd/0`             Current working directory 

:elixir:func:`delete_env/1`      Deletes an environment variable 

:elixir:func:`find_executable/1` Locate an executable on the system 

:elixir:func:`get_env/0`         System environment variables 

:elixir:func:`get_env/1`         Environment variable value 

:elixir:func:`get_pid/0`         Erlang VM process identifier 

:elixir:func:`halt/1`            Halt the Erlang runtime system 

:elixir:func:`put_env/1`         Set multiple environment variables 

:elixir:func:`put_env/2`         Set an environment variable value 

:elixir:func:`stacktrace/0`      Last exception stacktrace 

:elixir:func:`tmp_dir!/0`        Writable temporary directory, exception on error 

:elixir:func:`tmp_dir/0`         Writable temporary directory 

:elixir:func:`user_home!/0`      User home directory, exception on error 

:elixir:func:`user_home/0`       User home directory 

:elixir:func:`version/0`         Elixir version information 
================================ =





Functions
---------

.. elixir:function:: System.argv/0
   :sig: argv()


   Specs:
   
 
   * argv :: [:elixir:type:`String.t/0`]
 

   
   List command line arguments.
   
   Returns the list of command line arguments passed to the program.
   
   

.. elixir:function:: System.argv/1
   :sig: argv(args)


   Specs:
   
 
   * argv([:elixir:type:`String.t/0`]) :: :ok
 

   
   Modify command line arguments.
   
   Changes the list of command line arguments. Use it with caution, as it
   destroys any previous argv information.
   
   

.. elixir:function:: System.at_exit/1
   :sig: at_exit(fun)


   
   Register a program exit handler function.
   
   Registers a function that will be invoked at the end of program
   execution. Useful for invoking a hook in "script" mode.
   
   The function must receive the exit status code as an argument.
   
   

.. elixir:function:: System.build_info/0
   :sig: build_info()


   Specs:
   
 
   * build_info :: :elixir:type:`Keyword.t/0`
 

   
   Elixir build information.
   
   Returns a keyword list with Elixir version, git tag info and compilation
   date.
   
   

.. elixir:function:: System.cmd/1
   :sig: cmd(command)


   Specs:
   
 
   * cmd(char_list) :: char_list
 
   * cmd(:elixir:type:`String.t/0`) :: :elixir:type:`String.t/0`
 

   
   Execute a system command.
   
   Executes ``command`` in a command shell of the target OS, captures the
   standard output of the command and returns the result as a binary.
   
   If ``command`` is a char list, a char list is returned. Otherwise a
   string, correctly encoded in UTF-8, is expected.
   
   

.. elixir:function:: System.cwd/0
   :sig: cwd()


   
   Current working directory.
   
   Returns the current working directory or ``nil`` if one is not
   available.
   
   

.. elixir:function:: System.cwd!/0
   :sig: cwd!()


   
   Current working directory, exception on error.
   
   Returns the current working directory or raises
   ```RuntimeError`` <RuntimeError.html>`__.
   
   

.. elixir:function:: System.delete_env/1
   :sig: delete_env(varname)


   Specs:
   
 
   * delete_env(:elixir:type:`String.t/0`) :: :ok
 

   
   Deletes an environment variable.
   
   Removes the variable ``varname`` from the environment.
   
   

.. elixir:function:: System.find_executable/1
   :sig: find_executable(program)


   Specs:
   
 
   * find_executable(char_list) :: char_list | nil
 
   * find_executable(binary) :: binary | nil
 

   
   Locate an executable on the system.
   
   This function looks up an executable program given its name using the
   environment variable PATH on Unix and Windows. It also considers the
   proper executable extension for each OS, so for Windows it will try to
   lookup files with ``.com``, ``.cmd`` or similar extensions.
   
   If ``program`` is a char list, a char list is returned. Returns a binary
   otherwise.
   
   

.. elixir:function:: System.get_env/0
   :sig: get_env()


   Specs:
   
 
   * get_env :: %{:elixir:type:`String.t/0` => :elixir:type:`String.t/0`}
 

   
   System environment variables.
   
   Returns a list of all environment variables. Each variable is given as a
   ``{name, value}`` tuple where both ``name`` and ``value`` are strings.
   
   

.. elixir:function:: System.get_env/1
   :sig: get_env(varname)


   Specs:
   
 
   * get_env(binary) :: binary | nil
 

   
   Environment variable value.
   
   Returns the value of the environment variable ``varname`` as a binary,
   or ``nil`` if the environment variable is undefined.
   
   

.. elixir:function:: System.get_pid/0
   :sig: get_pid()


   Specs:
   
 
   * get_pid :: binary
 

   
   Erlang VM process identifier.
   
   Returns the process identifier of the current Erlang emulator in the
   format most commonly used by the operating system environment.
   
   See http://www.erlang.org/doc/man/os.html#getpid-0 for more info.
   
   

.. elixir:function:: System.halt/1
   :sig: halt(status \\ 0)


   Specs:
   
 
   * halt(non_neg_integer | binary | :abort) :: no_return
 

   
   Halt the Erlang runtime system.
   
   Halts the Erlang runtime system where the argument ``status`` must be a
   non-negative integer, the atom ``:abort`` or a binary.
   
   -  If an integer, the runtime system exits with the integer value which
      is returned to the operating system;
   
   -  If ``:abort``, the runtime system aborts producing a core dump, if
      that is enabled in the operating system;
   
   -  If a string, an erlang crash dump is produced with status as slogan,
      and then the runtime system exits with status code 1;
   
   Note that on many platforms, only the status codes 0-255 are supported
   by the operating system.
   
   For more information, check:
   http://www.erlang.org/doc/man/erlang.html#halt-1
   
   **Examples**
   
   ::
   
       System.halt(0)
       System.halt(1)
       System.halt(:abort)
   
   
   

.. elixir:function:: System.put_env/1
   :sig: put_env(dict)


   Specs:
   
 
   * put_env(:elixir:type:`Dict.t/0`) :: :ok
 

   
   Set multiple environment variables.
   
   Sets a new value for each environment variable corresponding to each key
   in ``dict``.
   
   

.. elixir:function:: System.put_env/2
   :sig: put_env(varname, value)


   Specs:
   
 
   * put_env(binary, binary) :: :ok
 

   
   Set an environment variable value.
   
   Sets a new ``value`` for the environment variable ``varname``.
   
   

.. elixir:function:: System.stacktrace/0
   :sig: stacktrace()


   
   Last exception stacktrace.
   
   Note that the Erlang VM (and therefore this function) does not return
   the current stacktrace but rather the stacktrace of the latest
   exception.
   
   Inlined by the compiler into
   ```:erlang.get_stacktrace/0`` <http://www.erlang.org/doc/man/erlang.html#get_stacktrace-0>`__.
   
   

.. elixir:function:: System.tmp_dir/0
   :sig: tmp_dir()


   
   Writable temporary directory.
   
   Returns a writable temporary directory. Searches for directories in the
   following order:
   
   1. The directory named by the TMPDIR environment variable
   2. The directory named by the TEMP environment variable
   3. The directory named by the TMP environment variable
   4. ``C:\TMP`` on Windows or ``/tmp`` on Unix
   5. As a last resort, the current working directory
   
   Returns ``nil`` if none of the above are writable.
   
   

.. elixir:function:: System.tmp_dir!/0
   :sig: tmp_dir!()


   
   Writable temporary directory, exception on error.
   
   Same as ```tmp_dir/0`` <#tmp_dir/0>`__ but raises
   ```RuntimeError`` <RuntimeError.html>`__ instead of returning ``nil`` if
   no temp dir is set.
   
   

.. elixir:function:: System.user_home/0
   :sig: user_home()


   
   User home directory.
   
   Returns the user home directory (platform independent). Returns ``nil``
   if no user home is set.
   
   

.. elixir:function:: System.user_home!/0
   :sig: user_home!()


   
   User home directory, exception on error.
   
   Same as ```user_home/0`` <#user_home/0>`__ but raises
   ```RuntimeError`` <RuntimeError.html>`__ instead of returning ``nil`` if
   no user home is set.
   
   

.. elixir:function:: System.version/0
   :sig: version()


   Specs:
   
 
   * version :: :elixir:type:`String.t/0`
 

   
   Elixir version information.
   
   Returns Elixir's version as binary.
   
   







