Non-linear Equations
====================

We now turn our attention to solving non-linear equations.
In an earlier lecture, we actually addressed
one common non-linear equation, the *quadratic* equation :math:`ax^2+bx+c=0`, and
discussed the potential hazards of using the seemingly straightforward quadratic
solution formula. We will start our discussion with an even simpler non-linear
equation:

.. math::
    
    x^2-a=0, \enspace\enspace a>0

The solution is obvious, :math:`x=\pm\sqrt{a}` (assuming, of course, that we have a
subroutine at our disposal that computes square roots). Let us, however,
consider a different approach:

* Start with :math:`x_0=\texttt{<initial guess>}`
* Iterate the sequence

    .. math::
        x_{k+1}=\frac{x_k^2+a}{2x_k}
        :label: iteration

We can show (and we will via examples) that this method is quite effective at
generating remarkably good approximations of :math:`\sqrt{a}` after just a few
iterations. Let us, however, attempt to analyze this process from a theoretical
standpoint. If we assume that the sequence :math:`x_0, x_1, x_2,\ldots` defined by this method has
a limit, how does that limit relate to the problem at hand? Assume
:math:`\lim_{k\rightarrow\infty}=A`. Then, taking limits on equation
:eq:`iteration` gives

.. math::

    \lim_{k\rightarrow\infty} x_{k+1}=\lim_{k\rightarrow\infty}\frac{x_k^2+a}{2x_k}
    \Rightarrow A=\frac{A^2+a}{2A}\Rightarrow 2A^2=A^2+a\Rightarrow A^2=a\Rightarrow
    A=\pm\sqrt{a}

Thus, if the iteration converges, the limit is the solution of the nonlinear
equation :math:`x^2-a=0`. The second question is whether it may be possible to
guarantee that the described iteration *will* converge. For this, we
manipulate equation :eq:`iteration` as follows

.. math::

    x_{k+1}=\frac{x_k^2+a}{2x_k}\Rightarrow
    x_{k+1}-\sqrt{a}=\frac{x_k^2+a}{2x_k}-\sqrt{a}=\frac{x_k^2-2x_k\sqrt{a}+a}{2x_k}=\frac{[x_k-\sqrt{a}]^2}{2x_k}

If we denote by :math:`e_k=x_k-\sqrt{a}` the error (or discrepancy) from the exact
solution of the approximate value :math:`x_k`, the previous equation reads

.. math::

    e_{k+1}=\frac{e_k^2}{2x_k}=\frac{e_k^2}{2(e_k+\sqrt{a})}

For example, if we were approximating the square root of :math:`a=2`, and at some
point we had :math:`e_k=10^{-3}`, the previous equation would suggest that
:math:`e_{k+1}<10^{-6}`. One more application of this equation would yield
:math:`e_{k+2}<10^{-12}`. Thus we see that, provided the iteration starts *close
enough* to the solution, we not only converge to the desired value, but actually
double the number of correct significant digits in each iteration. We defer the
detailed proof until after we have introduced the more general method.

.. toctree::
    :hidden:
    :maxdepth: 2

    Newton's Method <newton>
    Fixed Point Iteration <fixed>
    Order of Convergence <convergence>
    Multiple Roots <multiple>
    The Bisection Method <bisection>
