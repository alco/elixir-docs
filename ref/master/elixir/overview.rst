Elixir v0.14.0-dev
==================


* Modules_


* Exceptions_


* Protocols_



Modules
-------

===================================== =
:elixir:mod:`Agent`                   Agents are a simple abstraction around state 

:elixir:mod:`Application`             A module for working with applications and defining application callbacks 

:elixir:mod:`Atom`                    

:elixir:mod:`Base`                    This module provides data encoding and decoding functions according to `RFC 4648 <http://tools.ietf.org/html/rfc4648>`__ 

:elixir:mod:`Behaviour`               Utilities for defining behaviour interfaces 

:elixir:mod:`Bitwise`                 This module provides macros and operators for bitwise operators. These macros can be used in guards 

:elixir:mod:`Code`                    Utilities for managing code compilation, code evaluation and code loading 

:elixir:mod:`Dict`                    This module specifies the Dict API expected to be implemented by different dictionaries. It also provides functions that redirect to the underlying Dict, allowing a developer to work with different Dict implementations using one API 

:elixir:mod:`Enum`                    Provides a set of algorithms that enumerate over collections according to the ```Enumerable`` <Enumerable.html>`__ protocol: 

:elixir:mod:`Exception`               Functions to format throw/catch/exit and exceptions 

:elixir:mod:`File`                    This module contains functions to manipulate files 

:elixir:mod:`File.Stat`               A struct responsible to hold file information 

:elixir:mod:`File.Stream`             Defines a ```File.Stream`` <File.Stream.html>`__ struct returned by ``File.stream!/2`` 

:elixir:mod:`Float`                   Functions for working with floating point numbers 

:elixir:mod:`GenEvent`                A behaviour module for implementing event handling functionality 

:elixir:mod:`GenServer`               A behaviour module for implementing the server of a client-server relation 

:elixir:mod:`HashDict`                A key-value store 

:elixir:mod:`HashSet`                 A set store 

:elixir:mod:`IO`                      Functions handling IO 

:elixir:mod:`IO.ANSI`                 Functionality to render ANSI escape sequences (http://en.wikipedia.org/wiki/ANSI\_escape\_code) â characters embedded in text used to control formatting, color, and other output options on video text terminals 

:elixir:mod:`IO.Stream`               Defines a ```IO.Stream`` <IO.Stream.html>`__ struct returned by ```IO.stream/2`` <IO.html#stream/2>`__ and ```IO.binstream/2`` <IO.html#binstream/2>`__ 

:elixir:mod:`Inspect.Algebra`         A set of functions for creating and manipulating algebra documents, as described in ["Strictly Pretty" (2000) by Christian Lindig][0] 

:elixir:mod:`Inspect.Opts`            Defines the Inspect.Opts used by the Inspect protocol 

:elixir:mod:`Integer`                 Functions for working with integers 

:elixir:mod:`Kernel`                  ```Kernel`` <Kernel.html>`__ provides the default macros and functions Elixir imports into your environment. These macros and functions can be skipped or cherry-picked via the ``import`` macro. For instance, if you want to tell Elixir not to import the ``if`` macro, you can do: 

:elixir:mod:`Kernel.ParallelCompiler` A module responsible for compiling files in parallel 

:elixir:mod:`Kernel.ParallelRequire`  A module responsible for requiring files in parallel 

:elixir:mod:`Kernel.SpecialForms`     In this module we define Elixir special forms. Special forms cannot be overridden by the developer and are the basic building blocks of Elixir code 

:elixir:mod:`Kernel.Typespec`         Provides macros and functions for working with typespecs 

:elixir:mod:`Keyword`                 A keyword is a list of tuples where the first element of the tuple is an atom and the second element can be any value 

:elixir:mod:`List`                    Implements functions that only make sense for lists and cannot be part of the Enum protocol. In general, favor using the Enum API instead of List 

:elixir:mod:`Macro`                   Conveniences for working with macros 

:elixir:mod:`Macro.Env`               A struct that holds compile time environment information 

:elixir:mod:`Map`                     A Dict implementation that works on maps 

:elixir:mod:`Module`                  This module provides many functions to deal with modules during compilation time. It allows a developer to dynamically attach documentation, add, delete and register attributes and so forth 

:elixir:mod:`Node`                    Functions related to VM nodes 

:elixir:mod:`OptionParser`            This module contains functions to parse command line arguments 

:elixir:mod:`Path`                    This module provides conveniences for manipulating or retrieving file system paths 

:elixir:mod:`Port`                    Functions related to Erlang ports 

:elixir:mod:`Process`                 Conveniences for working with processes and the process dictionary 

:elixir:mod:`Protocol`                Functions for working with protocols 

:elixir:mod:`Range`                   Defines a Range 

:elixir:mod:`Record`                  Module to work, define and import records 

:elixir:mod:`Regex`                   Regular expressions for Elixir built on top of Erlang's ``re`` module 

:elixir:mod:`Set`                     This module specifies the Set API expected to be implemented by different representations 

:elixir:mod:`Stream`                  Module for creating and composing streams 

:elixir:mod:`String`                  A String in Elixir is a UTF-8 encoded binary 

:elixir:mod:`StringIO`                This module provides an IO device that wraps a string 

:elixir:mod:`Supervisor`              A behaviour module for implementing supevision functionality 

:elixir:mod:`Supervisor.Spec`         Convenience functions for defining a supervision specification 

:elixir:mod:`System`                  The System module provides access to variables used or maintained by the VM and to functions that interact directly with the VM or the host system 

:elixir:mod:`Task`                    Conveniences for spawning and awaiting for tasks 

:elixir:mod:`Task.Supervisor`         A tasks supervisor 

:elixir:mod:`Tuple`                   Functions for working with tuples 

:elixir:mod:`URI`                     Utilities for working with and creating URIs 

:elixir:mod:`Version`                 Functions for parsing and matching versions against requirements 
===================================== =

.. toctree::
   :hidden:

   
   Agent
   
   Application
   
   Atom
   
   Base
   
   Behaviour
   
   Bitwise
   
   Code
   
   Dict
   
   Enum
   
   Exception
   
   File
   
   File.Stat
   
   File.Stream
   
   Float
   
   GenEvent
   
   GenServer
   
   HashDict
   
   HashSet
   
   IO
   
   IO.ANSI
   
   IO.Stream
   
   Inspect.Algebra
   
   Inspect.Opts
   
   Integer
   
   Kernel
   
   Kernel.ParallelCompiler
   
   Kernel.ParallelRequire
   
   Kernel.SpecialForms
   
   Kernel.Typespec
   
   Keyword
   
   List
   
   Macro
   
   Macro.Env
   
   Map
   
   Module
   
   Node
   
   OptionParser
   
   Path
   
   Port
   
   Process
   
   Protocol
   
   Range
   
   Record
   
   Regex
   
   Set
   
   Stream
   
   String
   
   StringIO
   
   Supervisor
   
   Supervisor.Spec
   
   System
   
   Task
   
   Task.Supervisor
   
   Tuple
   
   URI
   
   Version
   




Exceptions
----------

============================================= =
:elixir:mod:`ArgumentError`                   

:elixir:mod:`ArithmeticError`                 

:elixir:mod:`BadArityError`                   

:elixir:mod:`BadFunctionError`                

:elixir:mod:`BadStructError`                  

:elixir:mod:`CaseClauseError`                 

:elixir:mod:`Code.LoadError`                  

:elixir:mod:`CompileError`                    

:elixir:mod:`Enum.EmptyError`                 

:elixir:mod:`Enum.OutOfBoundsError`           

:elixir:mod:`ErlangError`                     

:elixir:mod:`File.CopyError`                  

:elixir:mod:`File.Error`                      

:elixir:mod:`FunctionClauseError`             

:elixir:mod:`IO.StreamError`                  

:elixir:mod:`KeyError`                        

:elixir:mod:`MatchError`                      

:elixir:mod:`Protocol.UndefinedError`         

:elixir:mod:`Regex.CompileError`              

:elixir:mod:`RuntimeError`                    

:elixir:mod:`SyntaxError`                     

:elixir:mod:`SystemLimitError`                

:elixir:mod:`TokenMissingError`               

:elixir:mod:`TryClauseError`                  

:elixir:mod:`UndefinedFunctionError`          

:elixir:mod:`UnicodeConversionError`          

:elixir:mod:`Version.InvalidRequirementError` 

:elixir:mod:`Version.InvalidVersionError`     
============================================= =

.. toctree::
   :hidden:

   
   ArgumentError
   
   ArithmeticError
   
   BadArityError
   
   BadFunctionError
   
   BadStructError
   
   CaseClauseError
   
   Code.LoadError
   
   CompileError
   
   Enum.EmptyError
   
   Enum.OutOfBoundsError
   
   ErlangError
   
   File.CopyError
   
   File.Error
   
   FunctionClauseError
   
   IO.StreamError
   
   KeyError
   
   MatchError
   
   Protocol.UndefinedError
   
   Regex.CompileError
   
   RuntimeError
   
   SyntaxError
   
   SystemLimitError
   
   TokenMissingError
   
   TryClauseError
   
   UndefinedFunctionError
   
   UnicodeConversionError
   
   Version.InvalidRequirementError
   
   Version.InvalidVersionError
   



Protocols
---------

============================ =
:elixir:mod:`Access`         The Access protocol is the underlying protocol invoked when the brackets syntax is used. For instance, ``foo[bar]`` is translated to ``access foo, bar`` which, by default, invokes the ``Access.access`` protocol 

:elixir:mod:`Collectable`    A protocol to traverse data structures 

:elixir:mod:`Enumerable`     Enumerable protocol used by ```Enum`` <Enum.html>`__ and ```Stream`` <Stream.html>`__ modules 

:elixir:mod:`Inspect`        The ```Inspect`` <Inspect.html>`__ protocol is responsible for converting any Elixir data structure into an algebra document. This document is then formatted, either in pretty printing format or a regular one 

:elixir:mod:`List.Chars`     The List.Chars protocol is responsible for converting a structure to a list (only if applicable). The only function required to be implemented is ``to_char_list`` which does the conversion 

:elixir:mod:`Range.Iterator` A protocol used for iterating range elements 

:elixir:mod:`String.Chars`   The String.Chars protocol is responsible for converting a structure to a Binary (only if applicable). The only function required to be implemented is ``to_string`` which does the conversion 
============================ =

.. toctree::
   :hidden:

   
   Access
   
   Collectable
   
   Enumerable
   
   Inspect
   
   List.Chars
   
   Range.Iterator
   
   String.Chars
   

