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
misrepresented as :math:`b^\star (\neq b)`.
