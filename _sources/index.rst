Welcome to PyGOSA's documentation!
==================================

:authors:
    Sofiane Haddad,
    Nabil Rachdi
:organization: IMACS / Airbus Group Innovations
:date: 2015-09-29
:Last update: 2018-01-29
:Funding: `Chorus Project <http://www.chorus-project.fr:5640/dokuwiki/doku.php>`_

The :mod:`pygosa` module (*Python Goal Oriented Sensitivity Analysis*) provides functions for the evaluation of sensitivity factors for some common risk functions/quantities of interest based on contrast functions.

With dedicated contrasts, the toolbox computes sensitivity factors associated to:

  - Mean: the factors are similar to the Sobol ones;
  - Probability: factors are to be compared with the FORM/SORM factors;
  - Quantiles: the factors are new;

As illustration, for the Ishigami use case, the figure illustrates the computed quantile factors for quantiles varying from 5% to 95%.

.. image:: ishigami_example.png
   :scale: 50 %
   :align: center

The module provides also the ability to implement easily new contrasts.

.. toctree::
    :maxdepth: 3

    install.rst
    methodology.rst
    examples.rst
    api.rst
    validation.rst
