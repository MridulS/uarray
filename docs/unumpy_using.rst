.. currentmodule:: unumpy

Using ``unumpy``
================

``unumpy`` is an in-progress mirror of the NumPy API which allows the user
to dynamically switch out the backend that is used. It also allows
auto-selection of the backend based on the arguments passed into a function.

Note that currently, coverage is very incomplete. However, we have attempted
to provide at least one of each kind of object in ``unumpy`` for
reference. There are :obj:`ufunc` s and :obj:`ndarray` s,  which are classes,
methods on :obj:`ufunc` such as :obj:`__call__ <ufunc.__call__>`, and
:obj:`reduce <ufunc.reduce>` and also functions such as :obj:`sum`.

The idea is that once things are more mature, it will be possible to switch
out your backend with a simple import statement switch:

.. code:: python

    import numpy as np  # Old method
    import unumpy as np  # Once this project is mature

Currently, only the following functions are supported:

* All NumPy `universal functions <https://www.numpy.org/devdocs/reference/ufuncs.html>`_.

  * `ufunc reductions <https://www.numpy.org/devdocs/reference/generated/numpy.ufunc.reduce.html#numpy.ufunc.reduce>`_

* ufunc-based reductions

  * `sum <https://docs.scipy.org/doc/numpy/reference/generated/numpy.sum.html>`_
  * `prod <https://docs.scipy.org/doc/numpy/reference/generated/numpy.prod.html>`_
  * `min <https://docs.scipy.org/doc/numpy/reference/generated/numpy.amin.html>`_
  * `max <https://docs.scipy.org/doc/numpy/reference/generated/numpy.amax.html>`_
  * `any <https://docs.scipy.org/doc/numpy/reference/generated/numpy.any.html>`_
  * `all <https://docs.scipy.org/doc/numpy/reference/generated/numpy.all.html>`_

You can use the :obj:`uarray.set_backend` decorator to set a backend and use the
desired backend. Note that not every backend supports every method. For example,
PyTorch does not have an exact :obj:`ufunc` equivalent, so we dispatch to actual
methods using a dictionary lookup. The following
backends are supported:

* :obj:`numpy_backend.NumPyBackend`
* :obj:`torch_backend.TorchBackend`
* :obj:`xnd_backend.XndBackend`

Alternatively, the backend will be automatically used based on the type of the input
arrays passed in.
