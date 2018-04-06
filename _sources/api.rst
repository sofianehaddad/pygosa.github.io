========================
Documentation of the API
========================

This section contains the `API` documentation. It regroups the description of the functions of the the `pygosa` library.


.. currentmodule:: pygosa

Experiment Design
=================

In the field of numerical evaluation of sensitivity features, one has in practice to:

  - Define a mutivariate distribution with **independent copula**;
  - Define a sampling method (`Monte-Carlo`, `LHS`, `Sobol-Sequence` and a "budget", ie size allowed for simulations. This last one should be fixed in accordance with model complexity
    (`CPU` time consuming, linearity/non linearity behaviour, input dimension, risk(s) of interest...);
  - Generate two independent input samples using the previous ingredients, says :math:`X_1` and :math:`X_2`;
  - Mix :math:`X_1` and :math:`X_2` to get a full sample :math:`X` used for sensitivity evaluations;
  -  Propagate through the model to get :math:`Y`;
  -  Keep/store both :math:`X` and :math:`Y`;
  -  Evaluate the feature importance, plot data/pie chart...;

As crude **Monte-Carlo** designs are implemented, if the input dimension is :math:`d` and :math:`N` is the "budget" size allowed, then the **full** :math:`X` sample is of size **:math:`N + d \times N \times N`**.
It is a major drawback.

However the benefit is that we could evaluate *several quantities of interest* once output model is computed (:math:`\alpha` -quantiles for various :math:`\alpha` in [0, 1], mean, moments,...)

The `SensitivityDesign` class helps to perform the six first steps described above (all except evaluation of features).
The *propagation step* (fifth step) could be done inside the module if the model is available (as `OpenTURNS.Function` ) or *outside* if model is for example a cluster-code.
For that purpose, the `Generate` method in `SensitivityDesign` class builds and returns the full :math:`X` sample.
Propagation is handled by user outside the platform. Finally both the :math:`X` and :math:`Y` (model output) are provided to the class.


.. autosummary::
    :toctree: _generated/
    :template: class.rst_t

    SensitivityDesign


Contrast
========

Once designs defined, the final objective is to evaluate sensitivity features associated to a quantity of interest (or risk).

.. autosummary::
    :toctree: _generated/
    :template: class.rst_t

    ContrastSensitivityAnalysis

Mean factors
============

.. autosummary::
    :toctree: _generated/
    :template: class.rst_t

    MeanSensitivities

Quantile factors
================

.. autosummary::
    :toctree: _generated/
    :template: class.rst_t

    QuantileSensitivities

Probability factors
===================

.. autosummary::
    :toctree: _generated/
    :template: class.rst_t

    ProbabilitySensitivities
