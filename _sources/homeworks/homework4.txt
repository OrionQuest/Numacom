Homework #4
===========

For all programming assignments, please turn in your code along with your
solution. Submissions should be made on Sakai.

.. topic:: Problem 1

    Consider the following procedure for solving the nonlinear equation
    :math:`f(x)=0`:

    *   Start with an initial guess :math:`x_0`.
    *   For :math:`k=0,1,2,\ldots` do the following:

        *   Compute the value that standard Newton's method would provide, and
            call it :math:`\hat x_{k+1}`, i.e.,

            .. math::
                \hat x_{k+1} = x_k - \frac{f(x_k)}{f'(x_k)}

        *   Compute the next approximation :math:`x_{k+1}` by averaging
            :math:`x_k` and :math:`\hat x_{k+1}`, i.e.,

            .. math::
                x_{k+1} = \frac{x_k + \hat x_{k+1}}{2}

    a.  Show that if this method converges, it will converge to a solution of :math:`f(x)=0`.
    b.  Show that this method converges under the same conditions as Newton's method.
    c.  Determine the order of convergence of this method.

.. topic:: Problem 2

    For the equation

    .. math::
        f(x) = x^2 - 3x + 2 = 0

    each of the following functions yields an equivalent fixed-point problem:

    .. math::
        g_1(x)  & = & \enspace  (x^2+2)/3 \\
        g_2(x)  & = & \enspace  \sqrt{3x-2} \\
        g_3(x)  & = & \enspace 3 - 2/x \\
        g_4(x)  & = & \enspace (x^2 - 2)/(2x - 3)

    a.  Analyze the convergence properties of each of the corresponding
        fixed-point iteration schemes for the root :math:`x=2` by considering
        :math:`\lvert g_i'(2) \rvert`.

    b.  Confirm your analysis by implementing each of the schemes and verifying
        its convergence (or lack thereof) and approximate convergence rate.

.. topic:: Problem 3

    Implement the bisection, Newton, and secant methods for solving nonlinear
    equations in one dimension, and test your implementations by finding at
    least one root for each of the following equations. What termination
    criterion should you use? What convergence rate is achieved in each case?

    a.  :math:`x^3 - 2x - 5 = 0`.
    b.  :math:`e^{-x} = x`.
    c.  :math:`x \sin x = 1`.
    d.  :math:`x^3 - 3x^2 + 3x - 1 = 0`.

.. topic:: Problem 4

    Suppose you are using the Secant method to find a root :math:`x^\star` of a
    nonlinear equation :math:`f(x) = 0`. Show that if at any iteration it
    happens to be the case that either :math:`x_k = x^\star` or :math:`x_{k-1} =
    x^\star` (but not both), then it will also be true that :math:`x_{k+1} =
    x^\star`.

