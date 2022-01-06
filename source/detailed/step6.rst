.. _final:

Step 6: Final
=============

The final step is to lock down the ``otree`` user account. Throughout the installation, it had full sudo privileges. To remove them invoke::

    sudo deluser otree sudo

This removes ``otree`` from the sudo group.
The group change only takes effect after logging out and in again.

