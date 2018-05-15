.. oTree VM Documentation documentation master file, created by
   sphinx-quickstart on Sun Apr 29 11:25:08 2018.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

oTree Production Server Setup
=============================

This documentation contains all the information neccessary to setup oTree on a fresh Debian 9 install.
The rough process is as follows:

* install required software
* setup an otree user and set privileges
* install Python 3.6.x from sources
* initialize the PostgreSQL database
* setup Git with post-receive hooks
* setup nginx as a reverse proxy

The individual chapters cover the steps in more detail. 

Contents
--------

.. toctree::
   :maxdepth: 2

   preparations.rst
   quick.rst
   step1.rst
   step2.rst
   step3.rst
   step4.rst
   step5.rst
   final.rst
   usage.rst

Indices
==================

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`
