URI
==============================================================

.. elixir:module:: URI

   :mtype: 

Overview
--------

Utilities for working with and creating URIs.





Summary
-------

================================= =
:elixir:func:`decode/1`           Percent-unescape a URI 

:elixir:func:`decode/2`           

:elixir:func:`decode_query/2`     Decodes a query string into a dictionary (by default uses a map) 

:elixir:func:`default_port/1`     Returns the default port for a given scheme 

:elixir:func:`default_port/2`     Registers a scheme with a default port 

:elixir:func:`encode/1`           Percent-escape a URI 

:elixir:func:`encode_query/1`     Encodes an enumerable into a query string 

:elixir:func:`normalize_scheme/1` Normalizes the scheme according to the spec by downcasing it 

:elixir:func:`parse/1`            Parses a URI into components 

:elixir:func:`query_decoder/1`    Returns an iterator function over the query string that decodes the query string in steps 
================================= =



Types
-----

.. elixir:type:: URI.t/0

   :elixir:type:`t/0` :: %URI{scheme: term, path: term, query: term, fragment: term, authority: term, userinfo: term, host: term, port: term}
   





Functions
---------

.. elixir:function:: URI.decode/1
   :sig: decode(uri)


   
   Percent-unescape a URI.
   
   **Examples**
   
   ::
   
       iex> URI.decode("http%3A%2F%2Felixir-lang.org")
       "http://elixir-lang.org"
   
   
   

.. elixir:function:: URI.decode/2
   :sig: decode(arg1, uri)


   
   
   

.. elixir:function:: URI.decode_query/2
   :sig: decode_query(q, dict \\ %{})


   
   Decodes a query string into a dictionary (by default uses a map).
   
   Given a query string of the form "key1=value1&key2=value2...", produces
   a map with one entry for each key-value pair. Each key and value will be
   a binary. Keys and values will be percent-unescaped.
   
   Use :elixir:func:`query_decoder/1` if you want to iterate over each value manually.
   
   **Examples**
   
   ::
   
       iex> URI.decode_query("foo=1&bar=2")
       %{"bar" => "2", "foo" => "1"}
   
   
   

.. elixir:function:: URI.default_port/1
   :sig: default_port(scheme)


   
   Returns the default port for a given scheme.
   
   If the scheme is unknown to URI, returns ``nil``. Any scheme may be
   registered via :elixir:func:`default_port/2`.
   
   **Examples**
   
   ::
   
       iex> URI.default_port("ftp")
       21
   
       iex> URI.default_port("ponzi")
       nil
   
   
   

.. elixir:function:: URI.default_port/2
   :sig: default_port(scheme, port)


   
   Registers a scheme with a default port.
   
   It is recommended for this function to be invoked in your application
   start callback in case you want to register new URIs.
   
   

.. elixir:function:: URI.encode/1
   :sig: encode(s)


   
   Percent-escape a URI.
   
   **Example**
   
   ::
   
       iex> URI.encode("http://elixir-lang.org/getting_started/2.html")
       "http%3A%2F%2Felixir-lang.org%2Fgetting_started%2F2.html"
   
   
   

.. elixir:function:: URI.encode_query/1
   :sig: encode_query(l)


   
   Encodes an enumerable into a query string.
   
   Takes an enumerable (containing a sequence of two-item tuples) and
   returns a string of the form "key1=value1&key2=value2..." where keys and
   values are URL encoded as per :elixir:func:`encode/1`.
   
   Keys and values can be any term that implements the :elixir:mod:`String.Chars`
   protocol, except lists which are explicitly forbidden.
   
   **Examples**
   
   ::
   
       iex> hd = %{"foo" => 1, "bar" => 2}
       iex> URI.encode_query(hd)
       "bar=2&foo=1"
   
   
   

.. elixir:function:: URI.normalize_scheme/1
   :sig: normalize_scheme(scheme)


   
   Normalizes the scheme according to the spec by downcasing it.
   
   

.. elixir:function:: URI.parse/1
   :sig: parse(s)


   
   Parses a URI into components.
   
   URIs have portions that are handled specially for the particular scheme
   of the URI. For example, http and https have different default ports.
   Such values can be accessed and registered via :elixir:func:`URI.default_port/1`
   and :elixir:func:`URI.default_port/2`.
   
   **Examples**
   
   ::
   
       iex> URI.parse("http://elixir-lang.org/")
       %URI{scheme: "http", path: "/", query: nil, fragment: nil,
            authority: "elixir-lang.org", userinfo: nil,
            host: "elixir-lang.org", port: 80}
   
   
   

.. elixir:function:: URI.query_decoder/1
   :sig: query_decoder(q)


   
   Returns an iterator function over the query string that decodes the
   query string in steps.
   
   **Examples**
   
   ::
   
       iex> URI.query_decoder("foo=1&bar=2") |> Enum.map &(&1)
       [{"foo", "1"}, {"bar", "2"}]
   
   
   







