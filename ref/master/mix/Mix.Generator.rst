Mix.Generator
==============================================================

.. elixir:module:: Mix.Generator

   :mtype: 

Overview
--------

Conveniences for working with paths and generating content.

All of those functions are verbose, in the sense they log the action to
be performed via ``Mix.shell``.





Summary
-------

================================= =
:elixir:func:`create_directory/1` Creates a directory if one does not exist yet 

:elixir:func:`create_file/2`      Creates a file with the given contents. If the file already exists, asks for user confirmation 

:elixir:func:`embed_template/2`   Embed a template given by ``contents`` into the current module 

:elixir:func:`embed_text/2`       Embeds a text given by ``contents`` into the current module 

:elixir:func:`from_file/1`        Reads the content from a file relative to the current file and not relative to the cwd. Useful when used with embed macros: 
================================= =





Functions
---------

.. elixir:function:: Mix.Generator.create_directory/1
   :sig: create_directory(path)


   
   Creates a directory if one does not exist yet.
   
   

.. elixir:function:: Mix.Generator.create_file/2
   :sig: create_file(path, contents)


   
   Creates a file with the given contents. If the file already exists, asks
   for user confirmation.
   
   





Macros
------

.. elixir:macro:: Mix.Generator.embed_template/2
   :sig: embed_template(name, contents)


   
   Embed a template given by ``contents`` into the current module.
   
   It will define a private function with the ``name`` followed by
   ``_template`` that expects assigns as arguments.
   
   This function must be invoked passing a keyword list. Each key in the
   keyword list can be accessed in the template using the ``@`` macro.
   
   For more information, check ``EEx.SmartEngine``.
   
   

.. elixir:macro:: Mix.Generator.embed_text/2
   :sig: embed_text(name, contents)


   
   Embeds a text given by ``contents`` into the current module.
   
   It will define a private function with the ``name`` followed by
   ``_text`` that expects no argument.
   
   

.. elixir:macro:: Mix.Generator.from_file/1
   :sig: from_file(path)


   
   Reads the content from a file relative to the current file and not
   relative to the cwd. Useful when used with embed macros:
   
   ::
   
       embed_template :lib, from_file("../templates/lib.eex")
   
   
   





