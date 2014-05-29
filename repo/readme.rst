Readme
========


For more about Elixir, installation and documentation, `check Elixir's
website <http://elixir-lang.org/>`__.

Usage
-----

If you want to contribute to Elixir or run it from source, clone this
repository to your machine, compile and test it:

::

    $ git clone https://github.com/elixir-lang/elixir.git
    $ cd elixir
    $ make clean test

If Elixir fails to build (specifically when pulling in a new version via
git), be sure to remove any previous build artifacts by running
``make clean``, then ``make test``.

If tests pass, you are ready to move on to the `Getting Started
guide <http://elixir-lang.org>`__ or to try Interactive Elixir by
running: ``bin/iex`` in your terminal.

However, if tests fail, it is likely you have an outdated Erlang version
(Elixir requires Erlang 17.0 or later). You can check your Erlang
version by calling ``erl`` in the command line. You will see some
information as follows:

::

    Erlang/OTP 17 [erts-6.0] [source-07b8f44] [64-bit] [smp:4:4] [async-threads:10] [hipe] [kernel-poll:false]

If you have the correct version and tests still fail, feel free to `open
an issue <https://github.com/elixir-lang/elixir/issues>`__.

Building documentation
----------------------

Building the documentation requires
`ex\_doc <https://github.com/elixir-lang/ex_doc>`__ to be installed and
built in the same containing folder as elixir.

::

    # After cloning and compiling Elixir
    $ git clone git://github.com/elixir-lang/ex_doc.git
    $ cd ex_doc && ../elixir/bin/mix compile
    $ cd ../elixir && make docs

Contributing
------------

We appreciate any contribution to Elixir, so check out our
`CONTRIBUTING.md <CONTRIBUTING.md>`__ guide for more information. We
usually keep a list of features and bugs `in the issue
tracker <https://github.com/elixir-lang/elixir/issues>`__.

Important links
---------------

-  #elixir-lang on freenode IRC
-  `Website <http://elixir-lang.org>`__
-  `Issue tracker <https://github.com/elixir-lang/elixir/issues>`__
-  `elixir-talk Mailing list
   (questions) <http://groups.google.com/group/elixir-lang-talk>`__
-  `elixir-core Mailing list
   (development) <http://groups.google.com/group/elixir-lang-core>`__

License
-------

"Elixir" and the Elixir logo are copyright (c) 2012 Plataformatec.

Elixir source code is released under Apache 2 License with some parts
under Erlang's license (EPL).

Check `LEGAL <LEGAL>`__ and `LICENSE <LICENSE>`__ files for more
information.

.. |Elixir| image:: https://github.com/elixir-lang/elixir-lang.github.com/raw/master/images/logo/logo.png
.. |Build Status| image:: https://secure.travis-ci.org/elixir-lang/elixir.svg?branch=master
   :target: http://travis-ci.org/elixir-lang/elixir
