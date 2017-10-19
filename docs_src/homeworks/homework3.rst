Homework #3
===========

For all programming assignments, please turn in your code along with your
solution. Submissions should be made on Sakai.

.. topic:: Problem 1

    In this problem, you will construct a proof that the Jacobi method converges
    when applied to matrices that are diagonally dominant. In the following
    subproblems, you are free to use any of the individual questions (even if
    you did not prove it) to answer the ones that come after it.

    a.  If :math:`x\in\mathbb R^n` and :math:`T` is an :math:`n\times n` matrix,
        show that for any positive integer :math:`k` the following inequality
        holds:

        .. math::

            \lVert T^k x\rVert \leq \lVert T\rVert^k \lVert x\rVert

    b.  Show that the Jacobi method can be written as:

        .. math::

            x^{(k+1)} = Tx^{(k)} + c

        where :math:`T=D^{-1}(L+U)` (using the decomposition :math:`A = D - L - U`).

    c.  Define the *error* after the :math:`k^{th}` iteration to be :math:`e^{(k)} = x^{(k)} - x^\star`,
        where :math:`x^\star` is the *exact* solution to the equation :math:`Ax=b`. Show that:

        .. math::

            e^{(k+1)} = Te^{(k)}

        **Hint:** You can use (after explaining why it is true) that :math:`x^\star = Tx^\star+c`.

    d.  If :math:`A` is diagonally dominant by rows, and :math:`T` is the matrix
        defined in (b) above, show that :math:`\lVert T\rVert_\infty < 1`.

        **Hint:** The way to prove this question may become more apparent if you
        write out explicitly what the first few rows of :math:`T = D^{-1}(L+U)`
        look like.

    e.  Show that when :math:`A` is diagonally dominant by rows, then:

        .. math::

            \lVert e^{(k)}\rVert_\infty \leq \lVert T\rVert^k_\infty \lVert e^{(0)}\rVert_\infty

        Explain why this result implies that the Jacobi method is guaranteed to
        converge for matrices that are diagonally dominant with rows.

.. topic:: Problem 2

    A polynomial :math:`p(t)` of degree :math:`n` is defined as:

    .. math::

        p(t) = a_nt^n + a_{n-1}t^{n-1} + \ldots + a_1t + a_0

    For :math:`n = 0,1,\ldots,5`, fit a polynomial of degree :math:`n` by least
    squares to the following data:

    .. math::

        \begin{array}{ccccccc}
        t & 0.0 & 1.0 & 2.0 & 3.0 & 4.0 & 5.0 \\
        y & 1.0 & 2.7 & 5.8 & 6.6 & 7.5 & 9.9
        \end{array}

    Make a plot of the original data points along with each resulting polynomial
    curve (you may make separate graphs for each curve, or a single graph
    containing all of the curves). Which polynomial would you say captures the
    general trend of the data better?

.. topic:: Problem 3

    a.  Solve the following least squares problem using the normal equations:

        .. math::

            \left[\begin{array}{cc}
            0.16 & 0.10 \\
            0.17 & 0.11 \\
            2.02 & 1.29
            \end{array}\right]\left[\begin{array}{c}
            x_1 \\
            x_2
            \end{array}\right] \cong \left[\begin{array}{c}
            0.26 \\
            0.28 \\
            3.31
            \end{array}\right]

    b.  Now solve the same least squares problem again, but this time use the
        slightly perturbed right-hand side:

        .. math::

            b = \left[\begin{array}{c}
            0.27 \\
            0.25 \\
            3.33
            \end{array}\right]

    c.  Compare your results from parts (a) and (b). Can you explain this
        difference?

        **Hint:** Use the function ``np.linalg.cond`` to compute the condition
        number of :math:`A^TA` in different norms.

.. topic:: Problem 4

    a.  Show that the matrix

        .. math::

            A = \left[\begin{array}{ccc}
            0.1 & 0.2 & 0.3 \\
            0.4 & 0.5 & 0.6 \\
            0.7 & 0.8 & 0.9
            \end{array}\right]

        is singular. Describe the set of solutions to the system :math:`Ax = b` if

        .. math::

            b = \left[\begin{array}{c}
            0.1 \\
            0.3 \\
            0.5
            \end{array}\right]

    b.  If we were to use Gaussian Elimination with partial pivoting to solve
        this system using *exact* arithmetic, at what point would the process
        fail?

    c.  Because some of the entries of :math:`A` are not exactly representable
        in a binary floating-point system, the matrix is no longer exactly
        singular when entered into a computer. Thus, solving the system by
        Gaussian Elimination will not necessarily fail. Compare the computed
        solution with your description of the solution set in part (a). What is
        the estimated value of the condition number :math:`\kappa(A)`? How many
        digits of accuracy would this lead you to expect?
