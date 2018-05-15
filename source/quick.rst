.. _quick:

Quick Setup
==================

**Read** :ref:`preparations` **first!**

Basic setup as root
^^^^^^^^^^^^^^^^^^^

Run as ``root``::

    ./setup_otree_server.sh

Enter passwords along the way.
After the script finishes, you have two options: You can continue the installation with or without setting up SSL certificates.

Userspace setup without SSL
^^^^^^^^^^^^^^^^^^^^^^^^^^^

Run as ``otree``::

    ./1_continue_setup.sh

This will automatically execute the following scripts one after the other::

    ./2_install_python.sh
    ./3_setup_database.sh
    ./4_setup_git.sh
    ./5_setup_nginx.sh

Finally it will remove ``otree`` from the sudo group.


Userspace setup with SSL
^^^^^^^^^^^^^^^^^^^^^^^^

Run as ``otree``::

    ./1_continue_setup_ssl.sh

This will automatically execute the following scripts one after the other::

    ./2_install_python.sh
    ./3_setup_database.sh
    ./4_setup_git.sh
    ./5_setup_nginx_ssl.sh

Finally it will remove ``otree`` from the sudo group.