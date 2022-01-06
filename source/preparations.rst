.. _preparations:

Preparations
============

It is assumed that ``root`` can login to a standard shell.
Furthermore, it is assumed that the server is reachable via SSH.
If it is not, install openssh-server as ``root``:

.. code-block:: bash

	apt update
	apt install openssh-server

The following steps will reference installation scripts. These need to be downloaded, extracted and made executable.
As ``root`` run::

	wget https://github.com/guangtengmeng/otree_setup_scripts/archive/master.zip
	unzip master.zip
	cd otree_setup_scripts-master
	chmod +x setup_otree_server.sh

You are now ready for the first step of the installation.