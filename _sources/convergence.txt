Order of Convergence
~~~~~~~~~~~~~~~~~~~~

We previously used the hypothesis that :math:`g` (in the fixed point iteration :math:`x_{k+1}=g(x_k)`)
is a contraction to show that :math:`|x_k-a|\xrightarrow{k\rightarrow\infty}0`.
Remember that the quantity

.. math::
    e=x_\texttt{approximate}-x_\texttt{exact}

was previously defined as the (absolute) error. In this case, let us define
:math:`e_k=x_k-a` (:math:`a` is the solution, i.e., :math:`f(a)=0`) as the error after the :math:`k`-th
iteration. If :math:`g` is a contraction, we have

.. math::
    |e_{k+1}|=|x_{k+1}-a|=|g(x_k)-g(a)|\leq L|x_k-a|=L|e_k|

Since :math:`L<1`, the error shrinks at least by a constant factor at each iteration.
In some cases, we can do even better. Remember the following theorem:

.. topic:: Theorem

    If a function :math:`g` is :math:`k`-times differentiable, then:

    .. math::

        g(y)=g(x) + g'(x)(y-x)+\frac{g''(x)}{2!}(y-x)^2+\frac{g'''(x)}{3!}(y-x)^3 + \ldots + \frac{g^{(k-1)}(x)}{(k-1)!}(y-x)^{k-1}+\frac{g^{(k)}(c)}{k!}(y-x)^k

    for some number :math:`c` between :math:`x` and :math:`y`.

For :math:`k=1`, we simply obtain the mean value theorem:

.. math::
    g(y)=g(x)+g'(c)(y-x)\Leftrightarrow \frac{g(y)-g(x)}{y-x}=g'(c)

(for some :math:`c` between :math:`x` and :math:`y`), which we used before to show that
:math:`|g'(x)|\leq L<1` implies that :math:`g` is a contraction.
We will now use the theorem in the case :math:`k=2`:

.. math::
    g(y)=g(x)+g'(x)(y-x)+\frac{g''(c)}{2}(y-x)^2 \enspace\enspace \mbox{for some $c$ between $x$ and $y$}
    :label: taylor-2

Let :math:`g(x)=x-f(x)/f'(x)` (as in Newton's method). Now, let us make the following
substitutions in the equation above:

.. math::
    x\leftarrow a \enspace \mbox{(the solution), and} \enspace y\leftarrow x_k

If :math:`f'(a)\neq 0` and :math:`f''(a)` is defined, then

.. math::
    g'(a)=\frac{\overbrace{f(a)}^{=0}f''(a)}{[f'(a)]^2}=0

Thus, equation :eq:`taylor-2` becomes

.. math::
    &g(x_k)& = g(a)+\frac{g''(c)}{2}(x_k-a)^2 \\
    &\Rightarrow& x_{k+1}=a+\frac{g''(c)}{2}(x_k-a)^2 \\
    &\Rightarrow& |x_{k+1}-a|=\left|\frac{g''(c)}{2}\right||x_k-a|^2

.. math::
    \Rightarrow |e_{k+1}|\leq C|e_k|^2 \enspace\enspace \mbox{note the exponent!}
    :label: taylor-2-error

where

.. math::
    C\equiv \max\left|\frac{g''(x)}{2}\right|_{\mbox{$x$ between $a$ and $x_k$}}

Compare equation :eq:`taylor-2-error` with the general guarantee

.. math::
    |e_{k+1}|\leq L|e_k|
    :label: error-series

for contractions:

*   Equation :eq:`error-series` depends on :math:`L<1` to reduce the error. In
    equation :eq:`taylor-2-error`, even if :math:`C` is larger than one, if :math:`e_k`
    is small enough then :math:`e_{k+1}` will be reduced. Consider for example, the case
    :math:`C=10`, :math:`|e_k|=10^{-3}` which will guarantee :math:`|e_{k+1}|\leq 10^{-5}`, and
    :math:`|e_{k+2}|\leq 10^{-9}` in the next iteration.

*   Equation :eq:`error-series` implies that every iteration adds a fixed
    number (or, a fixed fraction) of correct significant digits. For example, if
    :math:`L=0.3`:

    .. math::
        |e_{k+2}|\leq 0.3|e_{k+1}|\leq 0.09|e_k|

    Thus, we gain :math:`1` significant digit every :math:`2` iterations.

More generally, if an iterative scheme for solving :math:`f(x)=0` can guarantee that

.. math::
    |e_{k+1}|\leq L|e_k|^d

then the exponent :math:`d` (which can be a fractional number too) is called the
*order of convergence*.  Specifically:

*   If :math:`d=1`, we shall also require that :math:`L<1` in order to guarantee that the error
    :math:`e_k` is being reduced. In this case, we say that the method exhibits
    *linear* convergence.

*   If :math:`d>1`, we no longer need :math:`L<1` as a strict condition for convergence
    (although we need to be "close enough" to the solution to guarantee progress).
    This case is described as *superlinear* convergence. The case :math:`d=2` is
    referred to as *quadratic* convergence, the case :math:`d=3` is referred to as
    *cubic* convergence, and so on.

We previously saw that Newton's method converges quadratically. More generally,
for the fixed point iteration :math:`x_{k+1}=g(x_k)`, if we can show that :math:`g'(a)=0`
(where :math:`a` is the solution), then Taylor's second order formula yields the same result
as in equation :eq:`taylor-2-error`, and the fixed point iteration converges quadratically.
