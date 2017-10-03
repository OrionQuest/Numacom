Homework #2
===========

For all programming assignments, please turn in your code along with your
solution. Submissions should be made on Sakai.

.. topic:: Problem 1

    Prove that the matrix :math:`L_k  = I + m_ke_k^T` is the inverse of the
    matrix :math:`M_k = I - m_ke_k^T`, where :math:`M_k` is the elimination
    matrix for the :math:`k^{th}` column :math:`a_k` of :math:`A`.

.. topic:: Problem 2

    Write a program to compute the LU decomposition of a matrix :math:`A` using the
    concept of elimination matrices. Use it to solve the following system:

    .. math::
        A=\left[\begin{array}{ccccccccc}
        21 & 32 & 14 & 8 & 6 & 9 & 11 & 3 & 5 \\
        17 & 2 & 8 & 14 & 55 & 23 & 19 & 1 & 6 \\
        41 & 23 & 13 & 5 & 11 & 22 & 26 & 7 & 9 \\
        12 & 11 & 5 & 8 & 3 & 15 & 7 & 25 & 19 \\
        14 & 7 & 3 & 5 & 11 & 23 & 8 & 7 & 9 \\
        2 & 8 & 5 & 7 & 1 & 13 & 23 & 11 & 17 \\
        11 & 7 & 9 & 5 & 3 & 8 & 26 & 13 & 17 \\
        23 & 1 & 5 & 19 & 11 & 7 & 9 & 4 & 16 \\
        31 & 5 & 12 & 7 & 13 & 17 & 24 & 3 & 11
        \end{array}\right]\left[\begin{array}{c}
        x_1 \\
        x_2 \\
        x_3 \\
        x_4 \\
        x_5 \\
        x_6 \\
        x_7 \\
        x_8 \\
        x_9
        \end{array}\right]=\left[\begin{array}{c}
        2 \\
        5 \\
        7 \\
        1 \\
        6 \\
        9 \\
        4 \\
        8 \\
        3
        \end{array}\right]

.. topic:: Problem 3

    Suppose that :math:`\lVert\cdot\rVert_a` and :math:`\lVert\cdot\rVert_b` are
    two equivalent vector norms in :math:`\mathbb R^n`. Thus, by definition, there
    exist two constants :math:`c,d>0` such that for any vector
    :math:`x\in\mathbb R^n`, we have

    .. math::

        c\lVert x\rVert_a \leq \lVert x\rVert_b \leq d\lVert x\rVert_a

    Prove that their induced matrix norms are also equivalent, i.e., there exist
    two constants :math:`c',d'>0` such that for any matrix :math:`A\in\mathbb
    R^{n\times n}`

    .. math::

        c'\lVert A\rVert_a \leq \lVert A\rVert_b \leq d'\lVert A\rVert_a

.. topic:: Problem 4

    (a) Use a single-precision routine for Gaussian elimination to solve the system
        :math:`Ax=b` defined below

    .. math::
        
        \left[\begin{array}{cccc}
        21.0 & 67.0 & 88.0 & 73.0 \\
        76.0 & 63.0 & 7.0 & 20.0 \\
        0.0 & 85.0 & 56.0 & 54.0 \\
        19.3 & 43.0 & 30.2 & 29.4
        \end{array}\right]\left[\begin{array}{c}
        x_1 \\
        x_2 \\
        x_3 \\
        x_4
        \end{array}\right]=\left[\begin{array}{c}
        141.0 \\
        109.0 \\
        218.0 \\
        93.7
        \end{array}\right]

    (b) Compute the residual :math:`r = b - Ax` using double-precision arithmetic,
        but storing the final result in a single-precision vector :math:`r`. (Note
        that the solution routine may destroy the matrix :math:`A`, so you may need
        to save a separate copy for computing the residual.)

    (c) Solve the linear system :math:`Az=r` to obtain the "improved" solution
        :math:`x+z`. (Note that the matrix :math:`A` need not be refactored.)

    (d) Repeat steps :math:`b)` and :math:`c)` until no further improvement is
        observed.

.. topic:: Problem 5

    Use Gaussian elimination *without* pivoting to solve the linear system

    .. math::

        \left[\begin{array}{cc}
        \varepsilon & 1 \\
        1 & 1
        \end{array}\right]\left[\begin{array}{c}
        x_1 \\
        x_2
        \end{array}\right] = \left[\begin{array}{c}
        1+\varepsilon \\
        2
        \end{array}\right]

    for :math:`\varepsilon=10^{-2k}`, where :math:`k=1,2,\ldots,10`.
    The exact solution is :math:`x=(1,1)^T`, independent of the value of
    :math:`\varepsilon`. How does the acccuracy of the computed solution behave
    as the value of :math:`\varepsilon` decreases?
