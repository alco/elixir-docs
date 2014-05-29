Mix.Project
==============================================================

.. elixir:module:: Mix.Project

   :mtype: 

Overview
--------

Defines and manipulate Mix projects.

In order to configure Mix, a developer needs to use :elixir:mod:`Mix.Project` in a
module and define a function named ``project`` that returns a keyword
list with configuration.

::

    defmodule MyApp do
      use Mix.Project

      def project do
        [app: :my_app,
         vsn: "0.6.0"]
      end
    end

After being defined, the configuration for this project can be read as
:elixir:func:`Mix.Project.config/0`. Notice that :elixir:func:`config/0` won't fail if a
project is not defined; this allows many mix tasks to work even without
a project.

In case the developer needs a project or wants to access a special
function in the project, he/she can call :elixir:func:`Mix.Project.get!/0` which
fails with :elixir:mod:`Mix.NoProjectError` in case a project is not defined.





Summary
-------

================================ =
:elixir:func:`app_path/1`        Returns the application path inside the build 

:elixir:func:`build_path/1`      Returns the build path for this project 

:elixir:func:`build_structure/2` Builds the project structure for the current application 

:elixir:func:`compile_path/1`    Returns the paths this project compiles to 

:elixir:func:`config/0`          Returns the project configuration 

:elixir:func:`config_files/0`    Returns a list of project configuration files for this project 

:elixir:func:`deps_path/1`       Returns the path to store dependencies for this project 

:elixir:func:`get!/0`            Same as :elixir:func:`get/0`, but raises an exception if there is no current project 

:elixir:func:`get/0`             Retrieves the current project if there is one 

:elixir:func:`in_project/4`      Runs the given ``fun`` inside the given project 

:elixir:func:`load_paths/0`      Returns all load paths for this project 

:elixir:func:`manifest_path/1`   The path to store manifests 

:elixir:func:`umbrella?/0`       Returns ``true`` if project is an umbrella project 
================================ =





Functions
---------

.. elixir:function:: Mix.Project.app_path/1
   :sig: app_path(config \\ config())


   
   Returns the application path inside the build.
   
   The returned path will be expanded.
   
   **Examples**
   
   ::
   
       Mix.Project.app_path
       #=> "/path/to/project/_build/shared/lib/app"
   
   
   

.. elixir:function:: Mix.Project.build_path/1
   :sig: build_path(config \\ config())


   
   Returns the build path for this project.
   
   The returned path will be expanded.
   
   **Examples**
   
   ::
   
       Mix.Project.build_path
       #=> "/path/to/project/_build/shared"
   
   If :build\_per\_environment is set to true (the default), it will create
   a new build per environment:
   
   ::
   
       Mix.env
       #=> :dev
       Mix.Project.build_path
       #=> "/path/to/project/_build/dev"
   
   
   

.. elixir:function:: Mix.Project.build_structure/2
   :sig: build_structure(config \\ config(), opts \\ [])


   
   Builds the project structure for the current application.
   
   **Options**
   
   -  ``:symlink_ebin`` - Symlink ebin instead of copying it
   
   
   

.. elixir:function:: Mix.Project.compile_path/1
   :sig: compile_path(config \\ config())


   
   Returns the paths this project compiles to.
   
   The returned path will be expanded.
   
   **Examples**
   
   ::
   
       Mix.Project.compile_path
       #=> "/path/to/project/_build/shared/lib/app/priv"
   
   
   

.. elixir:function:: Mix.Project.config/0
   :sig: config()


   
   Returns the project configuration.
   
   If there is no project defined, it still returns a keyword list with
   default values. This allows many mix tasks to work without the need for
   an underlying project.
   
   Note this configuration is cached once the project is pushed into the
   stack. Calling it multiple times won't cause it to be recomputed.
   
   Do not use ``Mix.Project.config`` to rely on runtime configuration. Use
   it only to configure aspects of your project (like compilation
   directories) and not your application runtime.
   
   

.. elixir:function:: Mix.Project.config_files/0
   :sig: config_files()


   
   Returns a list of project configuration files for this project.
   
   This function is usually used in compilation tasks to trigger a full
   recompilation whenever such configuration files change.
   
   By default it includes the mix.exs file, the lock manifest and all
   config files in the ``config`` directory.
   
   

.. elixir:function:: Mix.Project.deps_path/1
   :sig: deps_path(config \\ config())


   
   Returns the path to store dependencies for this project.
   
   The returned path will be expanded.
   
   **Examples**
   
   ::
   
       Mix.Project.deps_path
       #=> "/path/to/project/deps"
   
   
   

.. elixir:function:: Mix.Project.get/0
   :sig: get()


   
   Retrieves the current project if there is one.
   
   Otherwise ``nil`` is returned. It may happen in cases there is no
   mixfile in the current directory.
   
   If you expect a project to be defined, i.e. it is a requirement of the
   current task, you should call :elixir:func:`get!/0` instead.
   
   

.. elixir:function:: Mix.Project.get!/0
   :sig: get!()


   
   Same as :elixir:func:`get/0`, but raises an exception if there is no current
   project.
   
   This is usually called by tasks that need additional functions on the
   project to be defined. Since such tasks usually depend on a project
   being defined, this function raises :elixir:mod:`Mix.NoProjectError` in case no
   project is available.
   
   

.. elixir:function:: Mix.Project.in_project/4
   :sig: in_project(app, path, post_config \\ [], fun)


   
   Runs the given ``fun`` inside the given project.
   
   This function changes the current working directory and loads the
   project at the given directory onto the project stack.
   
   A ``post_config`` can be passed that will be merged into the project
   configuration.
   
   

.. elixir:function:: Mix.Project.load_paths/0
   :sig: load_paths()


   
   Returns all load paths for this project.
   
   

.. elixir:function:: Mix.Project.manifest_path/1
   :sig: manifest_path(config \\ config())


   
   The path to store manifests.
   
   By default they are stored in the app path inside the build directory
   but it may be changed in future releases.
   
   The returned path will be expanded.
   
   **Examples**
   
   ::
   
       Mix.Project.manifest_path
       #=> "/path/to/project/_build/shared/lib/app"
   
   
   

.. elixir:function:: Mix.Project.umbrella?/0
   :sig: umbrella?()


   
   Returns ``true`` if project is an umbrella project.
   
   







