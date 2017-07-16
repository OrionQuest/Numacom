Condition Numbers
-----------------

When solving a linear system :math:`Ax=b`, computer algorithms are only
providing an approximation :math:`x_\textsf{approx}` to the exact solution
:math:`x_\textsf{exact}`. This is due to factors such as finite precision,
round-off errors, or even imperfect solution algorithms. In either case, we have
an *error* (in fact, an error vector) defined as:

.. math::
    e = x_\textsf{approx} - x_\textsf{exact}

Naturally, we would like to have an understanding of the *magnitude* of this
error (for example, some appropriate norm :math:`\lVert e\rVert`). However, the
error cannot be directly measured because the exact solution :math:`x_\textsf{exact}` is unknown.

One remedy is offered via the *residual vector* defined as:

.. math::
    r = b-Ax_\textsf{approx}

The vector :math:`r` is something we *can* compute practically since it involves
only the known quantities :math:`b, A, x_\textsf{approx}`. Moreover, we have:

.. math::
    r               \enspace &=& \enspace b-Ax_\textsf{approx} \nonumber \\
                    \enspace &=& \enspace Ax_\textsf{exact} - Ax_\textsf{approx} \\
                    \enspace &=& \enspace -A(x_\textsf{approx} - x_\textsf{exact}) \\
                    \enspace &=& \enspace -Ae \\
    \Rightarrow r   \enspace &=& \enspace -Ae \\
    \Rightarrow e   \enspace &=& \enspace -A^{-1}r
    :label: error-vs-residual

Equation :eq:`error-vs-residual` links the error with the residual. This allows
us to write:

.. math::
    \lVert e\rVert = \lVert A^{-1}r\rVert \leq \lVert A^{-1}\rVert\cdot\lVert r\rVert

This equation provides a *bound* for the error, as a function of :math:`\lVert A^{-1}\rVert`
and the norm of the computable vector :math:`r`. Note that:

* We can obtain this estimate *without* knowing the exact solution, but
* We need :math:`\lVert A^{-1}\rVert` and generally, computing :math:`\lVert A^{-1}\rVert`
  is just as difficult (if not more) than finding :math:`x_\textsf{exact}`. However, there
  *are* special cases where an estimate of :math:`\lVert A^{-1}\rVert` can be obtained.

A Different Source of Error
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Sometimes, the right hand side :math:`b` of the system of equations :math:`Ax=b`
has errors that make it deviate from its intended value. For example, in the
Vandermonde matrix method for polynomial interpolation, :math:`b` contains the
samples :math:`(y_1,y_2,\ldots,y_n)`, where :math:`y_i = f(x_i)`. An error in a
measuring device that was supposed to sample :math:`f(x)` could lead to
erroneous readings :math:`y_i^\star` instead of :math:`y_i`. In general,
measuring inaccuracies can lead to the right hand side vector :math:`b` being
misrepresented as :math:`b^\star (\neq b)`. In this case, instead of the
intended solution :math:`x=A^{-1}b`, we in fact compute the solution to a
different system :math:`x^\star=A^{-1}b^\star`. How important is the error
:math:`e=x^\star-x` that is caused by this misrepresentation of :math:`b`?
Let :math:`\delta b=b^\star-b, \delta x=x^\star-x,Ax=b,Ax^\star=b^\star`. Then,
we have:

.. math::
    A(x^\star-x)            \enspace &=& \enspace b^\star-b \\
    A\delta x               \enspace &=& \enspace \delta b \\
    \Rightarrow \delta x    \enspace &=& \enspace A^{-1}\delta b

Taking norms,

.. math::
    \lVert \delta x\rVert = \lVert A^{-1}\delta b\rVert \leq \lVert A^{-1}\rVert\cdot\lVert \delta b\rVert
    :label: error-norm

Thus, the error in the computed solution :math:`\delta x` is proportional to the
error in :math:`b`. An even more relevant question is: how does the *relative*
error :math:`\lVert \delta x\rVert/\lVert x\rVert = \lVert
x^\star-x\rVert/\lVert x\rVert` compare to the relative error in :math:`b`
(:math:`\lVert\delta b\rVert/\lVert b\rVert`)? This may be more useful to know,
since :math:`\lVert\delta b\rVert` may be impossible to compute (if we don't
know the real :math:`b`). For this, we write:

.. math::
    Ax = b  &\Rightarrow& \lVert b\rVert = \lVert Ax\rVert \leq \lVert A\rVert\cdot\lVert x\rVert \\
            &\Rightarrow& \frac{1}{\lVert x\rVert} \leq \lVert A\rVert\cdot\frac{1}{\lVert b\rVert}
    :label: error-reciprocal

Multiplying equation :eq:`error-norm` and :eq:`error-reciprocal` gives

.. math::
    \frac{\lVert\delta x\rVert}{\lVert x\rVert} \leq \underbrace{\lVert A\rVert\cdot\lVert A^{-1}\rVert}_{\kappa (A)}\cdot\frac{\lVert \delta b\rVert}{\lVert b\rVert}

Thus, the relative error in :math:`x` is bounded by a multiple of the relative
error in :math:`b`. Thus multiplicative constant :math:`\kappa (A)=\lVert A\rVert\cdot\lVert A^{-1}\rVert`
is called the *condition number* of :math:`A`, and is an important measure of
the sensitivity of a linear system :math:`Ax=b` to being solved on a computer
in the presence of inaccurate values.

Why is all this relevant?
~~~~~~~~~~~~~~~~~~~~~~~~~

Simply put, *any* :math:`b` will have *some* small relative error due to the
fact that it is represented on a computer up to machine precision. The relative
error will be at least as much as the machine epsilon due to round-off.

.. math::
    \frac{\lVert\delta b\rVert_\infty}{\lVert b\rVert_\infty} \geq\varepsilon\approx 10^{-7} \enspace\enspace\enspace\enspace\mbox{(in single precision)}
