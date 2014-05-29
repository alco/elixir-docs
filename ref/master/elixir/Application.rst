Application
==============================================================

.. elixir:module:: Application

   :mtype: 

Overview
--------

A module for working with applications and defining application
callbacks.

In Elixir (actually, in Erlang/OTP), an application is a component
implementing some specific functionality, that can be started and
stopped as a unit, and which can be re-used in other systems as well.

Applications are defined with an application file named ``APP.app``
where ``APP`` is the APP name, usually in ``underscore_case``
convention. The application file must reside in the same ``ebin``
directory as the application's modules bytecode.

In Elixir, Mix is responsible for compiling your source code and
generating your application ``.app`` file. Furthermore, Mix is also
responsible for configuring, starting and stoping your application and
its dependencies. For this reason, this documentation will focus on the
remaining aspects of your application: the application environment, and
the application callback module.

You can learn more about Mix compilation of ``.app`` files by typing
``mix help compile.app``.

Application environment
~~~~~~~~~~~~~~~~~~~~~~~

Once an application is started, OTP provides an application environment
that can be used to configure applications.

Assuming you are inside a Mix project, you can edit your application
function in the ``mix.exs`` file to the following:

::

    def application do
      [env: [hello: :world]]
    end

In the application function, we can define the default environment
values for our application. By starting your application with
``iex -S mix``, you can access the default value:

::

    Application.get_env(:APP_NAME, :hello)
    #=> {:ok, :hello}

It is also possible to put and delete values from the application value,
including new values that are not defined in the environment file
(although those should be avoided).

In the future, we plan to support configuration files which allows
developers to configure the environment of their dependencies.

Keep in mind that each application is responsible for its environment.
Do not use the fucntions in this module for directly access or modify
the environment of other application (as it may lead to inconsistent
data in the application environment).

Application module callback
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Often times, an application defines a supervision tree that must be
started and stopped when the application starts and stops. For such, we
need to define an application module callback. The first step is to
define the module callback in the application definition in the
``mix.exs`` file:

::

    def application do
      [mod: {MyApp, []}]
    end

Our application now requires the ``MyApp`` module to provide an
application callback. This can be done by invoking ``use Application``
in that module and defining a :elixir:func:`start/2` callback, for example:

::

    defmodule MyApp do
      use Application

      def start(_type, _args) do
        MyApp.Supervisor.start_link()
      end
    end

:elixir:func:`start/2` most commonly returns ``{:ok, pid}`` or
``{:ok, pid, state}`` where ``pid`` identifies the supervision tree and
the state is the application state. ``args`` is second element of the
tuple given to the ``:mod`` option.

The ``type`` passed into :elixir:func:`start/2` is usually ``:normal`` unless in a
distributed setup where applications takeover and failovers are
configured. This particular aspect of applications can be read with more
detail in the OTP documentation:

-  http://www.erlang.org/doc/man/application.html
-  http://www.erlang.org/doc/design\_principles/applications.html

A developer may also implement the :elixir:func:`stop/1` callback (automatically
defined by ``use Application``) which does any application cleanup. It
receives the application state and can return any value. Notice that
shutting down the supervisor is automatically handled by the VM;





Summary
-------

=================================== =
:elixir:func:`app_dir/1`            Gets the directory for app 

:elixir:func:`app_dir/2`            Returns the given path inside :elixir:func:`app_dir/1` 

:elixir:func:`delete_env/3`         Deletes the ``key`` from the given ``app`` environment 

:elixir:func:`ensure_all_started/2` Ensures the given ``app`` and its applications are started 

:elixir:func:`ensure_started/2`     Ensures the given ``app`` is started 

:elixir:func:`fetch_env/2`          Returns the value for ``key`` in ``app``'s environment in a tuple 

:elixir:func:`format_error/1`       Formats the error reason returned by :elixir:func:`start/2`, ``ensure_started/2,``\ stop/1\ ``,``\ load/1\ ``and``\ unload/1\`, returns a string 

:elixir:func:`get_all_env/1`        Returns all key-value pairs for ``app`` 

:elixir:func:`get_env/3`            Returns the value for ``key`` in ``app``'s environment 

:elixir:func:`load/1`               Loads the given ``app`` 

:elixir:func:`put_env/4`            Puts the ``value`` in ``key`` for the given ``app`` 

:elixir:func:`start/2`              Starts the given ``app`` 

:elixir:func:`stop/1`               Stops the given ``app`` 

:elixir:func:`unload/1`             Unloads the given ``app`` 
=================================== =



Types
-----

.. elixir:type:: Application.app/0

   :elixir:type:`app/0` :: atom
   

.. elixir:type:: Application.key/0

   :elixir:type:`key/0` :: atom
   

.. elixir:type:: Application.value/0

   :elixir:type:`value/0` :: term
   

.. elixir:type:: Application.start_type/0

   :elixir:type:`start_type/0` :: :permanent | :transient | :temporary
   





Functions
---------

.. elixir:function:: Application.app_dir/1
   :sig: app_dir(app)


   Specs:
   
 
   * app_dir(:elixir:type:`app/0`) :: :elixir:type:`String.t/0`
 

   
   Gets the directory for app.
   
   This information is returned based on the code path. Here is an example:
   
   ::
   
       File.mkdir_p!("foo/ebin")
       Code.prepend_path("foo/ebin")
       Application.app_dir(:foo)
       #=> "foo"
   
   Even though the directory is empty and there is no ``.app`` file it is
   considered the application directory based on the name "foo/ebin". The
   name may contain a dash ``-`` which is considered to be the app version
   and it is removed for the lookup purposes:
   
   ::
   
       File.mkdir_p!("bar-123/ebin")
       Code.prepend_path("bar-123/ebin")
       Application.app_dir(:bar)
       #=> "bar-123"
   
   For more information on code paths, check the :elixir:mod:`Code` module in Elixir
   and also Erlang's ``:code`` module.
   
   

.. elixir:function:: Application.app_dir/2
   :sig: app_dir(app, path)


   Specs:
   
 
   * app_dir(:elixir:type:`app/0`, :elixir:type:`String.t/0`) :: :elixir:type:`String.t/0`
 

   
   Returns the given path inside :elixir:func:`app_dir/1`.
   
   

.. elixir:function:: Application.delete_env/3
   :sig: delete_env(app, key, opts \\ [])


   Specs:
   
 
   * delete_env(:elixir:type:`app/0`, :elixir:type:`key/0`, timeout: timeout, persistent: boolean) :: :ok
 

   
   Deletes the ``key`` from the given ``app`` environment.
   
   See :elixir:func:`put_env/4` for a description of the options.
   
   

.. elixir:function:: Application.ensure_all_started/2
   :sig: ensure_all_started(app, type \\ :temporary)


   Specs:
   
 
   * ensure_all_started(:elixir:type:`app/0`, :elixir:type:`start_type/0`) :: {:ok, [:elixir:type:`app/0`]} | {:error, term}
 

   
   Ensures the given ``app`` and its applications are started.
   
   Same as :elixir:func:`start/2` but also starts the applications listed under
   ``:applications`` in the ``.app`` file in case they were not previously
   started.
   
   

.. elixir:function:: Application.ensure_started/2
   :sig: ensure_started(app, type \\ :temporary)


   Specs:
   
 
   * ensure_started(:elixir:type:`app/0`, :elixir:type:`start_type/0`) :: :ok | {:error, term}
 

   
   Ensures the given ``app`` is started.
   
   Same as :elixir:func:`start/2` but returns ``:ok`` if the application was already
   started. This is useful in scripts and in test setup, where test
   applications need to be explicitly started:
   
   ::
   
       :ok = Application.ensure_started(:my_test_dep)
   
   
   

.. elixir:function:: Application.fetch_env/2
   :sig: fetch_env(app, key)


   Specs:
   
 
   * fetch_env(:elixir:type:`app/0`, :elixir:type:`key/0`) :: {:ok, :elixir:type:`value/0`} | :error
 

   
   Returns the value for ``key`` in ``app``'s environment in a tuple.
   
   If the specified application is not loaded, or the configuration
   parameter does not exist, the function returns ``:error``.
   
   

.. elixir:function:: Application.format_error/1
   :sig: format_error(reason)


   Specs:
   
 
   * format_error(any) :: :elixir:type:`String.t/0`
 

   
   Formats the error reason returned by :elixir:func:`start/2`,
   ``ensure_started/2,``\ stop/1\ ``,``\ load/1\ ``and``\ unload/1\`,
   returns a string.
   
   

.. elixir:function:: Application.get_all_env/1
   :sig: get_all_env(app)


   Specs:
   
 
   * get_all_env(:elixir:type:`app/0`) :: [{:elixir:type:`key/0`, :elixir:type:`value/0`}]
 

   
   Returns all key-value pairs for ``app``.
   
   

.. elixir:function:: Application.get_env/3
   :sig: get_env(app, key, default \\ nil)


   Specs:
   
 
   * get_env(:elixir:type:`app/0`, :elixir:type:`key/0`, :elixir:type:`value/0`) :: :elixir:type:`value/0`
 

   
   Returns the value for ``key`` in ``app``'s environment.
   
   If the specified application is not loaded, or the configuration
   parameter does not exist, the function returns the ``default`` value.
   
   

.. elixir:function:: Application.load/1
   :sig: load(app)


   Specs:
   
 
   * load(:elixir:type:`app/0`) :: :ok | {:error, term}
 

   
   Loads the given ``app``.
   
   In order to be loaded, an ``.app`` file must be in the load paths. All
   ``:included_applications`` will also be loaded.
   
   Loading the application does not start it nor load its modules, but it
   does load its environment.
   
   

.. elixir:function:: Application.put_env/4
   :sig: put_env(app, key, value, opts \\ [])


   Specs:
   
 
   * put_env(:elixir:type:`app/0`, :elixir:type:`key/0`, :elixir:type:`value/0`, timeout: timeout, persistent: boolean) :: :ok
 

   
   Puts the ``value`` in ``key`` for the given ``app``.
   
   **Options**
   
   -  ``:timeout`` - the timeout for the change (defaults to 5000ms);
   
   -  ``:persistent`` - persists the given value on application load and
      reloads;
   
   If :elixir:func:`put_env/4` is called before the application is loaded, the
   application environment values specified in the ``.app`` file will
   override the ones previously set.
   
   The persistent option can be set to true when there is a need to
   guarantee parameters set with this function will not be overridden by
   the ones defined in the application resource file on load. This means
   persistent values will stick after the application is loaded and also on
   application reload.
   
   

.. elixir:function:: Application.start/2
   :sig: start(app, type \\ :temporary)


   Specs:
   
 
   * start(:elixir:type:`app/0`, :elixir:type:`start_type/0`) :: :ok | {:error, term}
 

   
   Starts the given ``app``.
   
   If the ``app`` is not loaded, the application will first be loaded using
   :elixir:func:`load/1`. Any included application, defined in the
   ``:included_applications`` key of the ``.app`` file will also be loaded,
   but they won't be started.
   
   Furthermore, all applications listed in the ``:applications`` key must
   be explicitly started before this application is. If not,
   ``{:error, {:not_started, app}}`` is returned, where ``app`` is the name
   of the missing application.
   
   In case you want to automatically load **and start** all of ``app``'s
   dependencies, see :elixir:func:`ensure_all_started/2`.
   
   The ``type`` argument specifies the type of the application:
   
   -  ``:permanent`` - if ``app`` terminates, all other applications and
      the entire node are also terminated;
   -  ``:transient`` - if ``app`` terminates with ``:normal`` reason, it is
      reported but no other applications are terminated. If a transient
      application terminates abnormally, all other applications and the
      entire node are also terminated;
   -  ``:temporary`` - if ``app`` termiantes, it is reported but no other
      applications are terminated (the default);
   
   Note that it is always possible to stop an application explicitly by
   calling :elixir:func:`stop/1`. Regardless of the type of the application, no other
   applications will be affected.
   
   Note also that the ``:transient`` type is of little practical use, since
   when a supervision tree terminates, the reason is set to ``:shutdown``,
   not ``:normal``.
   
   

.. elixir:function:: Application.stop/1
   :sig: stop(app)


   Specs:
   
 
   * stop(:elixir:type:`app/0`) :: :ok | {:error, term}
 

   
   Stops the given ``app``.
   
   When stopped, the application is still loaded.
   
   

.. elixir:function:: Application.unload/1
   :sig: unload(app)


   Specs:
   
 
   * unload(:elixir:type:`app/0`) :: :ok | {:error, term}
 

   
   Unloads the given ``app``.
   
   It will also unload all ``:included_applications``. Note that the
   function does not purge the application modules.
   
   







