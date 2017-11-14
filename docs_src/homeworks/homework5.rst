Homework #5
===========

For all programming assignments, please turn in your code along with your
solution. Submissions should be made on Sakai.

.. topic:: Problem 1

    Express the following polynomial in the correct form for evaluation by
    Horner's method:

    .. math::
        p(t) = 5t^3 - 3t^2 + 7t  - 2

.. topic:: Problem 2

    How many multiplications are required to evaluate a polynomial :math:`p(t)`
    of degree :math:`n-1` at a given point :math:`t`

    a)  Represented in the monomial basis?
    b)  Represented in the Lagrange basis?
    c)  Represented in the Newton basis?

.. topic:: Problem 3

    a)  Determine the polynomial interpolant to the data

        .. math::

            \begin{array}{ccccc}
            t & 1 & 2 & 3 & 4 \\
            p(t) & 11 & 29 & 65 & 125
            \end{array}

        using the monomial basis.

    b)  Determine the Lagrange polynomial interpolant to the same data and show
        that the resulting polynomial is equivalent to that obtained in part (a).

    c)  Compute the Newton polynomial interpolant to the same data using each of
        the three methods discussed in class (triangular matrix, incremental
        interpolation, and divided differences) and show that each produces the
        same result as the previous two methods.

.. topic:: Problem 4

    a)  For a given set of data points :math:`t_1,\ldots,t_n`, define the function
        :math:`\pi(t)` by

        .. math::
            \pi(t) = (t-t_1)(t-t_2)\ldots (t-t_n)

        Show that

        .. math::
            \pi'(t_j) = (t_j - t_1)\ldots (t_j - t_{j-1})(t_j - t_{j+1})\ldots (t_j - t_n)

        **Hint:** If :math:`f_1,\ldots,f_n` are functions of a variable :math:`t`, then

        .. math::
            \frac{d}{dt} \prod_{i=1}^n f_i = \sum_{i=1}^n f_i' \prod_{j\neq i} f_j

    b)  Use the result of part (a) to show that the :math:`j^{th}` Lagrange
        basis function can be expressed as

        .. math::
            l_j(t) = \frac{\pi(t)}{(t-t_j)\pi'(t_j)}

.. topic:: Problem 5 (Extra Credit)

    Horner's rule provides an efficient method for evaluating a polynomial
    :math:`p(t) = \sum_{i=0}^n a_i t^i` of degree :math:`n` at any :math:`t=t_0`. In this exercise, we will develop a
    procedure for computing its derivative :math:`p'(t)` at :math:`t_0`.
    Notice that for any :math:`t_0`, we can divide :math:`p(t)` by :math:`(t-t_0)`
    to get quotient and remainder:

    .. math::
        p(t) = q(t)(t-t_0) + p(t_0)
        :label: factor

    where the quotient polynomial :math:`q(t)` has degree :math:`n-1`:

    .. math::
        q(t) = \sum_{i=0}^{n-1} b_i t^i

    One can easily verify that :math:`p'(t_0) = q(t_0)`. So if we can find the
    coefficients :math:`b_i` of the quotient polynomial :math:`q(t)`, we can use
    Horner's rule to compute :math:`p'(t_0)`. If we substitute the expressions of :math:`p(t)` and
    :math:`q(t)` in equation :eq:`factor` and equate the coefficients of
    :math:`t^i` on the LHS and RHS, and solve for the coefficients
    :math:`b_i` and remainder :math:`p(t_0)`, we get a series of equations that
    can be organized as a recursion relation:

    .. math::
        \begin{eqnarray*}
        b_{n-1} &=& a_n \\
        b_{i-1} &=& a_i + t_0b_i \enspace \mbox{for } i=1\ldots n-1 \\
        p(t_0) &=& a_0 + t_0b_0
        \end{eqnarray*}

    Write a program that uses the above recursion relation to evaluate both the
    polynomial :math:`p(t)` and it's derivative :math:`p'(t)` at
    :math:`t=t_0`. Show its output on few example polynomial functions (which you
    are free to choose).
