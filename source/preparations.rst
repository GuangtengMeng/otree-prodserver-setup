.. _preparations:

Preparations
============

It is assumed that ``root`` can login to a standard shell.
Furthermore, it is assumed that the server is reachable via SSH.
If it is not, install openssh-server as ``root``:

.. code-block:: bash

	apt-get update
	apt-get install openssh-server

The following steps will reference installation scripts. These need to be downloaded, extracted and made executable.
As ``root`` run::

	wget http://ckgk.de/otree_vm_setup.zip
	unzip otree_vm_setup.zip
	chmod +x setup_otree_server.sh

You are now ready for the first step of the installation.