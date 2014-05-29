Macro.Env
==============================================================

.. elixir:module:: Macro.Env

   :mtype: 

Overview
--------

A struct that holds compile time environment information.

The current environment can be accessed at any time as ``__ENV__``.
Inside macros, the caller environment can be accessed as ``__CALLER__``.
It contains the following fields:

-  ``module`` - the current module name.
-  ``file`` - the current file name as a binary
-  ``line`` - the current line as an integer
-  ``function`` - a tuple as ``{atom, integer``}, where the first
   element is the function name and the seconds its arity. Returns
   ``nil`` if not inside a function
-  ``context`` - the context of the environment. It can be nil (default
   context), inside a guard or inside an assign
-  ``aliases`` - a list of two item tuples, where the first item is the
   aliased name and the second the actual name
-  ``requires`` - the list of required modules
-  ``functions`` - a list of functions imported from each module
-  ``macros`` - a list of macros imported from each module
-  ``macro_aliases`` - a list of aliases defined inside the current
   macro
-  ``context_modules`` - a list of modules defined in the current
   context
-  ``vars`` - a list keeping all defined variables as {var, context}
-  ``export_vars`` - a list keeping all variables to be exported in a
   construct (may be nil)
-  ``lexical_tracker`` - PID to the lexical tracker which is responsible
   to keep user info
-  ``local`` - the module to expand local functions to






Summary
-------

=========================== =
:elixir:func:`in_guard?/1`  Returns whether the compilation environment is currently inside a guard 

:elixir:func:`in_match?/1`  Returns whether the compilation environment is currently inside a match clause 

:elixir:func:`location/1`   Returns a keyword list containing the file and line information as keys 

:elixir:func:`stacktrace/1` Returns the environment stacktrace 
=========================== =



Types
-----

.. elixir:type:: Macro.Env.name_arity/0

   :elixir:type:`name_arity/0` :: {atom, non_neg_integer}
   

.. elixir:type:: Macro.Env.file/0

   :elixir:type:`file/0` :: binary
   

.. elixir:type:: Macro.Env.line/0

   :elixir:type:`line/0` :: non_neg_integer
   

.. elixir:type:: Macro.Env.aliases/0

   :elixir:type:`aliases/0` :: [{module, module}]
   

.. elixir:type:: Macro.Env.macro_aliases/0

   :elixir:type:`macro_aliases/0` :: [{module, {integer, module}}]
   

.. elixir:type:: Macro.Env.context/0

   :elixir:type:`context/0` :: :match | :guard | nil
   

.. elixir:type:: Macro.Env.requires/0

   :elixir:type:`requires/0` :: [module]
   

.. elixir:type:: Macro.Env.functions/0

   :elixir:type:`functions/0` :: [{module, [:elixir:type:`name_arity/0`]}]
   

.. elixir:type:: Macro.Env.macros/0

   :elixir:type:`macros/0` :: [{module, [:elixir:type:`name_arity/0`]}]
   

.. elixir:type:: Macro.Env.context_modules/0

   :elixir:type:`context_modules/0` :: [module]
   

.. elixir:type:: Macro.Env.vars/0

   :elixir:type:`vars/0` :: [{atom, atom | non_neg_integer}]
   

.. elixir:type:: Macro.Env.export_vars/0

   :elixir:type:`export_vars/0` :: :elixir:type:`vars/0` | nil
   

.. elixir:type:: Macro.Env.lexical_tracker/0

   :elixir:type:`lexical_tracker/0` :: pid
   

.. elixir:type:: Macro.Env.local/0

   :elixir:type:`local/0` :: module | nil
   

.. elixir:type:: Macro.Env.t/0

   :elixir:type:`t/0` :: %Macro.Env{module: module, file: :elixir:type:`file/0`, line: :elixir:type:`line/0`, function: :elixir:type:`name_arity/0` | nil, context: :elixir:type:`context/0`, requires: :elixir:type:`requires/0`, aliases: :elixir:type:`aliases/0`, functions: :elixir:type:`functions/0`, macros: :elixir:type:`macros/0`, macro_aliases: :elixir:type:`aliases/0`, context_modules: :elixir:type:`context_modules/0`, vars: :elixir:type:`vars/0`, export_vars: :elixir:type:`export_vars/0`, lexical_tracker: :elixir:type:`lexical_tracker/0`, local: :elixir:type:`local/0`}
   





Functions
---------

.. elixir:function:: Macro.Env.in_guard?/1
   :sig: in_guard?(arg1)


   
   Returns whether the compilation environment is currently inside a guard.
   
   

.. elixir:function:: Macro.Env.in_match?/1
   :sig: in_match?(arg1)


   
   Returns whether the compilation environment is currently inside a match
   clause.
   
   

.. elixir:function:: Macro.Env.location/1
   :sig: location(arg1)


   
   Returns a keyword list containing the file and line information as keys.
   
   

.. elixir:function:: Macro.Env.stacktrace/1
   :sig: stacktrace(env)


   
   Returns the environment stacktrace.
   
   







