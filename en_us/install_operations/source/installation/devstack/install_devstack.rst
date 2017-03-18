.. _Installing the Open edX Developer stack:

########################################
Installing Open edX Devstack
########################################

This section describes how to install the Open edX developer stack (devstack).

.. contents::
   :local:
   :depth: 1

****************************************
Installation Prerequisites for Devstack
****************************************

Before you install devstack, make sure that you have met the
:ref:`installation prerequisites<Installation Prerequisites>`.

****************************************
**UPDATE**: On Ubuntu 16.04 
sudo apt-get update
sudo apt-get install nfs-kernel-server
****************************************

You must also ensure that you have the administrator password for your local
computer. The administrator password is needed to configure NFS (network file
system) to allow users to access code directories directly from your computer.

****************
Install Devstack
****************

To install devstack, follow these steps.

**UPDATE**: nfsd is the nfs client that comes with macOS. Ubuntu 16.04 has nfs-kernel-server which you installed before.

#. Ensure the ``nfsd`` client is running. You can use the ``nfsd status``
   command.

   .. code-block:: bash

     sudo nfsd status
     nfsd service is enabled
     nfsd is running (pid 313, 8 threads)

   If the nfsd service is not running, use the ``nfsd start`` command.

   .. code-block:: bash

     sudo nfsd start
     Starting the nfsd service
     
   **UPDATE**: If using Ubuntu 16.04 run:
   
   .. code-block:: bash
     sudo systemctl restart nfs-kernel-server

#. Create a ``devstack`` directory and navigate to it in the command prompt.

   .. code-block:: bash

     mkdir devstack
     cd devstack

#.  Set the ``OPENEDX_RELEASE`` environment variable to the Git tag name of the
    release of the Open edX platform that you are installing. For
    information about the latest Open edX releases and the Git tag names for
    them, see `Open edX Releases Wiki page`_.

    For example, ``open-release/ficus.1`` is the Git tag name for the
    first Eucalyptus release. The following command sets the value of the
    ``OPENEDX_RELEASE`` environment variable to ``open-release/ficus.1``.

    .. code-block:: bash

      export OPENEDX_RELEASE="open-release/ficus.1"

    If you do not set this environment variable, Vagrant will install the most
    recent snapshot version of the Open edX platform. The snapshot version is
    not a supported release.
    
    **UPDATE:** If you need to develop against master (like me for the grades calculation improvements), run:
    
    .. code-block:: bash

      export OPENEDX_RELEASE="master"

#. Download the install script.

   .. code-block:: bash

     curl -OL https://raw.github.com/edx/configuration/$OPENEDX_RELEASE/util/install/install_stack.sh

#. Run the install script to create and start the devstack virtual machine.

   .. code-block:: bash

     bash install_stack.sh devstack

   If you destroy and recreate the virtual machine, Vagrant reuses the box
   file and does not download it again. See `Vagrant's documentation on
   boxes`_ for more information.

   When prompted, enter the administrator password for your local computer.

When you have completed these steps, see :ref:`Starting the Open edX Developer
Stack` to begin using devstack.

For help with the devstack installation, see
:ref:`troubleshooting_devstack_installation`.


.. include:: ../../../../links/links.rst
