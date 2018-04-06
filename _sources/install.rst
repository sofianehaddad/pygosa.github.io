.. _install:

======
Get it
======


Dependencies
============

Python2 >= 2.7:

- :mod:`numpy` >= 1.8

- :mod:`matplotlib` >= 1.4

- :mod:`openturns` >= 1.9. `See here <http://openturns.github.io/openturns/master/install.html>`_ for more details.

- :mod:`pandas`

For documentation:

- :mod:`sphinx` >= 1.1

Build from source
=================

Get source::

    $ git clone https://www.github.com/sofianehaddad/pygosa.git

Install::

    $ python setup.py install

If you need to install the module in the user folder :

.. code-block:: shell

    $ python setup.py install --user

Finally to build the documentation, you should invoke the `build_sphinx` option :

.. code-block:: shell

    $ python setup.py build_sphinx

