.. _usage:

Experimenter Usage
==================

The server should now be set up completely. To get an experiment running, experimenters can add the server as a remote to their local git repository and then push their version to the remote repository.


Setting up the remote repository
""""""""""""""""""""""""""""""""

To add the oTree server as a remote invoke the following command from your oTree project / local git repository directory::

    git remote add production ssh://otree@SERVER_URL/home/otree/oTree.git

Make sure to replace ``SERVER_URL`` with the URL the server is accessible from. 


Pushing to production
"""""""""""""""""""""

When the experiment is ready to go live, they can simply push it to production::

    git push production master

Users will have to know and enter the password for the ``otree`` user account.
A few moments later oTree's web interface should be available from any browser pointed to the server's URL.

A note of caution
"""""""""""""""""

If the experimenter does not setup their oTree project to include `database migrations <http://otree.readthedocs.io/en/latest/server/next_steps.html#modifying-an-existing-database>`_ the database will be reset after each push. **This means that data currently stored in the database will be erased.**