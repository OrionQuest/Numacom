Newton's Method
~~~~~~~~~~~~~~~

This example is a special case of an algorithm for solving nonlinear equations
known as Newton's method (also called the *Newton-Raphson* method). The
general idea is as follows: if we "zoom" close enough to any smooth function,
its graph looks more and more like a straight line (specifically, the
*tangent* line to the curve). Newton's method suggests: if after :math:`k` iterations we have approximated the
solution of :math:`f(x)=0` (a general nonlinear equation) as :math:`x_k`, then:

    .. image:: images/newton.png
        :height: 426px
        :width: 816px
        :scale: 75%
        :align: center

* Form the tangent line at :math:`(x_k,f(x_k))`.
* Select :math:`x_{k+1}` as the intersection of the tangent line with the horizontal axis (:math:`y=0`).

If :math:`(x_n,y_n)=(x_n,f(x_n))`, the tangent line to the plot of :math:`f(x)` at :math:`(x_n,y_n)` is:

.. math::
    
    y-y_n=\lambda(x-x_n), \enspace\enspace \mbox{where $\lambda=f'(x_n)$ is the slope}

Thus, the tangent line has equation :math:`y-y_n=f'(x_n)(x-x_n)`.

    .. image:: images/newton-iteration.png
        :height: 728px
        :width: 901px
        :scale: 75%
        :align: center

Setting :math:`y=0` gives

.. math::

    -f(x_n)=f'(x_n)(x-x_n)\Rightarrow x=x_n-\frac{f(x_n)}{f'(x_n)}=x_{n+1}

Ultimately, Newton's method reduces to: 

.. math::
    x_{n+1}=x_n-\frac{f(x_n)}{f'(x_n)}
    :label: newton

Our previous example (square root of :math:`a`) is just an application of Newton's
method to the nonlinear equation :math:`f(x)=x^2-a=0`. Applying equation
:eq:`newton` gives:

.. math::

    x_{k+1}=x_k-\frac{f(x_k)}{f'(x_k)}=x_k-\frac{x_k^2-a}{2x_k}=\frac{2x_k^2-x_k^2+a}{2x_k}=\frac{x_k^2+a}{2x_k}

which is the same iteration we considered previously.
A few comments about Newton's method:

*   It requires the function :math:`f(x)` to be not only continuous, but differentiable as
    well. We will later see variants that do not *explicitly* require knowledge
    of :math:`f'`. This would be an important consideration if the formula for :math:`f'(x)` is
    significantly more complex and expensive to evaluate than :math:`f(x)`, or if we
    simply do not possess an analytic expression for :math:`f'` (this could be the case if
    :math:`f(x)` is not given to us via an explicit formula, but only defined via a
    black-box computer function that computes the value).

*   If we ever have an approximation :math:`x_k` with :math:`f'(x_k)\approx 0`, we should expect
    problems, especially if we are not close to a solution (we would be nearly
    dividing by zero). In such cases, the tangent line is almost (or exactly)
    horizontal. Thus, the next iterate can be a very remote value and convergence
    may be far from guaranteed.

    .. image:: images/newton-convergence.png
        :height: 766px
        :width: 1218px
        :scale: 50%
        :align: center


