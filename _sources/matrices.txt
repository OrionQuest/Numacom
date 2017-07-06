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

In general, an :math:`m\times n` matrix is written as:

.. math::

    \left(
    \begin{array}{cccc}
    a_{11} & a_{12} & \ldots & a_{1n} \\
    a_{21} & a_{22} & \ldots & a_{2n} \\
    \vdots & \vdots & \ddots & \vdots \\
    a_{m1} & a_{m2} & \ldots & a_{mn}
    \end{array}
    \right)

In the example above, :math:`a_{ij}=v^j_i`. `NumPy <http://www.numpy.org/>`_ has a ``matrix`` class to conveniently define
:math:`m\times n` matrices, as shown below: ::

    >>> a=np.matrix('1 2 3;4 5 6;7 8 9')
    >>> a
    matrix([[1, 2, 3],
            [4, 5, 6],
            [7, 8, 9]])
    >>> b=np.matrix([[1,2,3],[4,5,6],[7,8,9]])
    >>> b
    >>> matrix([[1, 2, 3],
        [4, 5, 6],
        [7, 8, 9]])

Note that `NumPy <http://www.numpy.org/>`_ defines the individual elements of
the matrix by specifying the rows, *not* the columns.
