Base
==============================================================

.. elixir:module:: Base

   :mtype: 

Overview
--------

This module provides data encoding and decoding functions according to
`RFC 4648 <http://tools.ietf.org/html/rfc4648>`__.

This document defines the commonly used base 64, base 32, and base 16
encoding schemes.





Summary
-------

============================== =
:elixir:func:`decode16!/1`     Decodes a base 16 encoded string into a binary string 

:elixir:func:`decode16/1`      Decodes a base 16 encoded string into a binary string 

:elixir:func:`decode32!/1`     Decodes a base 32 encoded string into a binary string 

:elixir:func:`decode32/1`      Decodes a base 32 encoded string into a binary string 

:elixir:func:`decode64!/1`     Decodes a base 64 encoded string into a binary string 

:elixir:func:`decode64/1`      Decodes a base 64 encoded string into a binary string 

:elixir:func:`encode16/1`      Encodes a binary string into a base 16 encoded string 

:elixir:func:`encode32/1`      Encodes a binary string into a base 32 encoded string 

:elixir:func:`encode64/1`      Encodes a binary string into a base 64 encoded string 

:elixir:func:`hex_decode32!/1` Decodes a base 32 encoded string with extended hexadecimal alphabet into a binary string 

:elixir:func:`hex_decode32/1`  Decodes a base 32 encoded string with extended hexadecimal alphabet into a binary string 

:elixir:func:`hex_encode32/1`  Encodes a binary string into a base 32 encoded string with an extended hexadecimal alphabet 

:elixir:func:`url_decode64!/1` Decodes a base 64 encoded string with URL and filename safe alphabet into a binary string 

:elixir:func:`url_decode64/1`  Decodes a base 64 encoded string with URL and filename safe alphabet into a binary string 

:elixir:func:`url_encode64/1`  Encodes a binary string into a base 64 encoded string with URL and filename safe alphabet 
============================== =





Functions
---------

.. elixir:function:: Base.decode16/1
   :sig: decode16(string)


   Specs:
   
 
   * decode16(binary) :: {:ok, binary} | :error
 

   
   Decodes a base 16 encoded string into a binary string.
   
   The following alphabet is used both for encoding and decoding:
   
   +---------+------------+---------+------------+---------+------------+---------+------------+
   | Value   | Encoding   | Value   | Encoding   | Value   | Encoding   | Value   | Encoding   |
   +=========+============+=========+============+=========+============+=========+============+
   | 0       | 0          | 4       | 4          | 8       | 8          | 12      | C          |
   +---------+------------+---------+------------+---------+------------+---------+------------+
   | 1       | 1          | 5       | 5          | 9       | 9          | 13      | D          |
   +---------+------------+---------+------------+---------+------------+---------+------------+
   | 2       | 2          | 6       | 6          | 10      | A          | 14      | E          |
   +---------+------------+---------+------------+---------+------------+---------+------------+
   | 3       | 3          | 7       | 7          | 11      | B          | 15      | F          |
   +---------+------------+---------+------------+---------+------------+---------+------------+
   
   **Examples**
   
   ::
   
       iex> Base.decode16("666F6F626172")
       {:ok, "foobar"}
   
   
   

.. elixir:function:: Base.decode16!/1
   :sig: decode16!(string)


   Specs:
   
 
   * decode16!(binary) :: binary
 

   
   Decodes a base 16 encoded string into a binary string.
   
   An :elixir:mod:`ArgumentError` exception is raised if the padding is incorrect or
   a non-alphabet character is present in the string.
   
   **Examples**
   
   ::
   
       iex> Base.decode16!("666F6F626172")
       "foobar"
   
   
   

.. elixir:function:: Base.decode32/1
   :sig: decode32(string)


   Specs:
   
 
   * decode32(binary) :: {:ok, binary} | :error
 

   
   Decodes a base 32 encoded string into a binary string.
   
   The following alphabet is used both for encoding and decoding:
   
   +---------+------------+---------+------------+---------+------------+---------+------------+
   | Value   | Encoding   | Value   | Encoding   | Value   | Encoding   | Value   | Encoding   |
   +=========+============+=========+============+=========+============+=========+============+
   | 0       | A          | 9       | J          | 18      | S          | 27      | 3          |
   +---------+------------+---------+------------+---------+------------+---------+------------+
   | 1       | B          | 10      | K          | 19      | T          | 28      | 4          |
   +---------+------------+---------+------------+---------+------------+---------+------------+
   | 2       | C          | 11      | L          | 20      | U          | 29      | 5          |
   +---------+------------+---------+------------+---------+------------+---------+------------+
   | 3       | D          | 12      | M          | 21      | V          | 30      | 6          |
   +---------+------------+---------+------------+---------+------------+---------+------------+
   | 4       | E          | 13      | N          | 22      | W          | 31      | 7          |
   +---------+------------+---------+------------+---------+------------+---------+------------+
   | 5       | F          | 14      | O          | 23      | X          |         |            |
   +---------+------------+---------+------------+---------+------------+---------+------------+
   | 6       | G          | 15      | P          | 24      | Y          | (pad)   | =          |
   +---------+------------+---------+------------+---------+------------+---------+------------+
   | 7       | H          | 16      | Q          | 25      | Z          |         |            |
   +---------+------------+---------+------------+---------+------------+---------+------------+
   | 8       | I          | 17      | R          | 26      | 2          |         |            |
   +---------+------------+---------+------------+---------+------------+---------+------------+
   
   **Examples**
   
   ::
   
       iex> Base.decode32("MZXW6YTBOI======")
       {:ok, "foobar"}
   
   
   

.. elixir:function:: Base.decode32!/1
   :sig: decode32!(string)


   Specs:
   
 
   * decode32!(binary) :: binary
 

   
   Decodes a base 32 encoded string into a binary string.
   
   An :elixir:mod:`ArgumentError` exception is raised if the padding is incorrect or
   a non-alphabet character is present in the string.
   
   **Examples**
   
   ::
   
       iex> Base.decode32!("MZXW6YTBOI======")
       "foobar"
   
   
   

.. elixir:function:: Base.decode64/1
   :sig: decode64(string)


   Specs:
   
 
   * decode64(binary) :: {:ok, binary} | :error
 

   
   Decodes a base 64 encoded string into a binary string.
   
   The following alphabet is used both for encoding and decoding:
   
   +---------+------------+---------+------------+---------+------------+---------+------------+
   | Value   | Encoding   | Value   | Encoding   | Value   | Encoding   | Value   | Encoding   |
   +=========+============+=========+============+=========+============+=========+============+
   | 0       | A          | 17      | R          | 34      | i          | 51      | z          |
   +---------+------------+---------+------------+---------+------------+---------+------------+
   | 1       | B          | 18      | S          | 35      | j          | 52      | 0          |
   +---------+------------+---------+------------+---------+------------+---------+------------+
   | 2       | C          | 19      | T          | 36      | k          | 53      | 1          |
   +---------+------------+---------+------------+---------+------------+---------+------------+
   | 3       | D          | 20      | U          | 37      | l          | 54      | 2          |
   +---------+------------+---------+------------+---------+------------+---------+------------+
   | 4       | E          | 21      | V          | 38      | m          | 55      | 3          |
   +---------+------------+---------+------------+---------+------------+---------+------------+
   | 5       | F          | 22      | W          | 39      | n          | 56      | 4          |
   +---------+------------+---------+------------+---------+------------+---------+------------+
   | 6       | G          | 23      | X          | 40      | o          | 57      | 5          |
   +---------+------------+---------+------------+---------+------------+---------+------------+
   | 7       | H          | 24      | Y          | 41      | p          | 58      | 6          |
   +---------+------------+---------+------------+---------+------------+---------+------------+
   | 8       | I          | 25      | Z          | 42      | q          | 59      | 7          |
   +---------+------------+---------+------------+---------+------------+---------+------------+
   | 9       | J          | 26      | a          | 43      | r          | 60      | 8          |
   +---------+------------+---------+------------+---------+------------+---------+------------+
   | 10      | K          | 27      | b          | 44      | s          | 61      | 9          |
   +---------+------------+---------+------------+---------+------------+---------+------------+
   | 11      | L          | 28      | c          | 45      | t          | 62      | +          |
   +---------+------------+---------+------------+---------+------------+---------+------------+
   | 12      | M          | 29      | d          | 46      | u          | 63      | /          |
   +---------+------------+---------+------------+---------+------------+---------+------------+
   | 13      | N          | 30      | e          | 47      | v          |         |            |
   +---------+------------+---------+------------+---------+------------+---------+------------+
   | 14      | O          | 31      | f          | 48      | w          | (pad)   | =          |
   +---------+------------+---------+------------+---------+------------+---------+------------+
   | 15      | P          | 32      | g          | 49      | x          |         |            |
   +---------+------------+---------+------------+---------+------------+---------+------------+
   | 16      | Q          | 33      | h          | 50      | y          |         |            |
   +---------+------------+---------+------------+---------+------------+---------+------------+
   
   **Examples**
   
   ::
   
       iex> Base.decode64("Zm9vYmFy")
       {:ok, "foobar"}
   
   
   

.. elixir:function:: Base.decode64!/1
   :sig: decode64!(string)


   Specs:
   
 
   * decode64!(binary) :: binary
 

   
   Decodes a base 64 encoded string into a binary string.
   
   The following alphabet is used both for encoding and decoding:
   
   An :elixir:mod:`ArgumentError` exception is raised if the padding is incorrect or
   a non-alphabet character is present in the string.
   
   **Examples**
   
   ::
   
       iex> Base.decode64!("Zm9vYmFy")
       "foobar"
   
   
   

.. elixir:function:: Base.encode16/1
   :sig: encode16(data)


   Specs:
   
 
   * encode16(binary) :: binary
 

   
   Encodes a binary string into a base 16 encoded string.
   
   **Examples**
   
   ::
   
       iex> Base.encode16("foobar")
       "666F6F626172"
   
   
   

.. elixir:function:: Base.encode32/1
   :sig: encode32(data)


   Specs:
   
 
   * encode32(binary) :: binary
 

   
   Encodes a binary string into a base 32 encoded string.
   
   **Examples**
   
   ::
   
       iex> Base.encode32("foobar")
       "MZXW6YTBOI======"
   
   
   

.. elixir:function:: Base.encode64/1
   :sig: encode64(data)


   Specs:
   
 
   * encode64(binary) :: binary
 

   
   Encodes a binary string into a base 64 encoded string.
   
   **Examples**
   
   ::
   
       iex> Base.encode64("foobar")
       "Zm9vYmFy"
   
   
   

.. elixir:function:: Base.hex_decode32/1
   :sig: hex_decode32(string)


   Specs:
   
 
   * hex_decode32(binary) :: {:ok, binary} | :error
 

   
   Decodes a base 32 encoded string with extended hexadecimal alphabet into
   a binary string.
   
   The following alphabet is used both for encoding and decoding:
   
   +---------+------------+---------+------------+---------+------------+---------+------------+
   | Value   | Encoding   | Value   | Encoding   | Value   | Encoding   | Value   | Encoding   |
   +=========+============+=========+============+=========+============+=========+============+
   | 0       | 0          | 9       | 9          | 18      | I          | 27      | R          |
   +---------+------------+---------+------------+---------+------------+---------+------------+
   | 1       | 1          | 10      | A          | 19      | J          | 28      | S          |
   +---------+------------+---------+------------+---------+------------+---------+------------+
   | 2       | 2          | 11      | B          | 20      | K          | 29      | T          |
   +---------+------------+---------+------------+---------+------------+---------+------------+
   | 3       | 3          | 12      | C          | 21      | L          | 30      | U          |
   +---------+------------+---------+------------+---------+------------+---------+------------+
   | 4       | 4          | 13      | D          | 22      | M          | 31      | V          |
   +---------+------------+---------+------------+---------+------------+---------+------------+
   | 5       | 5          | 14      | E          | 23      | N          |         |            |
   +---------+------------+---------+------------+---------+------------+---------+------------+
   | 6       | 6          | 15      | F          | 24      | O          | (pad)   | =          |
   +---------+------------+---------+------------+---------+------------+---------+------------+
   | 7       | 7          | 16      | G          | 25      | P          |         |            |
   +---------+------------+---------+------------+---------+------------+---------+------------+
   | 8       | 8          | 17      | H          | 26      | Q          |         |            |
   +---------+------------+---------+------------+---------+------------+---------+------------+
   
   **Examples**
   
   ::
   
       iex> Base.hex_decode32("CPNMUOJ1E8======")
       {:ok, "foobar"}
   
   
   

.. elixir:function:: Base.hex_decode32!/1
   :sig: hex_decode32!(string)


   Specs:
   
 
   * hex_decode32!(binary) :: binary
 

   
   Decodes a base 32 encoded string with extended hexadecimal alphabet into
   a binary string.
   
   An :elixir:mod:`ArgumentError` exception is raised if the padding is incorrect or
   a non-alphabet character is present in the string.
   
   **Examples**
   
   ::
   
       iex> Base.hex_decode32!("CPNMUOJ1E8======")
       "foobar"
   
   
   

.. elixir:function:: Base.hex_encode32/1
   :sig: hex_encode32(data)


   Specs:
   
 
   * hex_encode32(binary) :: binary
 

   
   Encodes a binary string into a base 32 encoded string with an extended
   hexadecimal alphabet.
   
   **Examples**
   
   ::
   
       iex> Base.hex_encode32("foobar")
       "CPNMUOJ1E8======"
   
   
   

.. elixir:function:: Base.url_decode64/1
   :sig: url_decode64(string)


   Specs:
   
 
   * url_decode64(binary) :: {:ok, binary} | :error
 

   
   Decodes a base 64 encoded string with URL and filename safe alphabet
   into a binary string.
   
   The following alphabet is used both for encoding and decoding:
   
   +---------+------------+---------+------------+---------+------------+---------+--------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Value   | Encoding   | Value   | Encoding   | Value   | Encoding   | Value   | Encoding                                                                                                                                                     |
   +=========+============+=========+============+=========+============+=========+==============================================================================================================================================================+
   | 0       | A          | 17      | R          | 34      | i          | 51      | z                                                                                                                                                            |
   +---------+------------+---------+------------+---------+------------+---------+--------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | 1       | B          | 18      | S          | 35      | j          | 52      | 0                                                                                                                                                            |
   +---------+------------+---------+------------+---------+------------+---------+--------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | 2       | C          | 19      | T          | 36      | k          | 53      | 1                                                                                                                                                            |
   +---------+------------+---------+------------+---------+------------+---------+--------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | 3       | D          | 20      | U          | 37      | l          | 54      | 2                                                                                                                                                            |
   +---------+------------+---------+------------+---------+------------+---------+--------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | 4       | E          | 21      | V          | 38      | m          | 55      | 3                                                                                                                                                            |
   +---------+------------+---------+------------+---------+------------+---------+--------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | 5       | F          | 22      | W          | 39      | n          | 56      | 4                                                                                                                                                            |
   +---------+------------+---------+------------+---------+------------+---------+--------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | 6       | G          | 23      | X          | 40      | o          | 57      | 5                                                                                                                                                            |
   +---------+------------+---------+------------+---------+------------+---------+--------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | 7       | H          | 24      | Y          | 41      | p          | 58      | 6                                                                                                                                                            |
   +---------+------------+---------+------------+---------+------------+---------+--------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | 8       | I          | 25      | Z          | 42      | q          | 59      | 7                                                                                                                                                            |
   +---------+------------+---------+------------+---------+------------+---------+--------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | 9       | J          | 26      | a          | 43      | r          | 60      | 8                                                                                                                                                            |
   +---------+------------+---------+------------+---------+------------+---------+--------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | 10      | K          | 27      | b          | 44      | s          | 61      | 9                                                                                                                                                            |
   +---------+------------+---------+------------+---------+------------+---------+--------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | 11      | L          | 28      | c          | 45      | t          | 62      | -                                                                                                                                                            |
   +---------+------------+---------+------------+---------+------------+---------+--------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | 12      | M          | 29      | d          | 46      | u          | 63      | \_\| \| 13\| N\| 30\| e\| 47\| v\| \| \| \| 14\| O\| 31\| f\| 48\| w\| (pad)\| =\| \| 15\| P\| 32\| g\| 49\| x\| \| \| \| 16\| Q\| 33\| h\| 50\| y\| \| \|   |
   +---------+------------+---------+------------+---------+------------+---------+--------------------------------------------------------------------------------------------------------------------------------------------------------------+
   
   **Examples**
   
   ::
   
       iex> Base.url_decode64("_3_-_A==")
       {:ok, <<255,127,254,252>>}
   
   
   

.. elixir:function:: Base.url_decode64!/1
   :sig: url_decode64!(string)


   Specs:
   
 
   * url_decode64!(binary) :: binary
 

   
   Decodes a base 64 encoded string with URL and filename safe alphabet
   into a binary string.
   
   An :elixir:mod:`ArgumentError` exception is raised if the padding is incorrect or
   a non-alphabet character is present in the string.
   
   **Examples**
   
   ::
   
       iex> Base.url_decode64!("_3_-_A==")
       <<255,127,254,252>>
   
   
   

.. elixir:function:: Base.url_encode64/1
   :sig: url_encode64(data)


   Specs:
   
 
   * url_encode64(binary) :: binary
 

   
   Encodes a binary string into a base 64 encoded string with URL and
   filename safe alphabet.
   
   **Examples**
   
   ::
   
       iex> Base.url_encode64(<<255,127,254,252>>)
       "_3_-_A=="
   
   
   







