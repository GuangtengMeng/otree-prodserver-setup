.. _step4:

Step 4: Git Repository
======================

We now set up the Git repository and a specific post-receive script that makes it easy for experimenters to deploy experiments on the server.

Quick Setup
^^^^^^^^^^^

Run as ``otree``::

	./4_setup_git.sh


Step by step instructions
^^^^^^^^^^^^^^^^^^^^^^^^^

Directories
"""""""""""

First we will create two directories: ``oTree`` will contain the live oTree project. ``oTree.git`` will be the repository that experimenters can push their experiments to. After creating the directories, we initialize an empty Git repository in the latter.

.. code-block:: bash

    mkdir /home/otree/oTree 
    mkdir /home/otree/oTree.git
    cd /home/otree/oTree.git
    git init --bare
    cd ~


Post-Receive Script
"""""""""""""""""""

Experimenters can push their oTree experiments to the Git repository we have just created. Now we set up a script that is executed after every push to the repository. It will take care of the following steps:

* wipe the current virtual environment
* re-create the virtual environment
* install current versions of all required packages
* attempt to migrate the existing database if migrations are specified by the experimenter
* reset the database in all other cases
* restart the web server

Edit ``oTree.git/hooks/post-receive`` with nano::
    
    nano /home/otree/oTree.git/hooks/post-receive

Add the following script::

    #!/bin/bash
    GIT_WORK_TREE="/home/otree/oTree"
    VENV_DIR="/home/otree/venv_otree"
    export GIT_WORK_TREE
    git checkout -f

    if [[ -d "$VENV_DIR" ]]; then
        echo "[log] - Cleaning virtualenv"
        rm -rf $VENV_DIR
        echo "[log] - Finished creating virtualenv"
    fi

    # recreate venv
    echo "[log] - create venv"
    python3.6 -m venv $VENV_DIR

    # activate
    echo "[log] - activate venv"
    echo $VENV_DIR
    source $VENV_DIR/bin/activate
    source /home/otree/.otree_env

    # install requirements
    echo "[log] - install requirements"
    pip install -U pip
    pip install -r $GIT_WORK_TREE/requirements.txt

    echo "[log] - Staring DB migration"
    cd $GIT_WORK_TREE
    if [[ -d "$GIT_WORK_TREE/otree_core_migrations" ]]
        then
            echo "[log] - detected migrations in otree project dir"
            echo "[log] - attempting migrations"
            otree migrate
            echo "[log] - migrations done"
        else
            echo "[log] - no migrations defined"
            echo "[log] - resetting db"
            otree resetdb --noinput
            echo "[log] - database reset"
    fi

    cd ..
    echo "[log] - Finished DB migration "

    echo "[log] - restart services"
    sudo /usr/sbin/service supervisor restart


Finally, we make the script executable::

    chmod +x /home/otree/oTree.git/hooks/post-receive

Continue with step 5.