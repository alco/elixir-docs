Protocol
==============================================================

.. elixir:module:: Protocol

   :mtype: 

Overview
--------

Functions for working with protocols.





Summary
-------

================================== =
:elixir:func:`assert_impl\!/2`     Checks if the given module is loaded and is an implementation of the given protocol 

:elixir:func:`assert_protocol\!/1` Checks if the given module is loaded and is protocol 

:elixir:func:`consolidate/2`       Receives a protocol and a list of implementations and consolidates the given protocol 

:elixir:func:`consolidated?/1`     Returns true if the protocol was consolidated 

:elixir:func:`def/1`               Defines a new protocol function 

:elixir:func:`extract_impls/2`     Extract all types implemented for the given protocol from the given paths 

:elixir:func:`extract_protocols/1` Extract all protocols from the given paths 
================================== =





Functions
---------

.. elixir:function:: Protocol.assert_impl!/2
   :sig: assert_impl!(protocol, impl)


   Specs:
   
 
   * assert_impl!(module, module) :: :ok | no_return
 

   
   Checks if the given module is loaded and is an implementation of the
   given protocol.
   
   Returns ``:ok`` if so, otherwise raises ArgumentError.
   
   

.. elixir:function:: Protocol.assert_protocol!/1
   :sig: assert_protocol!(module)


   Specs:
   
 
   * assert_protocol!(module) :: :ok | no_return
 

   
   Checks if the given module is loaded and is protocol.
   
   Returns ``:ok`` if so, otherwise raises ArgumentError.
   
   

.. elixir:function:: Protocol.consolidate/2
   :sig: consolidate(protocol, types)


   Specs:
   
 
   * consolidate(module, [module]) :: {:ok, binary} | {:error, :not_a_protocol} | {:error, :no_beam_info}
 

   
   Receives a protocol and a list of implementations and consolidates the
   given protocol.
   
   Consolidation happens by changing the protocol ``impl_for`` in the
   abstract format to have fast lookup rules. Usually the list of
   implementations to use during consolidation are retrieved with the help
   of :elixir:func:`extract_impls/2`.
   
   It returns the updated version of the protocol bytecode. A given
   bytecode or protocol implementation can be checked to be consolidated or
   not by analyzing the protocol attribute:
   
   ::
   
       Protocol.consolidated?(Enumerable)
   
   If the first element of the tuple is true, it means the protocol was
   consolidated.
   
   This function does not load the protocol at any point nor loads the new
   bytecode for the compiled module. However each implementation must be
   available and it will be loaded.
   
   

.. elixir:function:: Protocol.consolidated?/1
   :sig: consolidated?(protocol)


   Specs:
   
 
   * consolidated?(module) :: boolean
 

   
   Returns true if the protocol was consolidated.
   
   

.. elixir:function:: Protocol.extract_impls/2
   :sig: extract_impls(protocol, paths)


   Specs:
   
 
   * extract_impls(module, [char_list | :elixir:type:`String.t/0`]) :: [atom]
 

   
   Extract all types implemented for the given protocol from the given
   paths.
   
   The paths can be either a char list or a string. Internally they are
   worked on as char lists, so passing them as lists avoid extra
   conversion.
   
   Does not load any of the implementations.
   
   **Examples**
   
   ::
   
       # Get Elixir's ebin and retrieve all protocols
       iex> path = :code.lib_dir(:elixir, :ebin)
       iex> mods = Protocol.extract_impls(Enumerable, [path])
       iex> List in mods
       true
   
   
   

.. elixir:function:: Protocol.extract_protocols/1
   :sig: extract_protocols(paths)


   Specs:
   
 
   * extract_protocols([char_list | :elixir:type:`String.t/0`]) :: [atom]
 

   
   Extract all protocols from the given paths.
   
   The paths can be either a char list or a string. Internally they are
   worked on as char lists, so passing them as lists avoid extra
   conversion.
   
   Does not load any of the protocols.
   
   **Examples**
   
   ::
   
       # Get Elixir's ebin and retrieve all protocols
       iex> path = :code.lib_dir(:elixir, :ebin)
       iex> mods = Protocol.extract_protocols([path])
       iex> Enumerable in mods
       true
   
   
   





Macros
------

.. elixir:macro:: Protocol.def/1
   :sig: def(arg1)


   
   Defines a new protocol function.
   
   Protocols do not allow functions to be defined directly, instead, the
   regular ``Kernel.def/*`` macros are replaced by this macro which defines
   the protocol functions with the appropriate callbacks.
   
   





