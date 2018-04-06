========================
Reference guide document
========================

This section contains the reference guide, which is the theoretical documentation.

Context
=======

From more than one decade, uncertainty propagation and sensitivity analysis are widely used to handle mathematical models of industrial problems involving many parameters or variables: geophysics and oil reservoir, safety in
nuclear industry, soil pollution, and more generally domains where it can be found heavy computation codes with large number of inputs and complex computations so that only few simulations of these codes can be run.

The uncertainty propagation methodology uses random variables as inputs, even for deterministic codes, and study the distribution (or some characteristics) of the output. It is justified on the one hand by the poor knowledge
of the input parameter (or variables), and on the other hand by the relatively small number of observed output available.

Very often, some of the input variables strongly affect the output (or a characteristic), while others have a small effect (and even no effect). The sensitivity analysis try to quantify these effects.

The module presents new indicators.


Contrast (or loss function) definition
======================================

Let us set :math:`\Theta` be some generic set and :math:`Q` be some probability measure on a space :math:`\mathcal{Y}`.
A (:math:`\Theta, Q`)-**contrast function**, or simply **contrast function**, is defined as any function :math:`\psi`:

.. math::

  \psi : \Theta & \longrightarrow  L_{1}(Q)

  \theta & \longmapsto \psi(\cdot, \theta)  :  y\in\mathcal{Y} \longmapsto \Psi(\rho,y)

such that


.. math::

  \theta^{*} = \underset{\theta \in \Theta}{argmin\ } \mathbb{E}_{Y \sim Q} \psi(Y; \theta)


is *unique*. The function :math:`\Psi  : \theta \mapsto \mathbb{E}_{Y \sim Q}\, \psi(Y; \theta)` is the **average contrast function**, or abusively contrast function if there is no ambiguity.


The contrast function is a very useful object in *Statistical Learning Theory* where it defines estimation procedures of some feature :math:`\theta^{*} \in \Theta` (scalar or functional) associated to a random variable :math:`Y`.

For instance, when observing a :math:`n`-sample :math:`(Y_1,\ldots,Y_n)` of the random variable :math:`Y`, an estimator of :math:`\theta^{*}` is given by :math:`\widehat\theta=\mbox{Argmin}_{\theta} \Psi_n(\theta)`, where :math:`\Psi_n` is obtained by substituting the expectation :math:`w.r.t.` the variable :math:`Y` by the expectation :math:`w.r.t.` the empirical measure of the sample. It reads:

.. math::

   \Psi_n(\theta)=\frac{1}{n}\sum_{i=1}^n \psi(Y_i;\theta).


Then, considering for example the following contrast function

.. math::

    \psi : (y; \theta)\mapsto (y - \theta)^2

provides the well known estimation procedure of the mean

.. math::

  \widehat\theta= \underset{\theta}{argmin\ } \frac{1}{n}\sum_{i=1}^n (Y_i - \theta)^2

That gives obviously

.. math::

   \widehat\theta = \frac{1}{n}\sum_{i=1}^n Y_i

The same stands for "functional" features associated to the random variable :math:`Y` (density function, etc.).

Feature characterization by contrast
------------------------------------

The previous writing provides a characterization of a feature :math:`\theta^*` of :math:`Y` by a contrast :math:`\psi`. Notice that it may exist various contrasts :math:`\psi` characterizing :math:`\theta^*`.

The previous remark comes from the PhD work of N. Rachdi.

Some usual contrasts
--------------------

Let us give an non exhaustive list of contrasts that allow to estimate various parameters associated to a probability distribution. We give the classical contrasts associated to each parameter.


  -  Central parameters:

    - The mean :  :math:`\Psi(\theta)=\mathbb E |Y-\theta|^2`.
    - The median (in :math:`\mathbb R`) : :math:`\Psi(\theta)=\frac{1}{2}\mathbb E|Y-\theta|`.

  - An excess probability : :math:`\Psi(\theta)=\mathbb E |{\bf1}_{Y\ge t}-\theta|^2`.
  - All the probability tail: :math:`\Psi(\theta)=\int_{t_0}^\infty \mathbb E |{\bf1}_{Y\ge t}-\theta(t)|^2 dt`.
  - The :math:`\alpha`-quantile : :math:`\Psi(\theta)=\mathbb E (Y-\theta)(\alpha -{\bf1}_{Y\le\theta})`.
  - All the quantile "tail": :math:`\Psi(\theta)=\int_{\alpha_0}^1 \mathbb E (Y-\theta(\alpha))(\alpha -{\bf1}_{Y\le\theta(\alpha)})d\alpha`.
  - The probability density function, which is an infinite dimensional parameter.

    - Using the kernel method with a given kernel `K` and a window size `r>0`, we set :math:`K_r(Y)=\frac{1}{r}K(\frac{Y}{r})` and the contrast is:

      .. math:: \Psi(\theta)=\mathbb E \int_{-\infty}^{+\infty}(K_r(Y-t)-\theta(t))^2dt.

      In fact it is an unbiased estimator of the convolution of the *p.d.f* with `K_r`, which is the target "parameter".
    - Using an orthonormal :math:`\mathbb L^2` basis :math:`(\varphi_j,j\ge 0)` truncated at the order~ :math:`N` :

      .. math:: \Psi(\theta)=\mathbb E \sum_{j=0}^N (\varphi_j(Y)-\int_{-\infty}^{+\infty} \varphi_j(u)\theta(u) du)^2.

      What is really estimated here, is the orthogonal projection of the *p.d.f* on the truncated basis, which is the target "parameter".

Most of these contrasts are of quadratic type, contrary to the contrasts associated to the quantiles.


Sensitivity with respect to a contrast
======================================

We are interested in the sensitivity of a scalar output :math:`Y` to an input variable :math:`X_k`, we assume that :math:`Y` is a function of some input variables:

.. math::

  Y=h(X_1,\ldots,X_d)=h({\bf X})

Generally :math:`h` is a "black box", in the sense that :math:`h` is not explicit but results from heavy computer code, complex mathematical (or statistical) models.
For sake of simplicity let us consider a scalar output :math:`Y` but the method can easily be extended to a multiple output :math:`Y\in \mathbb{R}^q`


We assume that :math:`\Psi` is a contrast associated to a "parameter" :math:`\theta^*` where :math:`\theta^* =\mbox{Argmin} \Psi(\theta)`.
Moreover :math:`\Psi` writes :math:`\Psi(\theta)=\mathbb E\psi(Y;\theta)`


Let :math:`\Psi(\theta)=\mathbb E\psi(Y;\theta)` be a contrast. The contrast variation due to :math:`X_k` is defined as :

.. math::

  V_k= \min_\theta \Psi(\theta)-\mathbb E( \min_\theta \mathbb E(\psi(Y;\theta)|X_k))

and we have :math:`V_k \geq 0`. We can also write :math:`V_k` as follows

.. math::

    V_k =  \mathbb{E}_{(X_k,Y)}\left(\psi(Y;\theta^*)  - \psi(Y;\theta_k(X_k))\right) \label{contrast_var}

where :math:`\theta^* = \displaystyle{\\argmin_{\theta} \Psi(\theta)}` and :math:`\theta_k(x) = \displaystyle{\\argmin_{\theta} \mathbb E(\psi(Y;\theta)|X_k = x)}`


Notice that the inequality

.. math::

   \mathbb E(\min_\theta \mathbb E(\psi(Y;\theta)|X_k))\le \min_\theta \mathbb E(\mathbb E(\psi(Y;\theta)|X_k))= \Psi(\theta)

implies that :math:`V_k` is non negative.

Moreover, let us remark that if :math:`Y` does not depend on :math:`X_k`, :math:`V_k` is *0* and conversely if :math:`Y=h(X_k)` then :math:`V_k` is maximum.

We make the following assumption:

.. math::
   :label: assumption

    \mathbb E \min_{\theta}\psi(Y;\theta)\in  \mathbb R

Notice that all the contrasts identified satisfy :eq:`assumption` since :math:`\min_{\theta}\psi(Y;\theta)=0`.

Now we are in position to define a new index generalizing the Sobol one based on contrasts that satisfy :eq:`assumption` .

:math:`\boldsymbol{\psi}` -**Indices**: assume that a contrast :math:`\Psi(\theta)=\mathbb E\psi(Y;\theta)` satisfies the first assumption. The  :math:`\psi` -index of the variable :math:`Y=h(X_1,\ldots,X_d)` with respect to the contrast :math:`\Psi` and the variable :math:`X_k` is defined as:

.. math::

   S^k_{\psi}=\frac{V_k}{ \min_\theta \Psi(\theta)-\mathbb E \min_{\theta}\psi(Y;\theta)}

or

.. math::

   S^k_{\psi}= \frac{\mathbb{E}_{(X_k,Y)}\left(\psi(Y;\theta^*)  - \psi(Y;\theta_k(X_k))\right)}{ \min_\theta \Psi(\theta)-\mathbb E \min_{\theta}\psi(Y;\theta)}. \label{def_psi_indice}

Note that these indices could be extended to higher order.
