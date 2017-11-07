Fixed Point Iteration
~~~~~~~~~~~~~~~~~~~~~

Newton's method is in itself a special case of a broader category of methods for
solving nonlinear equations called *fixed point iteration* methods.
Generally, if :math:`f(x)=0` is the nonlinear equation we seek to solve, a fixed point
iteration method proceeds as follows:

*   Start with :math:`x_0 = \enspace <\textsf{initial guess}>`.
*   Iterate the sequence

    .. math::
        x_{k+1} = g(x_k)

    where :math:`g(x)` is a properly designed function for this purpose. Note that :math:`g(x)`
    is related, but otherwise different than :math:`f(x)`.

Following this method, we construct the sequence :math:`x_0, x_1,
x_2,\ldots,x_k,\ldots` hoping that it will converge to a solution of :math:`f(x)=0`.
The following questions arise at this point:

1.  If this sequence converges, does it converge to *a solution of* :math:`f(x)=0`?

2.  Is this iteration guaranteed to converge?

3.  How fast does this iteration converge?

4.  (Of practical concern) When do we stop iterating and declare that we have
    obtained an acceptable approximation?

We start by addressing the first question: if the sequence :math:`\{x_k\}` does
converge, can we ensure that it will converge to a solution of :math:`f(x)=0`?
Taking limits on :math:`x_{k+1}=g(x_k)`, and assuming that

1.  :math:`\lim_{k\rightarrow\infty} x_k=a`, and
2.  the function :math:`g` is continuous,

gives

.. math::

    \lim_{k\rightarrow\infty} x_{k+1}=\lim_{k\rightarrow\infty}g(x_k)\Rightarrow a=g(a)

The simplest way to guarantee that :math:`a` is a solution to :math:`f(x)=0` (in other
words, :math:`f(a)=0`) is if we construct :math:`g(x)` such that

.. math::
    x=g(x) \enspace\enspace \mbox{is mathematically equivalent to} \enspace\enspace f(x)=0

There are many ways to make this happen, for example,

.. math::
    f(x)=0\Leftrightarrow x+f(x)=x \Leftrightarrow x=g(x), \enspace\enspace \mbox{where} \enspace\enspace g(x)\equiv x+f(x)

or

.. math::

    f(x)=0\Leftrightarrow e^{-x}f(x)=0\Leftrightarrow e^{-x}f(x)+x^2=x^2\Leftrightarrow\frac{e^{-x}f(x)+x^2}{x}=x\Leftrightarrow g(x)=x\enspace\enspace \mbox{where} \enspace\enspace g(x)\equiv\frac{e^{-x}f(x)+x^2}{x}

or

.. math::
    f(x)=0\Leftrightarrow -\frac{f(x)}{f'(x)}=0\Leftrightarrow x-\frac{f(x)}{f'(x)}=x\Leftrightarrow g(x)=x, \enspace\enspace \mbox{where} \enspace\enspace g(x)\equiv x-\frac{f(x)}{f'(x)}

The last example is exactly Newton's method; substituting the definition of
:math:`g(x)` above into the iteration :math:`x_{k+1}=g(x_k)` yields the familiar Newton
update equation. Thus, we know that if fixed point iteration converges, it will be to
a solution of :math:`f(x)=0`. From above, it should be apparent that the choice
of :math:`g(x)` is certainly not unique. Unfortunately, not all
these choices lead to an effective method. For example, consider the nonlinear
equation :math:`f(x)=x^2-a=0` (solution: :math:`\pm\sqrt{a}`) and the function :math:`g(x)=a/x`.
We can easily verify that

.. math::
    x=g(x)=\frac{a}{x}\Leftrightarrow x^2=a\Leftrightarrow x^2-a=0=f(x)

However, the iteration :math:`x_{k+1}=g(x_k)=a/x_k` yields,

.. math::
    x_1=\frac{a}{x_0},\enspace\enspace x_2=\frac{a}{x_1}=\frac{a}{a/x_0}=x_0

Thus, the sequence alternates forever between the values :math:`x_0,x_1,x_0,x_1,\ldots`
regardless of the initial value. Other choices of :math:`g(x)` may also create
divergent sequences, often regardless of the value of the initial guess.
Fortunately, there are ways to ensure that the sequence :math:`\{x_k\}` converges, by
making an appropriate choice of :math:`g(x)`. We will use the following definition:

.. topic:: Definition

    A function :math:`g(x)` is called a *contraction in
    the interval* :math:`[a,b]`, if there exists a number :math:`L\in[0,1)` such that

    .. math::
        |g(x)-g(y)|\leq L|x-y|

    for any :math:`x,y\in[a,b]`.

Examples:

*   :math:`g(x)=x/2`:

    .. math::
        |g(x)-g(y)|=\frac{1}{2}|x-y|

    for any :math:`x,y\in\mathbb R`.

*   :math:`g(x)=x^2`, in :math:`[0.1,0.2]`:

    .. math::
        |g(x)-g(y)|=|x^2-y^2|=|x+y||x-y|\leq 0.4|x-y|

    for :math:`x,y\in[0.1,0.2]` (in this case this condition is essential!)

If we can establish that the function :math:`g` in the fixed point iteration
:math:`x_{k+1}=g(x_k)` is a contraction, we can show the following:

.. topic:: Theorem

    Let :math:`a` be the actual solution to :math:`f(x)=0`, and assume :math:`|x_0-a|<\delta`,
    where :math:`\delta` is an arbitrary positive number. If :math:`g` is a contraction on
    :math:`(a-\delta,a+\delta)`, the fixed point iteration is guaranteed to converge to :math:`a`.

    *Proof:* Since :math:`a` is the solution, we have :math:`a=g(a)`. Thus,

    .. math::
        |x_1-a| &=& \enspace |g(x_0)-g(a)|\leq L|x_0-a|<L\delta \\
        |x_2-a| &=& \enspace |g(x_1)-g(a)|\leq L|x_1-a|<L^2\delta \\
        &\vdots& \\
        |x_k-a| &<& \enspace L^k\delta

    Since :math:`L<1`, we have :math:`\lim_{k\rightarrow\infty} |x_k-a|=0`, i.e.,
    :math:`x_k\rightarrow a`.

In some cases, it can be cumbersome to apply the definition directly to show
that a given function :math:`g` is a contraction. However, if we can compute the
derivative :math:`g'(x)` we have a simpler criterion:

.. topic:: Theoreom

    If :math:`g` is differentiable and a number :math:`L\in[0,1)` exists such
    that :math:`|g'(x)|\leq L` for all :math:`x\in[a,b]`, then :math:`g` is a contraction on :math:`[a,b]`.

    *Proof:* Let :math:`x,y\in[a,b]` and, without loss of generality, assume :math:`x<y`. The mean value
    theorem states that

    .. math::
        \frac{g(x)-g(y)}{x-y}=g'(c) \enspace\enspace \mbox{for some $c\in(x,y)$.}

    Now, if :math:`|g'(x)|\leq L` for all :math:`x\in[a,b]`, then regardless of the exact value
    of :math:`c` we have

    .. math::
        |g'(c)|\leq L\Rightarrow \left|\frac{g(x)-g(y)}{x-y}\right|\leq L\Rightarrow |g(x)-g(y)|\leq L|x-y|

Examples:

*   Let :math:`g(x)=\sin(\frac{2x}{3})`. Then

    .. math::
        |g'(x)|=\frac{2}{3}\left|\cos\left(\frac{2x}{3}\right)\right|\leq \frac{2}{3}<1

    Thus, :math:`g` is a contraction.

*   Let us try to apply the derivative criterion to see if the function

    .. math::
        g(x)=x-\frac{f(x)}{f'(x)}

    which defines Newton's method is a contraction:

    .. math::
        g'(x)=1-\frac{f'(x)f'(x)-f(x)f''(x)}{[f'(x)]^2}=\frac{f(x)f''(x)}{[f'(x)]^2}

    Now let us assume that

    *   :math:`f(a)=0`, i.e., :math:`a` is a solution of :math:`f(x)=0`,
    *   :math:`f'(a)\neq 0`, and
    *   :math:`f''` is *bounded* near :math:`a` (for example, if :math:`f''` is continuous).

    Then

    .. math::
        \lim_{x\rightarrow a} g'(x)=\frac{f(a)f''(a)}{[f'(a)]^2}=0

    This means that there is an interval :math:`(a-\delta,a+\delta)` where :math:`|g'(x)|` is
    *small* (since :math:`\lim_{x\rightarrow a} g'(x)=0`). Specifically, we can find
    an :math:`L<1` such that :math:`|g'(x)|\leq L` when :math:`|x-a|<\delta`. This means that :math:`g` is a
    contraction on :math:`(a-\delta,a+\delta)`, and if the initial guess also falls in
    that interval, the iteration is guaranteed to converge to the solution :math:`a`.

Let us revisit Newton's method once again. The equality we showed previously

.. math::
    g'(x)=\frac{f(x)f''(x)}{[f'(x)]^2}

can give us some insights about certain cases, where convergence is more likely,
and others where convergence may be at risk:

*   If :math:`f''` is small, :math:`g'(x)` will also tend to be small. In the limit case where
    :math:`f''(x)=0`, convergence is instantaneous. Of course, this is of limited interest
    because it would imply that the equation of interest is in fact linear, or :math:`f(x)=ax+b`.
    However, when :math:`f''(x)\approx 0`, we can expect very rapid convergence.

*   If :math:`f'(x)` is large, convergence will typically occur more easily. Of course,
    sometimes this fact coincides with :math:`f''` being large, in which case the two
    factors compete or cancel one another.

*   Another consequence is that, when :math:`f'(x)\approx 0` (i.e., the graph of :math:`f` is
    mostly ``flat"), convergence will be less certain. Compare this with our
    intuitive graphical explanation of ``flat" tangents in Newton's method.
