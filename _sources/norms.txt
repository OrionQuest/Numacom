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

Matrix Norms
~~~~~~~~~~~~

We can actually define norms for (square) matrices as well.

.. topic:: Definition

    A matrix norm is a function :math:`\lVert\cdot\rVert : \mathbb R^{n\times n}\rightarrow \mathbb R` that satisfies:

    1. :math:`\lVert M\rVert\geq 0` for all :math:`M\in\mathbb R^{n\times n}`, :math:`\lVert M\rVert = 0`
       if and only if :math:`M=O`.
    2. :math:`\lVert \alpha M\rVert = \vert\alpha\vert\cdot\lVert M\rVert`
    3. :math:`\lVert M+N\rVert\leq \lVert M\rVert + \lVert N\rVert`
    4. :math:`\lVert M\cdot N\rVert \leq \lVert M\rVert\cdot\lVert N\rVert`

Property :math:`(4)` above has slightly different flavor than vector
norms. Although more types of matrix norms exist, one common category is that of
matrix norms *induced by* vector norms.

.. topic:: Definition

    If :math:`\lVert\cdot\rVert_\star` is a valid vactor norm, its
    *induced* matrix norm is defined as:

    .. math::
        \lVert M\rVert_\star = \max_{x\in\mathbb R^n,x\neq 0} \frac{\lVert Mx\rVert_\star}{\lVert x\rVert_\star}

    or equivalently,

    .. math::
        \lVert M\rVert_\star = \max_{x\in\mathbb R^n,\lVert x\rVert=1} \lVert Mx\rVert_\star

Note again, that *not all* valid matrix norms are induced by vector norms. One
notable example is the very commonly used *Frobenius norm*:

.. math::
    \lVert M\rVert_F = \sqrt{\sum_{i,j=1}^n M_{ij}^2}

We can easily show that induced norms satify properties :math:`(1)` through
:math:`(4)`. Properties :math:`(1)-(3)` are rather trivial, for example,

.. math::
    \lVert M+N\rVert &=& \max_{x\neq 0} \frac{\lVert (M+N)x\rVert}{\lVert x\rVert} \leq \max_{x\neq 0} \frac{\lVert Mx\rVert + \lVert Nx\rVert}{\lVert x\rVert} \\
                     &=& \max_{x\neq 0} \frac{\lVert Mx\rVert}{\lVert x\rVert} + \max_{x\neq 0} \frac{\lVert Nx\rVert}{\lVert x\rVert} = \lVert M\rVert + \lVert N\rVert

Property :math:`(4)` is slightly trickier to show. First, a lemma:

.. topic:: Lemma

    If :math:`\lVert\cdot\rVert` is a matrix norm induced by a vector
    norm :math:`\lVert\cdot\rVert`, then

    .. math::
        \lVert Ax\rVert \leq \lVert A\rVert\cdot \lVert x\rVert
        :label: vector-norm-inequality

    *Proof:* Since :math:`\lVert A\rVert = \max_{x\neq 0}\lVert Ax\rVert/\lVert x\rVert`, we have that for an arbitrary :math:`y\in\mathbb R^n (y\neq 0)`

    .. math::
        \lVert A\rVert = \max_{x\neq 0}\frac{\lVert Ax\rVert}{\lVert x\rVert}\geq \frac{\lVert Ay\rVert}{\lVert y\rVert} \Rightarrow \lVert Ay\rVert \leq \lVert A\rVert\cdot\lVert y\rVert

    This holds for :math:`y\neq 0`, but we can see that it is also true for :math:`y=0`.

Now property :math:`(4)` can be easily proved using the above lemma:

.. math::
    \lVert MN\rVert &=& \max_{\lVert x\rVert=1} \lVert MNx\rVert \leq \max_{\lVert x\rVert=1} \lVert M\rVert\cdot \lVert Nx\rVert \\
                    &=& \lVert M\rVert\cdot \max_{\lVert x\rVert=1} \lVert Nx\rVert = \lVert M\rVert\cdot\lVert N\rVert \\
    \Rightarrow \lVert MN\rVert &\leq& \lVert M\rVert\cdot\lVert N\rVert

Note that when writing an expression such as :eq:`vector-norm-inequality`, the
matrix norm :math:`\lVert A\rVert` is understood to be the inferred norm from the
vector norm used in :math:`\lVert Ax\rVert` and :math:`\lVert x\rVert`. Thus,

.. math::
    \lVert Ax\rVert_1 \leq \lVert A\rVert_1\cdot \lVert x\rVert_1

and

.. math::
    \lVert Ax\rVert_\infty \leq \lVert A\rVert_\infty\cdot \lVert x\rVert_\infty

are both valid, but we *cannot* mix and match, for example:

.. math::
    \lVert Ax\rVert_\infty \leq \lVert A\rVert_2\cdot \lVert x\rVert_1

Although the definition of an induced norm allowed us to prove certain
properties, it does not necessarily provide a convenient formula for evaluating
the matrix norm. Fortunately, such formulas do exist for the :math:`L_1` and
:math:`L_\infty` induced matrix norms. Given here (without proof):

.. math::
    \lVert A\rVert_1        &=& \max_j \sum_{i=1}^n \vert A_{ij}\vert \enspace\enspace\enspace\mbox{(maximum absolute column sum)} \\
    \lVert A\rVert_\infty   &=& \max_i \sum_{i=1}^n \vert A_{ij}\vert \enspace\enspace\enspace\mbox{(maximum absolute row sum)}

The formula for the :math:`L_2` induced matrix norm is more complicated. We will see it when we study eigenvalues.
