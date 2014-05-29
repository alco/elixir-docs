Inspect.Opts
==============================================================

.. elixir:module:: Inspect.Opts

   :mtype: 

Overview
--------

Defines the Inspect.Opts used by the Inspect protocol.

The following fields are available:

-  ``:structs`` - when false, structs are not formatted by the inspect
   protocol, they are instead printed as maps, defaults to true;

-  ``:binaries`` - when ``:as_strings`` all binaries will be printed as
   strings, non-printable bytes will be escaped; when ``:as_binaries``
   all binaries will be printed in bit syntax; when the default
   ``:infer``, the binary will be printed as a string if it is
   printable, otherwise in bit syntax;

-  ``:char_lists`` - when ``:as_char_lists`` all lists will be printed
   as char lists, non-printable elements will be escaped; when
   ``:as_lists`` all lists will be printed as lists; when the default
   ``:infer``, the list will be printed as a char list if it is
   printable, otherwise as list;

-  ``:limit`` - limits the number of items that are printed for tuples,
   bitstrings, and lists, does not apply to strings nor char lists,
   defaults to 50;

-  ``:pretty`` - if set to true enables pretty printing, defaults to
   false;

-  ``:width`` - defaults to the 80 characters;









Types
-----

.. elixir:type:: Inspect.Opts.t/0

   :elixir:type:`t/0` :: %Inspect.Opts{structs: boolean, binaries: :infer | :as_binaries | :as_strings, char_lists: :infer | :as_lists | :as_char_lists, limit: pos_integer, width: pos_integer | :infinity, pretty: boolean}
   









