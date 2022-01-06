.. _step2:

Step 2: Python 3.9
==================

The Ubuntu 20.04 stable branch includes Python up to version 3.6. While oTree runs on this version, there are some bugs related to the presentation of the monitoring table. Columns appear to be scrambled. To avoid this, we install Python 3.9 from sources.


Get Python 3.9
""""""""""""""

Log in as ``otree`` and navigate to your home directory. Download and unpack Python 3.9 (any point release is fine, change the following commands accordingly)::

	cd ~
	wget https://www.python.org/ftp/python/3.9.9/Python-3.9.9.tgz
	tar  zxvf Python-3.9.9.tgz
	rm Python-3.9.9.tgz

Configuration and building
"""""""""""""""""""""""""""

Change working directory, then configure and make Python 3.9::

	cd Python-3.9.9
	./configure --with-ensurepip=install --enable-optimizations 
	make -j8

This might take a while. Time to get some coffee.

Installation
""""""""""""

By default ``python`` points to ``python2.7``. We will add python 3.9 as an alternative, but give the old association highest priority. We will have to use ``python3.9`` explicitly (rather than just ``python`` or ``python3``), but at least we are not breaking anything.

.. code-block:: bash

	sudo make altinstall
	sudo update-alternatives --install /usr/bin/python python /usr/local/bin/python3.9 40

Leave and remove working directory::

	cd ..
	sudo rm -rf Python3.9.9

Virtual environment
"""""""""""""""""""

OTree  will run in its own virtual environment. This allows us to keep it separate from the system Python installation and avoids dependency clutter. We will create an initial virtual environment::

	python3.9 -m venv venv_otree
	source venv_otree/bin/activate

Finally, we make sure that the oTree virtual environment is automatically activated whenever ``otree`` logs in::

	echo "source /home/otree/venv_otree/bin/activate" >>/home/otree/.otree_env
	echo "source /home/otree/.otree_env" >> /home/otree/.bashrc

This complete the second step.