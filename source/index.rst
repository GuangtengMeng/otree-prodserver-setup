.. oTree VM Documentation documentation master file, created by
   sphinx-quickstart on Tue Jan 6 10:07:14 2022.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

oTree Production Server Setup
=============================

This documentation contains all the information neccessary to setup oTree on a fresh Ubuntu 20.04 install.
The rough process is as follows:

* install required software
* setup an otree user and set privileges
* install Python 3.9.9 from sources
* initialize the PostgreSQL database
* setup Git with post-receive hooks
* setup nginx as a reverse proxy

The individual chapters cover the steps in more detail. 

Contents
--------

.. toctree::
   :maxdepth: 2

   about
   preparations.rst
   quick.rst
   detailed/index
   usage.rst

Indices
==================

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`
