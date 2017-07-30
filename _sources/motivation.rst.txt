Motivation
----------

In many instances, we are faced with mathematical problems where the conventional
method "on paper" does not perform as well when implemented on the computer.
Take, for example, the quadratic equation:

.. math::
    ax^2 + bx + c = 0

In theory, we have a perfectly conclusive method for determining the roots of
this equation; simply use the quadratic formula:

.. math::
    x_{1,2} = \frac{-b\pm\sqrt{b^2-4ac}}{2a}
    :label: quadratic

In fact, let us consider a very specific example:

.. math::
    0.0501x^2 -98.78x +5.015 = 0

The actual roots of this equation, rounded to :math:`10` digits of accuracy,
are:

.. math::
    x_1 = 1971.605916, \enspace\enspace\enspace\enspace x_2 = 0.05077069387

We then proceed to evaluate formula :eq:`quadratic` on the computer. Let us assume
that the computer stores all intermediate results of this computation with
:math:`4` `significant digits <https://www.google.com/>`_. Thus, we obtain the following answers:

.. math::
    x_1=1972, \enspace\enspace\enspace\enspace x_2=0.0998

Although the value of :math:`x_1` is reasonably accurate (in fact, it is the
correct answer to :math:`4` significant digits), the value of :math:`x_2` is off
by almost :math:`100\%` from the intended value, even when rounded to :math:`4`
digits. The reason for this behavior is hiding in the inaccurate (approximate)
representation of the intermediate steps of this calculation. Particularly, the
computer algorithm approximates :math:`\sqrt{b^2-4ac}\approx 98.77`, discarding
any subsequent digits due to its limited available precision. Substituting this
value into the quadratic formula yields:

.. math::
    x_{1,2} = \frac{98.78\pm 98.77}{0.1002}

The numerator involves either a sum or a difference of two nearly equal
quantities. When adding the two values, we compute the reasonably accurate
:math:`x_1=1972`. When subtracting, all the information that was discarded by
truncating :math:`\sqrt{b^2-4ac}\approx 98.77` is now dominating the computed
value of the numerator. As a consequence, we obtain the compromised value
:math:`x_2=0.0998`. In general, subtraction *reveals* the error, and division by
a small number *amplifies* it.

So, subtracting two nearly equal quantities is risky :math:`\ldots` can we avoid
doing so? There is, in fact, an alternative formulation:

.. math::
    x_{1,2} &=& \frac{(-b\pm\sqrt{b^2-4ac})(-b\mp\sqrt{b^2-4ac})}{2a(-b\mp\sqrt{b^2-4ac})} \\
            &=& \frac{b^2-(b^2-4ac)}{2a(-b\mp\sqrt{b^2-4ac})} = \frac{4ac}{2a(-b\mp\sqrt{b^2-4ac})} \\
            &=& \frac{2c}{-b\mp\sqrt{b^2-4ac}}
    :label: derationalized

Equation :eq:`derationalized` subtracts two quantities in the denominator,
whereas :eq:`quadratic` adds them (and vice-versa). This technique is called
*derationalization*. Applying this approach, we obtain:

.. math::
    x_1 = 1003, \enspace\enspace\enspace\enspace x_2=0.05077

Here the roles are reversed, :math:`x_2` is quite accurate, but :math:`x_1` is
off by about :math:`50\%` from the intended value. One might suggest that we
"selectively" use either :eq:`quadratic` or :eq:`derationalized` to compute
:math:`x_1` or :math:`x_2` respectively, and avoid the subtraction-induced
inaccuracies. Although this may be reaslistic in this isolated example, in more
complex problems that arise in practice, performing such a case-by-case handling
may prove impractical. In many cases, it may even be impossible to predict that
a value lacks accuracy (not knowing the exact value beforehand).

Let us take a brief detour and look at an iterative scheme for computing
:math:`\sqrt{a}`. Starting with an initial guess :math:`x_0`, we iterate as
follows:

.. math::
    x_{k+1} = \frac{x_k^2+a}{2x_k}

Assuming this scheme converges, i.e., :math:`\lim_{k\rightarrow\infty} x_k=A`,
gives:

.. math::
    A = \frac{A^2+a}{2A} \Rightarrow 2A^2=A^2+a \Rightarrow A^2=a \Rightarrow A=\sqrt{a}

Note that we computed :math:`\sqrt{a}` with just addition, multiplication, and
division operations! The same principle can be applied to solve a quadratic
equation as well. Consider the following scheme (which is a special case of what
we will later describe as Newton's method):

* Start with an initial guess :math:`x_0` of the solution.
* Iterate

.. math:: x_{k+1} = \frac{ax_k^2-c}{2ax_k+b}

* After :math:`N` iterations, take :math:`x_N` as the estimated solution.

Let us try it :math:`\ldots` start with a guess :math:`x_0=1`,

.. math::
    x_0=1, \enspace\enspace x_1=0.050313\ldots, \enspace\enspace x_2=0.0507706\ldots

After just two iterations, :math:`x_2` is correct to more than :math:`6`
significant digits! Let us aim for the other solution by setting :math:`x_0=2000`,

.. math::
    x_0=2000, \enspace\enspace x_1=1972.003\ldots, \enspace\enspace x_2=1971.60599\ldots

As is typically the case, there are trade-offs to consider: with this iterative
method, we require an "initial guess", and there is little guidance offered on
how to pick a good one. Also, we need a few iterations before we can obtain an
excellent approximation. On the other hand, the method does not require any
square roots, thus being significantly cheaper in terms of computation cost per
iteration. In general, the two different methodologies that we have seen fall
into two broad classes:

* **Direct methods:** These methods give a "recipe" for directly obtaining the
  final solution. The closed-form formulas we saw above for the roots of a
  quadratic equation fall in this category.
* **Iterative methods:** These methods obtain better approximations to the
  solution through successive iterations.

The traits and trade-offs of such methods will be a point of focus for this
class, and are central to the field we call *numerical analysis* and *scientific
computing*.
