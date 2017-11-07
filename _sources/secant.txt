The Secant Method
~~~~~~~~~~~~~~~~~

The *secant method* is yet another iterative technique for solving
nonlinear equations; it closely mimics Newton's method, but relaxes the
requirement that an analytic expression for the derivative :math:`f'(x)` must be
provided. It operates as follows:

*   We bootstrap the iteration not only with one initial guess :math:`(x_0)`, but also with
    a second improved approximation :math:`x_1`.

*   At the :math:`k`-th step of the iteration, we first approximate

    .. math::
        f'(x_k)\approx\frac{f(x_k)-f(x_{k-1})}{x_k-x_{k-1}}

    Remember that since

    .. math::
        f'(x_k)=\lim_{y\rightarrow x_k}\frac{f(x_k)-f(y)}{x_k-y}

    as the iterates :math:`x_{k-1}`, :math:`x_k` get closer to one another (while they both
    approach the solution) this approximation becomes more and more accurate.
    We then replace this particular approximation for :math:`f'(x_k)` in Newton's method
    :math:`x_{k+1}=x_k-f(x_k)/f'(x_k)` to obtain:

    .. math::
        x_{k+1}=x_k-\frac{f(x_k)}{\frac{f(x_k)-f(x_{k-1})}{x_k-x_{k-1}}}

Geometrically, Newton's method approximates :math:`f(x)` at each step by the
*tangent* line to the graph of :math:`f(x)`, while the method we just described
approximates :math:`f` by the *secant* line as illustrated below:

.. image:: images/secant.png
    :height: 413px
    :width: 1127px
    :scale: 70%
    :align: center

We can show that, once we are "close enough" to the solution, the error :math:`e_k`
for the secant method satisfies

.. math::
    |e_{k+1}|\leq c|e_k|^d,\enspace\enspace\mbox{where $d=\frac{1+\sqrt{5}}{2}\approx 1.6$}

Thus, the secant method provides *superlinear* convergence. In practice, it
may need a few more iterations (about :math:`50\%` more?) than Newton's method, but we
need to weigh in the fact that each iteration is likely cheaper, since no
derivatives of :math:`f` need to be evaluated.

*Order of convergence:* Let the exact solution be :math:`a`, i.e., :math:`f(a)=0`. Define :math:`e_k=x_k-a` and :math:`f_k=f(x_k)`. Then,

.. math::
    e_{k+1}=x_{k+1}-a &=& \enspace x_k-\frac{x_k-x_{k-1}}{f_k-f_{k-1}}f_k-a \\
                      &=& \enspace \frac{(x_{k-1}-a)f_k-(x_k-a)f_{k-1}}{f_k-f_{k-1}} \\
                      &=& \enspace \frac{e_{k-1}f_k-e_kf_{k-1}}{f_k-f_{k-1}} \\
                      &=& \enspace \frac{e_{k-1}f(a+e_k)-e_kf(a+e_{k-1})}{f_k-f_{k-1}}

Expanding :math:`f(a+e_k)` using Taylor's series gives

.. math::
    e_{k+1} &=& \enspace \frac{e_{k-1}(e_kf'(a)+e_k^2f''(a)/2+O(e_k^3))-e_k(e_{k-1}f'(a)+e_{k-1}^2f''(a)/2+O(e_{k-1}^3))}{e_kf'(a)+e_k^2f''(a)/2+O(e_k^3)-(e_{k-1}f'(a)+e^2_{k-1}f''(a)/2+O(e_{k-1}^3))} \nonumber \\
            &=& \enspace \frac{e_{k-1}e_kf''(a)(e_k-e_{k-1})/2+O(e_{k-1}^4)}{(e_k-e_{k-1})(f'(a)+(e_k+e_{k-1})f''(a)/2+O(e_{k-1}^2))}

.. math::
    \Rightarrow e_{k+1} = \frac{e_{k-1}e_kf''(a)}{2f'(a)}+O(e_{k-1}^3)
    :label: error

We want to find :math:`\alpha` such that :math:`|e_{k+1}|=C|e_k|^\alpha`. 
Since the first term in equation :eq:`error` dominates the error, we
ignore the cubic term and solve

.. math::
    \left|\frac{e_{k-1}e_kf''(a)}{2f'(a)}\right|=C|e_k|^\alpha
    :label: error-convergence-C

Canceling :math:`e_k` from both sides and changing :math:`k` to :math:`k+1` gives
:math:`|e_{k+1}|^{\alpha-1}=D|e_k|`, where :math:`D=|f''(a)/(2Cf'(a))|`. Raising both sides
by the power :math:`\alpha` gives

.. math::
    |e_{k+1}|^{\alpha (\alpha-1)}=D^\alpha|e_k^\alpha|
    :label: error-convergence-D

Equating equations :eq:`error-convergence-C` and
:eq:`error-convergence-D` gives, :math:`C=D^\alpha` and :math:`\alpha (\alpha-1)=1`.
The negative solution can be discarded because we know that the order of convergence is positive. Thus, the order
of convergence is :math:`\alpha=(1+\sqrt{5})/2\approx1.618`.
