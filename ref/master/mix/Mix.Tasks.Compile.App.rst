Mix.Tasks.Compile.App
==============================================================

.. elixir:module:: Mix.Tasks.Compile.App

   :mtype: 

Overview
--------

Writes an .app file.

An ``.app`` file is a file containing Erlang terms that defines your
application. Mix automatically generates this file based on your
``mix.exs`` configuration. You can learn more about OTP applications by
seeing the documentation for the ``Application`` module.

In order to generate the ``.app`` file, Mix expects your application to
have both ``:app`` and ``:version`` keys. Furthermore, you can configure
the generated application by defining an ``application`` function in
your ``mix.exs`` with the following options:

-  ``:applications`` - all applications your application depends on at
   runtime. For example, if your application depends on Erlang's
   ``:crypto``, it needs to be added to this list. Most of your
   dependencies must be added as well (unless they're a development or
   test dependency). Mix and other tools use this list in order to
   properly boot your application dependencies before starting the
   application itself;

-  ``:registered`` - the name of all registered processes in the
   application. If your application defines a local GenServer with name
   ``MyServer``, it is recommended to add ``MyServer`` to this list. It
   is mostly useful to detect conflicts in between applications that
   register the same names;

-  ``:mod`` - specify a module to invoke when the application is
   started, it must be in the format ``{Mod, args}`` where args is often
   an empty list. The module specified here must implement the callbacks
   defined by the ``Application`` module;

-  ``:env`` - default values for the application environment. The
   application environment is one of the most common ways to configure
   applications;

Let's see an example ``application`` function:

::

    def application do
      [mod: {MyApp, []},
       env: [default: :value],
       applications: [:crypto]]
    end

Besides the options above, ``.app`` files also expects other options
like ``:modules`` and ``:vsn``, but those are automatically filled by
Mix.

Command line options
~~~~~~~~~~~~~~~~~~~~

-  ``--force`` - forces compilation regardless of modification times






Summary
-------

==================== =
:elixir:func:`run/1` Callback implementation of ```Mix.Task.run/1`` <Mix.Task.html#run/1>`__ 
==================== =





Functions
---------

.. elixir:function:: Mix.Tasks.Compile.App.run/1
   :sig: run(args)


   
   Callback implementation of ```Mix.Task.run/1`` <Mix.Task.html#run/1>`__.
   
   







