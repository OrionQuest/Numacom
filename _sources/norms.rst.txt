Norms
-----

Norms are valuable tools for arguing about the extent and magnitude of error. We
introduce some concepts that we will broadly use later on:

.. topic:: Definition

    A *vector norm* is a function from :math:`\mathbb R^n` to
    :math:`\mathbb R`. If :math:`x\in\mathbb R^n`,
    we symbolize its norm by :math:`\lVert x\rVert`, and its defining properties are:
    
    #. :math:`\lVert x\rVert\geq 0` for all :math:`x\in\mathbb R^n`, also :math:`\lVert x\rVert=0`
       if and only if :math:`x=0`.
    #. :math:`\lVert \alpha x\rVert = \lvert\alpha\rvert\cdot \lVert x\rVert` for
       all :math:`\alpha\in\mathbb R,x\in\mathbb R^n`.
    #. :math:`\lVert x+y\rVert\leq \lVert x\rVert + \lVert y\rVert` for all
       :math:`x,y\in\mathbb R^n`.

Note that the properties above do not determine a *unique* form of a "norm"
function. In fact, many different valid norms exist. Typically, we will use
subscripts (for example, :math:`\lVert \cdot\rVert_a`) to denote different types
of norms.

Why are vector norms needed?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In many applications, such as the solution of a nonlinear equation :math:`f(x)=0`,
the error :math:`e=x_\textsf{approx}-x_\textsf{exact}` is a single number. Thus,
the absolute value of :math:`\vert e\vert` gives us a good idea of the "extent"
of the error.

When solving a system of linear equations :math:`Ax=b`, the exact solution
:math:`x_\textsf{exact}` as well as any approximation :math:`x_\textsf{approx}`
are vectors, and the error :math:`e=x_\textsf{approx}-x_\textsf{exact}` is a
vector too. It is not as straightforward to assess the "magnitude" of such a
vector-valued error. For example, consider :math:`e_1,e_2\in\mathbb R^{1000}`,
and

.. math::
    e_1=\left(\begin{array}{c}
    0.1 \\
    0.1 \\
    0.1 \\
    \vdots \\
    0.1
    \end{array}\right), \enspace\enspace\enspace e_2 = \left(\begin{array}{c}
    100 \\
    0 \\
    0 \\
    \vdots \\
    0
    \end{array}\right)

Which one is worse? While :math:`e_1` has a modest amount of error uniformly
distributed over all components, all components of :math:`e_2` are exact, but
one of them has a huge discrepancy! Exactly how we quantify and assess the
extent of error is application-dependent. Vectors norms are alternative ways to
measure this magnitude, and different norms would be appropriate for different
tasks.

Types of Vector Norms
~~~~~~~~~~~~~~~~~~~~~

Consider a vector :math:`v\in\mathbb R^n`. Some norms which satisfy the
properties of vector norms are:

1. The :math:`L_1`-norm (or :math:`1`-norm):

.. math::
    \lVert v\rVert_1         = \sum_{i=1}^n \vert v_i\vert

2. The :math:`L_2`-norm (or :math:`2`-norm, or Euclidean norm)

.. math::
    \lVert v\rVert_2 = \sqrt{\sum_{i=1}^n v_i^2}

3. The infinity norm (or max-norm)

.. math::
    \lVert v\rVert_\infty    = \enspace \max_{1\leq i\leq n}\vert v_i\vert

4. (Less common) :math:`L_p`-norm

.. math::
    \lVert v\rVert_p = \left(\sum_{i=1}^n \vert v_i\vert^p\right)^{1/p}

`NumPy <http://www.numpy.org/>`_ has a package called ``linalg`` that allows us
to directly compute all these different kinds of norms for a given vector, as shown below.
Here, the second parameter specifies the particular norm that we wish to compute
(in our case, the :math:`L_1` norm, :math:`L_2` norm, or :math:`L_\infty` norm, respectively): ::

    >>> v = v = np.array([3,1,4,5,2,7])
    >>> np.linalg.norm(v,1)
    22
    >>> np.linalg.norm(v,2)
    10.198039027185569
    >>> np.linalg.norm(v,np.inf)
    7
