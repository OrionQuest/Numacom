Midterm #1 Programming
======================

This is the take-home programming part of Midterm #1. You are **not allowed** to
collaborate with any other student, failure to comply will result in a score of
**zero** in the **entire** exam.

Please turn in your code along with your solution. Submissions should be made on Sakai.

.. topic:: Problem

    Write a routine for estimating the condition number :math:`\kappa(A)` of a
    matrix :math:`A` using the :math:`L_1`-norm. You will need to compute
    :math:`\lVert A\rVert_1`, which should be easy, and estimate :math:`\lVert
    A^{-1}\rVert_1`, which is more challenging. Note that we only want to
    **estimate** :math:`\lVert A^{-1}\rVert_1`, not compute it exactly (up to finite precision). One way
    to estimate :math:`\lVert A^{-1}\rVert_1` is to choose a vector :math:`y`
    such that the ratio :math:`\lVert z\rVert/\lVert y\rVert` is large, where
    :math:`z` is the solution to :math:`Az=y`. Try two different approaches to
    choosing :math:`y`:

    a.  Choose :math:`y` as the solution to the system :math:`A^Ty = c`, where
        :math:`c` is a vector each of whose components is :math:`\pm 1`, with the
        sign for each component chosen by the following heuristic. Using the
        factorization :math:`A = LU`, the system :math:`A^Ty=c` is solved in two
        stages, successively solving the triangular systems :math:`U^Tv = c` and
        :math:`L^Ty = v`. At each step of the first triangular solution, choose the
        corresponding component of :math:`c` to be either :math:`1` or :math:`-1`,
        depending on which will make the resulting component of :math:`v` *larger*
        in magnitude. (You will need to write a custom triangular solution routine
        to implement this.) Then solve the second triangular system in the usual way
        for :math:`y`.

        The idea here is that any ill-conditioning in :math:`A` will be
        reflected in :math:`U`, resulting in a relatively large :math:`v`. The
        relatively well-conditioned unit triangular matrix :math:`L` will then
        preserve this relationship, resulting in a relatively large :math:`y`.

    b.  Choose five different vectors :math:`y` *randomly* and use the one
        producing the largest ratio :math:`\lVert z\rVert/\lVert y\rVert`.

    Test both the approaches described in parts (a) and (b) on each of the
    following two matrices:

    .. math::

            A_1 &=& \enspace \left[\begin{array}{ccc} -10 & 7 & 0 \\ 5 & -1 & 5 \\ -3 & 2 & 6 \end{array}\right] \\
            A_2 &=& \enspace \left[\begin{array}{ccc} 92 & 66 & 25 \\ -73 & 78 & 24 \\ -80 & 37 & 10 \end{array}\right]

    Report your results using these two methods. Check the quality of your
    estimates using the function ``np.linalg.cond(A,1)`` and report your results.

    For solving the linear system :math:`Ax = b`, you can use the
    following code: ::

        import numpy as np
        x = np.linalg.solve(A,b)

    **Note:** The only place where you **should not** use this routine is when solving
    the system :math:`U^Tv = c`, where you need to adjust each component of :math:`c`
    depending on the magnitude of the corresponding component of :math:`v`.

    For computing the :math:`LU` decomposition of a matrix :math:`A`, you can
    use the following code: ::

        from scipy.linalg import lu
        A = np.array([[10.,-7.,0.],[5.,-1.,5.],[-3.,2.,6.]])
        P,L,U = lu(A,permute_l=False)

    Both the matrices :math:`A_1` and :math:`A_2` have been chosen such that the
    permutation matrix :math:`P = I_{3\times 3}`, the identity matrix. So you **do not** need to worry
    about pivoting in this problem. Finally, to generate a random vector :math:`y` using `NumPy <http://www.numpy.org/>`_,
    you can use the following code: ::

        >>> np.random.rand(3,1)
        array([[ 0.16823198],
               [ 0.91167363],
               [ 0.34837631]])

    Needless to say, you **cannot** use the function ``np.linalg.norm`` in this problem to compute the norm of a matrix. However,
    you **can** (and should) use it to compute the norm of a vector. Please use double precision,
    which is the default precision in `Python <https://www.python.org/>`_.
