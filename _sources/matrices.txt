.. _sec-matrices:

Matrices
--------

Suppose we have :math:`n` vectors :math:`v^1,v^2,\ldots,v^n\in\mathbb R^m`.
There are several options available to us for denoting this set, either by writing each
one individually as a separate column vector:

.. math::

    v^1=\left(
        \begin{array}{c}
        v^1_1 \\
        v^1_2 \\
        \vdots \\
        v^1_m
        \end{array}
    \right), v^2=\left(
        \begin{array}{c}
        v^2_1 \\
        v^2_2 \\
        \vdots \\
        v^2_m
        \end{array}
    \right),\ldots,v^n=\left(
        \begin{array}{c}
        v^n_1 \\
        v^n_2 \\
        \vdots \\
        v^n_m
        \end{array}
    \right)

or by adopting the more efficient notation of combining all of them into a single :math:`m\times n` matrix:

.. math::
    
    \left(
    \begin{array}{cccc}
    \vert & \vert & & \vert \\
    v^1 & v^2 & \ldots & v^n \\
    \vert & \vert & & \vert
    \end{array}
    \right) = \left(
    \begin{array}{cccc}
    v^1_1 & v^2_1 & \ldots & v^n_1 \\
    v^1_2 & v^2_2 & \ldots & v^n_2 \\
    \vdots & \vdots & \ddots & \vdots \\
    v^1_m & v^2_m & \ldots & v^n_m
    \end{array}
    \right)

In general, an :math:`m\times n` matrix :math:`A\in\mathbb R^{m\times n}` is written as:

.. math::

    A = \left(
    \begin{array}{cccc}
    A_{11} & A_{12} & \ldots & A_{1n} \\
    A_{21} & A_{22} & \ldots & A_{2n} \\
    \vdots & \vdots & \ddots & \vdots \\
    A_{m1} & A_{m2} & \ldots & A_{mn}
    \end{array}
    \right)

In the example above, :math:`A_{ij}=v^j_i`. `NumPy <http://www.numpy.org/>`_ has a ``matrix`` class to conveniently define
:math:`m\times n` matrices, as shown below: ::

    >>> a=np.matrix([[1,2,3],[4,5,6],[7,8,9]])
    >>> a
    >>> matrix([[1, 2, 3],
        [4, 5, 6],
        [7, 8, 9]])

Note that `NumPy <http://www.numpy.org/>`_ defines the individual elements of
the matrix by specifying the rows, *not* the columns. You are probably familiar
with the :math:`n\times n` *identity matrix* defined as:

.. math::

    I_{n\times n} = \left(\begin{array}{cccc}
    \vert & \vert & & \vert \\
    e^1 & e^2 & \ldots & e^n \\
    \vert & \vert & & \vert
    \end{array}
    \right) = \left(\begin{array}{ccccc}
    1 & 0 & \ldots & 0 & 0 \\
    0 & 1 & \ldots & 0 & 0 \\
    \vdots & \vdots & \ddots & \vdots & \vdots \\
    0 & 0 & \ldots & 1 & 0 \\
    0 & 0 & \ldots & 0 & 1
    \end{array}
    \right)

Let :math:`x\in\mathbb R^{n\times 1}` be an :math:`n`-dimensional column vector
and :math:`A\in\mathbb R^{m\times n}` be an :math:`m\times n` matrix. The
matrix-vector product :math:`b=Ax` is the :math:`m`-dimensional vector defined
as:

.. math::

    b = \left(\begin{array}{c}
    b_1 \\
    b_2 \\
    \vdots \\
    b_m
    \end{array}
    \right),\mbox{ where }b_i = \sum_{j=1}^n A_{ij}x_j\mbox{ for all }1\leq i\leq m

Note that *all* matrices are *linear* operators, i.e., if :math:`x,y\in\mathbb R^{n\times 1}`
are two arbitrary :math:`n`-dimensional vectors, and :math:`\alpha\in\mathbb R`
is an arbitrary scalar, then it follows that:

.. math::

    A(x+y) &=& \enspace Ax + Ay \\
    A(\alpha x) &=& \enspace \alpha Ax

Matrix-vector products can be computed in `NumPy <http://www.numpy.org/>`_ using
the ``dot`` operator, as shown below: ::

    >>> a=np.matrix([[1,2,3],[4,5,6],[7,8,9]])
    >>> b=np.array([4,5,9])
    >>> a.dot(b)
    array([ 41,  95, 149])

Suppose we consider the individual columns :math:`v^1,v^2,\ldots,v^n` of
:math:`A`, as shown above. Then the matrix-vector product :math:`b` can be
re-written as a *linear combination* of the columns of :math:`A`, i.e., :math:`b=Ax=\sum_{i=1}^n x_iv^i`.
This relation can be schematically depicted as follows:

.. math::

    \left(\begin{array}{c}
    \vert \\
    b \\
    \vert
    \end{array}\right) = \left(\begin{array}{cccc}
    \vert & \vert & & \vert \\
    v^1 & v^2 & \ldots & v^n \\
    \vert & \vert & & \vert
    \end{array}\right)\left(\begin{array}{c}
    x_1 \\
    x_2 \\
    \vdots \\
    x_n
    \end{array}\right) = x_1\left(\begin{array}{c}
    \vert \\
    v^1 \\
    \vert
    \end{array}\right) + x_2\left(\begin{array}{c}
    \vert \\
    v^2 \\
    \vert
    \end{array}\right) + \ldots + x_n\left(\begin{array}{c}
    \vert \\
    v^n \\
    \vert
    \end{array}\right)

Traditionally, we are used to viewing the relation :math:`Ax=b` as the *action*
of :math:`A` on :math:`x` to produce :math:`b`. The equation above is a
different interpretation that suggests, in contrast, that :math:`x` acts on
:math:`A` to produce :math:`b`. Also, note how the dimensions of the result
:math:`b` are dependent on the dimensions of :math:`A` and :math:`x`:

.. math::

    b_{m\times 1} = A_{m\times n}\cdot x_{n\times 1}

The "middle" dimension :math:`n` has to be the same for both :math:`A` and
:math:`x` and is consumed as a result of the multiplication. This same principle also applies to the case of multiplying two arbitrary matrices,
i.e., if :math:`A\in\mathbb R^{m\times n}` and :math:`B\in\mathbb R^{n\times
p}` are two matrices, then their product :math:`C=A\cdot B\in\mathbb R^{m\times p}`. The ``dot`` operator
in `NumPy <http://www.numpy.org/>`_ can also be used for multiplying two
matrices, as shown below: ::

    >>> a = np.matrix([[1,2,3,4],[5,6,7,8],[9,10,11,12]])
    >>> a
    matrix([[ 1,  2,  3,  4],
            [ 5,  6,  7,  8],
            [ 9, 10, 11, 12]])
    >>> b = np.matrix([[1,2,3],[4,5,6],[7,8,9],[10,11,12]])
    >>> b
    matrix([[ 1,  2,  3],
            [ 4,  5,  6],
            [ 7,  8,  9],
            [10, 11, 12]])
    >>> a.dot(b)
    matrix([[ 70,  80,  90],
            [158, 184, 210],
            [246, 288, 330]])
