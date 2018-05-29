.. _usage:

Experimenter Usage
==================

The server should now be set up completely. To get an experiment running, experimenters can add the server as a remote to their local git repository and then push their version to the remote repository.

Git Setup on experimenter's computer
""""""""""""""""""""""""""""""""""""

*If the experimenter is already using Git as their version control system, you can skip this step.*

First, install Git from `<https://git-scm.com/downloads>`_.

Then, navigate to your oTree project folder and initialize the git repository. You only need to do this once for each oTree project folder::
    
    git init


They will also have to configure their username and e-mail address::

    git config --global user.name "your name"
    git config --global user.email "test@exam"


Setting up the remote repository
""""""""""""""""""""""""""""""""

To add the oTree server as a remote invoke the following command from your oTree project / local git repository directory::

    git remote add production ssh://otree@SERVER_URL/home/otree/oTree.git

Make sure to replace ``SERVER_URL`` with the URL the server is accessible from. 


Pushing to production
"""""""""""""""""""""

When the experiment is ready to go live, experimenters can use the typical workflow of first staging and then commiting their changes before finally pushing them to production::

    git add . 
    git commit -am "your commit message here"
    git push production master

Users will have to know and enter the password for the ``otree`` user account.
A few moments later oTree's web interface should be available from any browser pointed to the server's URL.


A note of caution
"""""""""""""""""

If the experimenter does not setup their oTree project to include `database migrations <http://otree.readthedocs.io/en/latest/server/next_steps.html#modifying-an-existing-database>`_ the database will be reset after each push. **This means that data currently stored in the database will be erased.**