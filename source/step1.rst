.. _step1:

Step 1: Software, Users and Privileges
======================================

This step requires the installation scripts to be downloaded and currently being logged in as ``root``. 
Read :ref:`preparations` if this is not the case.

Quick Setup
^^^^^^^^^^^

Run as ``root``::

	./setup_otree_server.sh

Then follow the instructions.


Step by step instructions
^^^^^^^^^^^^^^^^^^^^^^^^^

`Note:` This is the long and extensively documented version of what the Quick Start script above accomplishes. If you have run the command above and did not encounter any errors, you may advance to step 2.

Software
""""""""

First we install the neccessary software using Debian's package manager::

	apt-get update
	apt-get install -y libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm zlib1g-dev libssl-dev libncurses5-dev libncursesw5-dev xz-utils tk-dev postgresql postgresql-contrib redis-server git supervisor nginx sudo
 
This includes:

* `PostgreSQL Database <https://www.postgresql.org/>`_
* `Redis Datastore <https://redis.io/>`_
* `Git Version Control System <https://git-scm.com/>`_
* `Nginx HTTP and reverse proxy server <https://nginx.org/>`_
* `Supervisor Process Control System <http://supervisord.org/>`_
* `Sudo <https://www.sudo.ws/>`_


User and privileges
"""""""""""""""""""

Typically, you do not want to work as ``root``. Accordingly, we will setup a user ``otree`` and allow this user to run specific commands as ``root`` through ``sudo``::
	
	adduser otree
	adduser otree sudo

This creates the user ``otree`` and adds him to the sudo group which allows him to run arbitrary commands as ``root``. This is just for the setup. We will remove ``otree`` from the sudo group at the end of the installation. In the end, we want ``otree`` to only be able to run specific commands which are needed to control the supervisor daemon. We will now prepare the sudoers file accordingly::

	nano /etc/sudoers.d/otree_supervisor

Copy in the following lines::
	
	# allow otree user to start, stop and restart supervisor
	otree ALL=NOPASSWD:/usr/sbin/service supervisor start
	otree ALL=NOPASSWD:/usr/sbin/service supervisor stop
	otree ALL=NOPASSWD:/usr/sbin/service supervisor restart

Save and exit nano with [ctrl] + [s] and [ctrl] + [x].

The three lines grant ``otree`` the right to start, stop, and restart supervisor. There will be more information on supervisor in a later installation step.


Prepare userspace installation
""""""""""""""""""""""""""""""

Now it is time to continue the installation from the userspace. Before we can do so, however, we need to copy over the installation scripts to ``otree``'s home directory::

	mv *.sh /home/otree/
	chmod +x /home/otree/*.sh 
	chown otree:otree /home/otree/*.sh

Continue with step 2.