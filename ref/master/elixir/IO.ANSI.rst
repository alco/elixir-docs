IO.ANSI
==============================================================

.. elixir:module:: IO.ANSI

   :mtype: 

Overview
--------

Functionality to render ANSI escape sequences
(http://en.wikipedia.org/wiki/ANSI\_escape\_code) — characters embedded
in text used to control formatting, color, and other output options on
video text terminals.





Summary
-------

===================================== =
:elixir:func:`black/0`                Sets foreground color to black 

:elixir:func:`black_background/0`     Sets background color to black 

:elixir:func:`blink_off/0`            Blink: off 

:elixir:func:`blink_rapid/0`          Blink: Rapid. MS-DOS ANSI.SYS; 150 per minute or more; not widely supported 

:elixir:func:`blink_slow/0`           Blink: Slow. Less than 150 per minute 

:elixir:func:`blue/0`                 Sets foreground color to blue 

:elixir:func:`blue_background/0`      Sets background color to blue 

:elixir:func:`bright/0`               Bright (increased intensity) or Bold 

:elixir:func:`clear/0`                Clear screen 

:elixir:func:`conceal/0`              Conceal. Not widely supported 

:elixir:func:`crossed_out/0`          Crossed-out. Characters legible, but marked for deletion. Not widely supported 

:elixir:func:`cyan/0`                 Sets foreground color to cyan 

:elixir:func:`cyan_background/0`      Sets background color to cyan 

:elixir:func:`default_background/0`   Default background color 

:elixir:func:`default_color/0`        Default text color 

:elixir:func:`encircled/0`            Encircled 

:elixir:func:`escape/2`               Escapes a string by converting named ANSI sequences into actual ANSI codes 

:elixir:func:`escape_fragment/2`      Escapes a string by converting named ANSI sequences into actual ANSI codes 

:elixir:func:`faint/0`                Faint (decreased intensity), not widely supported 

:elixir:func:`font_1/0`               Sets alternative font 1 

:elixir:func:`font_2/0`               Sets alternative font 2 

:elixir:func:`font_3/0`               Sets alternative font 3 

:elixir:func:`font_4/0`               Sets alternative font 4 

:elixir:func:`font_5/0`               Sets alternative font 5 

:elixir:func:`font_6/0`               Sets alternative font 6 

:elixir:func:`font_7/0`               Sets alternative font 7 

:elixir:func:`font_8/0`               Sets alternative font 8 

:elixir:func:`font_9/0`               Sets alternative font 9 

:elixir:func:`framed/0`               Framed 

:elixir:func:`green/0`                Sets foreground color to green 

:elixir:func:`green_background/0`     Sets background color to green 

:elixir:func:`home/0`                 Send cursor home 

:elixir:func:`inverse/0`              Image: Negative. Swap foreground and background 

:elixir:func:`italic/0`               Italic: on. Not widely supported. Sometimes treated as inverse 

:elixir:func:`magenta/0`              Sets foreground color to magenta 

:elixir:func:`magenta_background/0`   Sets background color to magenta 

:elixir:func:`no_underline/0`         Underline: None 

:elixir:func:`normal/0`               Normal color or intensity 

:elixir:func:`not_framed_encircled/0` Not framed or encircled 

:elixir:func:`not_italic/0`           Not italic 

:elixir:func:`not_overlined/0`        Not overlined 

:elixir:func:`overlined/0`            Overlined 

:elixir:func:`primary_font/0`         Sets primary (default) font 

:elixir:func:`red/0`                  Sets foreground color to red 

:elixir:func:`red_background/0`       Sets background color to red 

:elixir:func:`reset/0`                Resets all attributes 

:elixir:func:`reverse/0`              Image: Negative. Swap foreground and background 

:elixir:func:`terminal?/1`            Checks whether the default I/O device is a terminal or a file 

:elixir:func:`underline/0`            Underline: Single 

:elixir:func:`white/0`                Sets foreground color to white 

:elixir:func:`white_background/0`     Sets background color to white 

:elixir:func:`yellow/0`               Sets foreground color to yellow 

:elixir:func:`yellow_background/0`    Sets background color to yellow 
===================================== =





Functions
---------

.. elixir:function:: IO.ANSI.black/0
   :sig: black()


   
   Sets foreground color to black
   
   

.. elixir:function:: IO.ANSI.black_background/0
   :sig: black_background()


   
   Sets background color to black
   
   

.. elixir:function:: IO.ANSI.blink_off/0
   :sig: blink_off()


   
   Blink: off
   
   

.. elixir:function:: IO.ANSI.blink_rapid/0
   :sig: blink_rapid()


   
   Blink: Rapid. MS-DOS ANSI.SYS; 150 per minute or more; not widely
   supported
   
   

.. elixir:function:: IO.ANSI.blink_slow/0
   :sig: blink_slow()


   
   Blink: Slow. Less than 150 per minute
   
   

.. elixir:function:: IO.ANSI.blue/0
   :sig: blue()


   
   Sets foreground color to blue
   
   

.. elixir:function:: IO.ANSI.blue_background/0
   :sig: blue_background()


   
   Sets background color to blue
   
   

.. elixir:function:: IO.ANSI.bright/0
   :sig: bright()


   
   Bright (increased intensity) or Bold
   
   

.. elixir:function:: IO.ANSI.clear/0
   :sig: clear()


   
   Clear screen
   
   

.. elixir:function:: IO.ANSI.conceal/0
   :sig: conceal()


   
   Conceal. Not widely supported
   
   

.. elixir:function:: IO.ANSI.crossed_out/0
   :sig: crossed_out()


   
   Crossed-out. Characters legible, but marked for deletion. Not widely
   supported.
   
   

.. elixir:function:: IO.ANSI.cyan/0
   :sig: cyan()


   
   Sets foreground color to cyan
   
   

.. elixir:function:: IO.ANSI.cyan_background/0
   :sig: cyan_background()


   
   Sets background color to cyan
   
   

.. elixir:function:: IO.ANSI.default_background/0
   :sig: default_background()


   
   Default background color
   
   

.. elixir:function:: IO.ANSI.default_color/0
   :sig: default_color()


   
   Default text color
   
   

.. elixir:function:: IO.ANSI.encircled/0
   :sig: encircled()


   
   Encircled
   
   

.. elixir:function:: IO.ANSI.escape/2
   :sig: escape(string, emit \\ terminal?())


   Specs:
   
 
   * escape(:elixir:type:`String.t/0`, emit :: boolean) :: :elixir:type:`String.t/0`
 

   
   Escapes a string by converting named ANSI sequences into actual ANSI
   codes.
   
   The format for referring to sequences is ``%{red}`` and
   ``%{red,bright}`` (for multiple sequences).
   
   It will also append a ``%{reset}`` to the string. If you don't want this
   behaviour, use :elixir:func:`escape_fragment/2`.
   
   An optional boolean parameter can be passed to enable or disable
   emitting actual ANSI codes. When ``false``, no ANSI codes will emitted.
   By default, standard output will be checked if it is a terminal capable
   of handling these sequences (using :elixir:func:`terminal?/1` function)
   
   **Examples**
   
   ::
   
       iex> IO.ANSI.escape("Hello %{red,bright,green}yes", true)
       "Hello \e[31m\e[1m\e[32myes\e[0m"
   
   
   

.. elixir:function:: IO.ANSI.escape_fragment/2
   :sig: escape_fragment(string, emit \\ terminal?())


   Specs:
   
 
   * escape_fragment(:elixir:type:`String.t/0`, emit :: boolean) :: :elixir:type:`String.t/0`
 

   
   Escapes a string by converting named ANSI sequences into actual ANSI
   codes.
   
   The format for referring to sequences is ``%{red}`` and
   ``%{red,bright}`` (for multiple sequences).
   
   An optional boolean parameter can be passed to enable or disable
   emitting actual ANSI codes. When ``false``, no ANSI codes will emitted.
   By default, standard output will be checked if it is a terminal capable
   of handling these sequences (using :elixir:func:`terminal?/1` function)
   
   **Examples**
   
   ::
   
       iex> IO.ANSI.escape_fragment("Hello %{red,bright,green}yes", true)
       "Hello \e[31m\e[1m\e[32myes"
   
       iex> IO.ANSI.escape_fragment("%{reset}bye", true)
       "\e[0mbye"
   
   
   

.. elixir:function:: IO.ANSI.faint/0
   :sig: faint()


   
   Faint (decreased intensity), not widely supported
   
   

.. elixir:function:: IO.ANSI.font_1/0
   :sig: font_1()


   
   Sets alternative font 1
   
   

.. elixir:function:: IO.ANSI.font_2/0
   :sig: font_2()


   
   Sets alternative font 2
   
   

.. elixir:function:: IO.ANSI.font_3/0
   :sig: font_3()


   
   Sets alternative font 3
   
   

.. elixir:function:: IO.ANSI.font_4/0
   :sig: font_4()


   
   Sets alternative font 4
   
   

.. elixir:function:: IO.ANSI.font_5/0
   :sig: font_5()


   
   Sets alternative font 5
   
   

.. elixir:function:: IO.ANSI.font_6/0
   :sig: font_6()


   
   Sets alternative font 6
   
   

.. elixir:function:: IO.ANSI.font_7/0
   :sig: font_7()


   
   Sets alternative font 7
   
   

.. elixir:function:: IO.ANSI.font_8/0
   :sig: font_8()


   
   Sets alternative font 8
   
   

.. elixir:function:: IO.ANSI.font_9/0
   :sig: font_9()


   
   Sets alternative font 9
   
   

.. elixir:function:: IO.ANSI.framed/0
   :sig: framed()


   
   Framed
   
   

.. elixir:function:: IO.ANSI.green/0
   :sig: green()


   
   Sets foreground color to green
   
   

.. elixir:function:: IO.ANSI.green_background/0
   :sig: green_background()


   
   Sets background color to green
   
   

.. elixir:function:: IO.ANSI.home/0
   :sig: home()


   
   Send cursor home
   
   

.. elixir:function:: IO.ANSI.inverse/0
   :sig: inverse()


   
   Image: Negative. Swap foreground and background
   
   

.. elixir:function:: IO.ANSI.italic/0
   :sig: italic()


   
   Italic: on. Not widely supported. Sometimes treated as inverse.
   
   

.. elixir:function:: IO.ANSI.magenta/0
   :sig: magenta()


   
   Sets foreground color to magenta
   
   

.. elixir:function:: IO.ANSI.magenta_background/0
   :sig: magenta_background()


   
   Sets background color to magenta
   
   

.. elixir:function:: IO.ANSI.no_underline/0
   :sig: no_underline()


   
   Underline: None
   
   

.. elixir:function:: IO.ANSI.normal/0
   :sig: normal()


   
   Normal color or intensity
   
   

.. elixir:function:: IO.ANSI.not_framed_encircled/0
   :sig: not_framed_encircled()


   
   Not framed or encircled
   
   

.. elixir:function:: IO.ANSI.not_italic/0
   :sig: not_italic()


   
   Not italic
   
   

.. elixir:function:: IO.ANSI.not_overlined/0
   :sig: not_overlined()


   
   Not overlined
   
   

.. elixir:function:: IO.ANSI.overlined/0
   :sig: overlined()


   
   Overlined
   
   

.. elixir:function:: IO.ANSI.primary_font/0
   :sig: primary_font()


   
   Sets primary (default) font
   
   

.. elixir:function:: IO.ANSI.red/0
   :sig: red()


   
   Sets foreground color to red
   
   

.. elixir:function:: IO.ANSI.red_background/0
   :sig: red_background()


   
   Sets background color to red
   
   

.. elixir:function:: IO.ANSI.reset/0
   :sig: reset()


   
   Resets all attributes
   
   

.. elixir:function:: IO.ANSI.reverse/0
   :sig: reverse()


   
   Image: Negative. Swap foreground and background
   
   

.. elixir:function:: IO.ANSI.terminal?/1
   :sig: terminal?(device \\ :erlang.group_leader())


   Specs:
   
 
   * terminal?(:io.device) :: boolean
 

   
   Checks whether the default I/O device is a terminal or a file.
   
   Used to identify whether printing ANSI escape sequences will likely be
   displayed as intended. This is checked by sending a message to the group
   leader. In case the group leader does not support the message, it will
   likely lead to a timeout (and a slow down on execution time).
   
   

.. elixir:function:: IO.ANSI.underline/0
   :sig: underline()


   
   Underline: Single
   
   

.. elixir:function:: IO.ANSI.white/0
   :sig: white()


   
   Sets foreground color to white
   
   

.. elixir:function:: IO.ANSI.white_background/0
   :sig: white_background()


   
   Sets background color to white
   
   

.. elixir:function:: IO.ANSI.yellow/0
   :sig: yellow()


   
   Sets foreground color to yellow
   
   

.. elixir:function:: IO.ANSI.yellow_background/0
   :sig: yellow_background()


   
   Sets background color to yellow
   
   







