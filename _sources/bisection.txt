The Bisection Method
~~~~~~~~~~~~~~~~~~~~

Newton's method is a popular technique for the solution of nonlinear equations,
but alternative methods exist which may be preferable in certain situations. The
*Bisection method* is yet another technique for finding a solution to the
nonlinear equation :math:`f(x)=0`, which can be used provided that the function :math:`f` is
continuous. The motivation for this technique is drawn from  Bolzano's theorem
for continuous functions:

.. topic:: Theorem (Bolzano)

    If the function :math:`f(x)` is continuous in :math:`[a,b]` and
    :math:`f(a)f(b)<0` (i.e., the function has values with different signs at :math:`a` and
    :math:`b`), then a value :math:`c\in (a,b)` exists such that :math:`f(c)=0`.

.. image:: images/bisection.png
    :height: 782px
    :width: 1005px
    :scale: 60%
    :align: center

The bisection algorithm attempts to locate the value :math:`c` where the graph of :math:`f`
crosses over zero, by checking whether it belongs to either of the two
sub-intervals :math:`[a,x_m]`, :math:`[x_m,b]`, where :math:`x_m` is the midpoint

.. math::
    x_m=\frac{a+b}{2}

The algorithm proceeds as follows:

*   If :math:`f(x_m)=0`, we have our solution :math:`(x_m)` and the algorithm terminates.

*   In the much more likely case that :math:`f(x_m)\neq 0`, we observe that :math:`f(x_m)`
    *must* have the opposite sign than one of :math:`f(a)` or :math:`f(b)` (since they have
    opposite signs themselves). Thus,

    *   Either :math:`f(a)f(x_m)<0`, or

    *   :math:`f(x_m)f(b)<0`.

    We pick whichever of these two intervals satisfies the condition, and continue the bisection process with it.

**Convergence:** Let us conventionally define the "approximation" at :math:`x_k`
after the :math:`k`-th iteration as the midpoint

.. math::
    x_k=\frac{a_k+b_k}{2}

of :math:`I_k`. Since the actual solution :math:`f(c)=0` satisfies :math:`c\in I_k`, we have

.. math::
    |x_k-c|\leq\frac{1}{2}|I_k|

where :math:`|I_k|` symbolizes the length of the interval :math:`I_k`. Since the length of
the current search interval gets divided in half in each iteration, we have

.. math::
    |e_k|=|x_k-c|\leq \left(\frac{1}{2}\right)^k|I_0|

We interpret this behavior as *linear* convergence; although we cannot
strictly guarantee that :math:`|e_{k+1}|\leq L|e_k|` (:math:`L<1`) at each iteration, this
definition can also be iterated to yield

.. math::
    |e_k|\leq L^k|e_0|

which is qualitatively equivalent to the expression for bisection. Since the
order of convergence is linear, we expect to gain a fixed number (or fixed
fraction) of significant digits at each iteration; since :math:`0.5^{10}\approx 0.001`
we can actually say that the bisection method yields about :math:`3` additional
correct significant digits after every :math:`10` iterations.

The bisection procedure is very robust, by virtue of Bolzano's theorem, and
despite having only linear convergence can be used to find an approximation
within any desired error tolerance. It is often used to localize a good initial
guess which can then be rapidly improved with a fixed point iteration method
such as Newton's method. *Note that bisection search is not a fixed point
iteration itself!*
