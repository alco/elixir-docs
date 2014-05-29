Mix v0.14.0-dev
===============


* Modules_


* Exceptions_




Modules
-------

========================================= =
:elixir:mod:`Mix`                         Mix is a build tool that provides tasks for creating, compiling and testing Elixir projects. Mix is inspired by the Leiningen build tool for Clojure and was written by one of its contributors 

:elixir:mod:`Mix.Archive`                 Module responsible for managing `archives <http://www.erlang.org/doc/man/code.html>`__ 

:elixir:mod:`Mix.Config`                  Module for reading and merging app configurations 

:elixir:mod:`Mix.Generator`               Conveniences for working with paths and generating content 

:elixir:mod:`Mix.Project`                 Defines and manipulate Mix projects 

:elixir:mod:`Mix.SCM`                     This module provides helper functions and defines the behaviour required by any SCM used by mix 

:elixir:mod:`Mix.Shell`                   Defines Mix.Shell contract 

:elixir:mod:`Mix.Shell.IO`                This is Mix's default shell. It simply prints messages to stdio and stderr 

:elixir:mod:`Mix.Shell.Process`           This is a Mix shell that uses the current process mailbox for communication instead of IO 

:elixir:mod:`Mix.Task`                    A simple module that provides conveniences for creating, loading and manipulating tasks 

:elixir:mod:`Mix.Tasks.App.Start`         Starts all registered apps. If no apps key exists, it starts the current application 

:elixir:mod:`Mix.Tasks.Archive`           Packages the current project (though not its dependencies) into a zip file according to the specification of the `Erlang Archive Format <http://www.erlang.org/doc/man/code.html>`__ 

:elixir:mod:`Mix.Tasks.Clean`             Clean generated application files 

:elixir:mod:`Mix.Tasks.Cmd`               Executes the given command 

:elixir:mod:`Mix.Tasks.Compile`           A meta task that compiles source files 

:elixir:mod:`Mix.Tasks.Compile.App`       Writes an .app file 

:elixir:mod:`Mix.Tasks.Compile.Elixir`    Compiles Elixir source files 

:elixir:mod:`Mix.Tasks.Compile.Erlang`    Compile Erlang source files 

:elixir:mod:`Mix.Tasks.Compile.Leex`      Compile Leex source files 

:elixir:mod:`Mix.Tasks.Compile.Protocols` Consolidates all protocols in all paths 

:elixir:mod:`Mix.Tasks.Compile.Yecc`      Compile Yecc source files 

:elixir:mod:`Mix.Tasks.Deps`              List all dependencies and their status 

:elixir:mod:`Mix.Tasks.Deps.Check`        Checks if all dependencies are valid and if not, abort. Prints the invalid dependencies' status before aborting 

:elixir:mod:`Mix.Tasks.Deps.Clean`        Remove the given dependencies' files 

:elixir:mod:`Mix.Tasks.Deps.Compile`      Compile dependencies 

:elixir:mod:`Mix.Tasks.Deps.Get`          Get all out of date dependencies, i.e. dependencies that are not available or have an invalid lock 

:elixir:mod:`Mix.Tasks.Deps.Loadpaths`    Loads all dependencies for the current build. This is invoked directly by ``loadpaths`` when the CLI boots 

:elixir:mod:`Mix.Tasks.Deps.Unlock`       Unlock the given dependencies 

:elixir:mod:`Mix.Tasks.Deps.Update`       Update the given dependencies 

:elixir:mod:`Mix.Tasks.Do`                Executes the tasks separated by comma 

:elixir:mod:`Mix.Tasks.Escriptize`        Generates an escript for the project 

:elixir:mod:`Mix.Tasks.Help`              Lists all tasks or prints the documentation for a given task 

:elixir:mod:`Mix.Tasks.Iex`               A task that is simply meant to redirect users to ``iex -S mix`` 

:elixir:mod:`Mix.Tasks.Loadconfig`        Loads and persists the project configuration 

:elixir:mod:`Mix.Tasks.Loadpaths`         Loads the application and its dependencies paths 

:elixir:mod:`Mix.Tasks.Local`             List local tasks 

:elixir:mod:`Mix.Tasks.Local.Hex`         Install hex locally from https://hex.pm/installs/hex.ez 

:elixir:mod:`Mix.Tasks.Local.Install`     Install an archive locally 

:elixir:mod:`Mix.Tasks.Local.Rebar`       Fetch a copy of rebar from the given path or url. It defaults to a rebar copy that ships with Elixir source if available or fetches it from http://s3.hex.pm/rebar 

:elixir:mod:`Mix.Tasks.Local.Uninstall`   Uninstall local tasks: 

:elixir:mod:`Mix.Tasks.New`               Creates a new Elixir project. It expects the path of the project as argument 

:elixir:mod:`Mix.Tasks.Run`               Runs the given file or expression in the context of the application 

:elixir:mod:`Mix.Tasks.Test`              Run the tests for a project 

:elixir:mod:`Mix.Utils`                   Utilities used throughout Mix and tasks 
========================================= =

.. toctree::
   :hidden:

   
   Mix
   
   Mix.Archive
   
   Mix.Config
   
   Mix.Generator
   
   Mix.Project
   
   Mix.SCM
   
   Mix.Shell
   
   Mix.Shell.IO
   
   Mix.Shell.Process
   
   Mix.Task
   
   Mix.Tasks.App.Start
   
   Mix.Tasks.Archive
   
   Mix.Tasks.Clean
   
   Mix.Tasks.Cmd
   
   Mix.Tasks.Compile
   
   Mix.Tasks.Compile.App
   
   Mix.Tasks.Compile.Elixir
   
   Mix.Tasks.Compile.Erlang
   
   Mix.Tasks.Compile.Leex
   
   Mix.Tasks.Compile.Protocols
   
   Mix.Tasks.Compile.Yecc
   
   Mix.Tasks.Deps
   
   Mix.Tasks.Deps.Check
   
   Mix.Tasks.Deps.Clean
   
   Mix.Tasks.Deps.Compile
   
   Mix.Tasks.Deps.Get
   
   Mix.Tasks.Deps.Loadpaths
   
   Mix.Tasks.Deps.Unlock
   
   Mix.Tasks.Deps.Update
   
   Mix.Tasks.Do
   
   Mix.Tasks.Escriptize
   
   Mix.Tasks.Help
   
   Mix.Tasks.Iex
   
   Mix.Tasks.Loadconfig
   
   Mix.Tasks.Loadpaths
   
   Mix.Tasks.Local
   
   Mix.Tasks.Local.Hex
   
   Mix.Tasks.Local.Install
   
   Mix.Tasks.Local.Rebar
   
   Mix.Tasks.Local.Uninstall
   
   Mix.Tasks.New
   
   Mix.Tasks.Run
   
   Mix.Tasks.Test
   
   Mix.Utils
   




Exceptions
----------

==================================== =
:elixir:mod:`Mix.ElixirVersionError` 

:elixir:mod:`Mix.Error`              

:elixir:mod:`Mix.InvalidTaskError`   

:elixir:mod:`Mix.NoProjectError`     

:elixir:mod:`Mix.NoTaskError`        
==================================== =

.. toctree::
   :hidden:

   
   Mix.ElixirVersionError
   
   Mix.Error
   
   Mix.InvalidTaskError
   
   Mix.NoProjectError
   
   Mix.NoTaskError
   



