Frontenac cluster
=================

Tips and tricks for the `Frontenac CAC cluster <https://cac.queensu.ca>`_

Read through the CAC wiki for a primer on logging in and submitting batch jobs. 

.. lmod:

Lmod Module System
------------------
The environment module system used by Frontenac is
`Lmod <https://lmod.readthedocs.io/>`_. You use the command ``module`` to interact
with it. To load a module you use ``module load``, unload with
``module unload``, search for modules with ``module spider``, and see loaded
modules with ``module list``.

.. tip::

   For further info, use ``module --help`` to see other functions of Lmod. 

.. mesa:

Running MESA
------------
`MESA <https://docs.mesastar.org/en/release-r22.11.1/>`_ requires its own SDK to clobber default compilers. To get this to work on Compute Canada systems, including Frontenac, you need to invoke

.. code-block:: bash

   module force purge

Before any attempt to compile or run MESA. This directive should also be included in your bash script when submitting a slurm job. 

.. group directory:

Our Shared Group Directory
--------------------------
In addition to your user directory on the cluster, our group ``hpcg1719`` has a
shared directory found at:

.. code-block:: bash

   /global/project/hpcg1719

Here you can share files with the group without needing to
`secure copy <https://man7.org/linux/man-pages/man1/scp.1.html>`_ (``scp``) the
files to your computer and send it to someone else on the team.

In addition, you can create a
`symbolic link <https://en.wikipedia.org/wiki/Symbolic_link>`_ to our group
directory to quickly ``cd`` into it from your home directory using the
`link command <https://man7.org/linux/man-pages/man1/ln.1.html>`_ (``ln``):

.. code-block:: bash

   ln --symbolic /global/project/hpcg1719 ~/group-folder

which creates a symbolic link to our group's shared folder called
*group-folder* in your user home directory.
This can be removed by using ``unlink`` or the regular ``rm`` command:

.. code-block:: bash

   unlink ~/group-folder

.. code-block:: bash

   rm ~/group-folder

.. note::
   There is no trailing forward slash, as we are removing the link, not the
   directory it points at.


In the shared group directory there are a few test job scripts in
``Documents/Tests``. You can run them to test your account's job submissions,
or copy them and use them as a base for your own job scripts.

Compilers
---------

Fortran
*******

For Fortran you'll typically use the GNU compiler `gfortran`, which can be found
in the `StdEnv` module (loaded by default). If you want to use the *Intel*
Fortran compiler you have to load the legacy (Frontenac doesn't have modern
licences for `ifort`) module `ics`.

.. code:: bash

   module load ics
