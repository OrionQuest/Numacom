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

Equivalence of different norms
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Several inequalities can be proved for the :math:`L_1`, :math:`L_2`, and
:math:`L_\infty`-norms, respectively. We start by showing that :math:`\lVert
x\rVert_\infty\leq \lVert x\rVert_1`.

.. math::
    \lVert x\rVert_\infty = \max_{i=1}^n \vert x_i\vert \leq \sum_{i=1}^n \vert x_i\vert = \lVert x\rVert_1

The inequality above follows from the fact that the sum of the absolute values
:math:`\sum_{i=1}^n \vert x_i\vert` *contains* the maximum absolute value :math:`\max_{i=1}^n
\vert x_i\vert`. Furthermore, the absolute value :math:`\vert x_i\vert` of each component
is less than or equal to the maximum of the absolute values over all components. This allows us to prove an
inequality in the reverse direction as well, albeit with the multiplicative factor
of :math:`n`.

.. math::
    \sum_{i=1}^n \vert x_i\vert \leq \sum_{i=1}^n \max_{i=1}^n \vert x_i\vert = \sum_{i=1}^n \lVert x\rVert_\infty = n\cdot\lVert x\rVert_\infty

The above two inequalities can be compactly written as :math:`\lVert x\rVert_\infty \leq \lVert x\rVert_1\leq n\cdot\lVert x\rVert_\infty`.
The equality holds when all components of :math:`x` are equal, as can be easily verified.

.. topic:: Example 1

    Consider the vector :math:`v = (5,2,1,4,3)`. The :math:`L_1` and
    :math:`L_\infty`-norms of :math:`v` are

    .. math::
        \lVert v\rVert_1 = 15\enspace\enspace\enspace\enspace \mbox{and} \enspace\enspace\enspace\enspace \lVert v\rVert_\infty = 5

    respectively. Note that :math:`\lVert v\rVert_\infty = 5\leq \lVert v\rVert_1 = 15 \leq 5\cdot\lVert v\rVert_\infty = 5\cdot 5 = 25`.

.. topic:: Definition

    Two vector norms :math:`\lVert x\rVert_a` and :math:`\lVert x\rVert_b` are
    called *equivalent* if there exist real numbers :math:`c,d>0`, such that

    .. math::
        c\lVert x\rVert_a \leq \lVert x\rVert_b \leq \lVert x\rVert_a

It follows from this definition that the :math:`L_1` and :math:`L_\infty`-norms are
equivalent, as proved above. Now consider the square of the :math:`L_1`-norm

.. math::
    \lVert x\rVert_1^2 = (\vert x_1\vert + \vert x_2\vert + \ldots + \vert x_n\vert)^2 = \sum_{i=1}^n\vert x_i\vert^2 + 2\sum_{i<j} \vert x_i\vert\cdot\vert x_j\vert \geq \sum_{i=1}^n\vert x_i\vert^2 = \lVert x\rVert_2^2

The above inequality implies that :math:`\lVert x\rVert_1\geq \lVert x\rVert_2`.
For the reverse direction of the inequality, consider the `AM-GM inequality <https://en.wikipedia.org/wiki/Inequality_of_arithmetic_and_geometric_means>`_:

.. math::
    2\vert x_i\vert\cdot\vert x_j\vert \enspace &\leq& \enspace \vert x_i\vert^2 + \vert x_j\vert^2 \\
    \Rightarrow 2\sum_{i<j} \vert x_i\vert\cdot\vert x_j\vert \enspace &\leq& \enspace (n-1)\cdot\sum_{i=1}^n \vert x_i\vert^2

The second inequality follows from the fact that each :math:`x_i` appears with
*exactly* :math:`n-1` other components :math:`x_j`.
Using the above inequality with the square of the :math:`L_1`-norm gives

.. math::
    \lVert x\rVert_1^2 = \sum_{i=1}^n\vert x_i\vert^2 + 2\sum_{i<j} \vert x_i\vert\cdot\vert x_j\vert \leq n\sum_{i=1}^n\vert x_i\vert^2 = n\cdot\lVert x\rVert_2^2

This implies that :math:`\lVert x\rVert_1\leq\sqrt{n}\lVert x\rVert_2`.
Combining the two inequalities gives :math:`\lVert x\rVert_2\leq\lVert
x\rVert_1\leq\sqrt{n}\lVert x\rVert_2`, proving that the :math:`L_1` and
:math:`L_2`-norms are equivalent as well. Again, equality holds when all components of
:math:`x` are equal.

.. topic:: Example 2

    Consider the same vector :math:`v = (5,2,1,4,3)`. The :math:`L_1` and
    :math:`L_2`-norms of :math:`v` are

    .. math::
        \lVert v\rVert_1 = 15 \enspace\enspace\enspace\enspace \mbox{and} \enspace\enspace\enspace\enspace \lVert v\rVert_2 = 7.4162

    respectively. Note that :math:`\lVert v\rVert_2 = 7.4162 \leq \lVert v\rVert_1 = 15 \leq \sqrt{5}\cdot 7.4162 = 16.5831`.
