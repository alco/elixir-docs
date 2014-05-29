Mix.Tasks.Deps.Clean
==============================================================

.. elixir:module:: Mix.Tasks.Deps.Clean

   :mtype: 

Overview
--------

Remove the given dependencies' files.

Since this is a destructive action, cleaning of all dependencies can
only happen by passing the ``--all`` command line option. It also works
accross all environments, unless ``--only`` is given.

Clean does not unlock the dependencies, unless ``--unlock`` is given.





Summary
-------

==================== =
:elixir:func:`run/1` Callback implementation of ```Mix.Task.run/1`` <Mix.Task.html#run/1>`__ 
==================== =





Functions
---------

.. elixir:function:: Mix.Tasks.Deps.Clean.run/1
   :sig: run(args)


   
   Callback implementation of ```Mix.Task.run/1`` <Mix.Task.html#run/1>`__.
   
   







