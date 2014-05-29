Mix.Tasks.Deps
==============================================================

.. elixir:module:: Mix.Tasks.Deps

   :mtype: 

Overview
--------

List all dependencies and their status.

Dependencies must be specified in the ``mix.exs`` file in one of the
following formats:

::

    {app, requirement}
    {app, opts}
    {app, requirement, opts}

Where:

-  app is an atom
-  requirement is a version requirement or a regular expression
-  opts is a keyword list of options

By default, dependencies are fetched using the `Hex package
manager <https://hex.pm/>`__:

::

    {:plug, ">= 0.4.0"}

By specifying such dependencies, Mix will automatically install Hex (if
it wasn't previously installed and download a package suitable to your
project).

Mix also supports git and path dependencies:

::

    {:foobar, git: "https://github.com/elixir-lang/foobar.git", tag: "0.1"}

And also umbrella applications:

::

    {:myapp, in_umbrella: true}

The dependencies versions are expected to follow Semantic Versioning and
the requirements must be specified as defined in the ``Version`` module.

Below we provide a more detailed look into the available options.

Mix options
~~~~~~~~~~~

-  ``:app`` - When set to false, does not read the app file for this
   dependency
-  ``:env`` - The environment to run the dependency on, defaults to
   :prod
-  ``:compile`` - A command to compile the dependency, defaults to a
   mix, rebar or make command
-  ``:optional`` - The dependency is optional and used only to specify
   requirements
-  ``:only`` - The dependency will belongs only to the given
   environments, useful when declaring dev- or test-only dependencies
-  ``:override`` - If set to true the dependency will override any other
   definitions of itself by other dependencies

Git options (``:git``)
~~~~~~~~~~~~~~~~~~~~~~

-  ``:git`` - The git repository URI
-  ``:github`` - A shortcut for specifying git repos from github, uses
   ``git:``
-  ``:ref`` - The reference to checkout (may be a branch, a commit sha
   or a tag)
-  ``:branch`` - The git branch to checkout
-  ``:tag`` - The git tag to checkout
-  ``:submodules`` - When true, initialize submodules for the repo

Path options (``:path``)
~~~~~~~~~~~~~~~~~~~~~~~~

-  ``:path`` - The path for the dependency
-  ``:in_umbrella`` - When true, sets a path dependency pointing to
   "../#{app}", sharing the same environment as the current application

mix deps task
~~~~~~~~~~~~~

This task lists all dependencies in the following format:

-  APP VERSION (SCM) [locked at REF] STATUS

It supports the following options:

-  ``--all`` - check all dependencies, regardless of specified
   environment






Summary
-------

==================== =
:elixir:func:`run/1` Callback implementation of :elixir:func:`Mix.Task.run/1` 
==================== =





Functions
---------

.. elixir:function:: Mix.Tasks.Deps.run/1
   :sig: run(args)


   
   Callback implementation of :elixir:func:`Mix.Task.run/1`.
   
   







