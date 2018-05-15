.. _step3:

Step 3: Database and Supervisor
===============================

We now setup the PostgreSQL database and prepare a supervisor script which makes sure that the oTree web server is automatically started and restarted if if fails for any reason.

Quick Setup
^^^^^^^^^^^

Run as ``otree``::

	./3_setup_database.sh


Step by step instructions
^^^^^^^^^^^^^^^^^^^^^^^^^

PostgreSQL
""""""""""

We start by setting up the database and a database user for oTree::

	sudo -i -u postgres psql postgres -c "CREATE DATABASE django_db;"
	sudo -i -u postgres psql postgres -c "CREATE USER otree_user WITH PASSWORD 'CHANGE_THIS_PASSWORD_TO_YOUR_LIKING';"
	sudo -i -u postgres psql postgres -c "GRANT ALL PRIVILEGES ON DATABASE django_db TO $db_user;"

`Note:` You can use ``tr -cd '[:alnum:]' < /dev/urandom | fold -w30 | head -n1`` to quickly generate a random 30 character password from the command line.


Supervisor
""""""""""

We need to make sure that the oTree web server is started on system boot. It should also automatically restart, if it fails for any reason. To do so, we setup a supervisor script::

	sudo nano /etc/supervisor/condf.d/otree.conf

Include the following lines:: 

	[program:otree]
	command=/home/otree/venv_otree/bin/otree runprodserver 8000
	directory=/home/otree/oTree
	stdout_logfile=/home/otree/otree-supervisor.log
	stderr_logfile=/home/otree/otree-supervisor-errors.log
	autostart=true
	autorestart=true
	environment=
	    PATH="/home/otree/venv_otree/bin/:%(ENV_PATH)s",
	    DATABASE_URL="postgres://otree_user:YOUR_DATABASE_PASSWORD@localhost/django_db",
	    OTREE_ADMIN_PASSWORD="YOUR_WEBINTERFACE_ADMIN_PASSWORD",
	    OTREE_PRODUCTION=1,
	    OTREE_AUTH_LEVEL=STUDY,

Make sure to replace ``YOUR_DATABASE_PASSWORD`` with the one you set above. Also come up with a password for the oTree web interface and replace ``YOUR_WEBINTERFACE_ADMIN_PASSWORD`` accordingly. Finally, save the file and exit nano with [ctrl] + [s] and [ctrl] + [x].


Environment Variables
"""""""""""""""""""""

Finally, we want ``otree`` to be able to manually reset the database and invoke other oTree commands. We need to make sure that the credentials are available as environment variables whenever ``otree`` logs in.

Edit ``/home/otree/.otree_env`` with nano::

	nano /home/otree/.otree_env

Add the following lines to the end::

	export DATABASE_URL="postgres://otree_user:YOUR_DATABASE_PASSWORD@localhost/django_db"
	export OTREE_ADMIN_PASSWORD="YOUR_WEBINTERFACE_ADMIN_PASSWORD"
	export OTREE_PRODUCTION=1
	export OTREE_AUTH_LEVEL=STUDY

Again, make sure to replace ``YOUR_DATABASE_PASSWORD`` with the one you set above. Also come up with a password for the oTree web interface and replace ``YOUR_WEBINTERFACE_ADMIN_PASSWORD`` accordingly. Finally, save the file and exit nano with [ctrl] + [s] and [ctrl] + [x].

Continue with step 4.