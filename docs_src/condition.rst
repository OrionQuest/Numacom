Matrix Norms and Condition Numbers
----------------------------------

Similar to vectors, norms can also be defined for (square) matrices. These norms
allow us to measure the *nicety* of a linear system in terms of admitting stable
numerical algorithms. It turns out these norms allow us to precisly quantify the
convergence behavior of many iterative schemes, as we will see in later
sections.

Matrix Norms
~~~~~~~~~~~~

.. topic:: Definition

    A matrix norm is a function :math:`\lVert\cdot\rVert : \mathbb R^{n\times n}\rightarrow \mathbb R` that satisfies:

    1. :math:`\lVert M\rVert\geq 0` for all :math:`M\in\mathbb R^{n\times n}`, :math:`\lVert M\rVert = 0`
       if and only if :math:`M=O`.
    2. :math:`\lVert \alpha M\rVert = \vert\alpha\vert\cdot\lVert M\rVert`
    3. :math:`\lVert M+N\rVert\leq \lVert M\rVert + \lVert N\rVert`
    4. :math:`\lVert M\cdot N\rVert \leq \lVert M\rVert\cdot\lVert N\rVert`

Property :math:`(4)` above has slightly different flavor than vector
norms. Although more types of matrix norms exist, one common category is that of
matrix norms *induced by* vector norms.

.. topic:: Definition

    If :math:`\lVert\cdot\rVert_\star` is a valid vector norm, its
    *induced* matrix norm is defined as:

    .. math::
        \lVert M\rVert_\star = \max_{x\in\mathbb R^n,x\neq 0} \frac{\lVert Mx\rVert_\star}{\lVert x\rVert_\star}

    or equivalently,

    .. math::
        \lVert M\rVert_\star = \max_{x\in\mathbb R^n,\lVert x\rVert=1} \lVert Mx\rVert_\star

Note again, that *not all* valid matrix norms are induced by vector norms. One
notable example is the very commonly used *Frobenius norm*:

.. math::
    \lVert M\rVert_F = \sqrt{\sum_{i,j=1}^n M_{ij}^2}

We can easily show that induced norms satify properties :math:`(1)` through
:math:`(4)`. Properties :math:`(1)-(3)` are rather trivial, for example,

.. math::
    \lVert M+N\rVert &=& \max_{x\neq 0} \frac{\lVert (M+N)x\rVert}{\lVert x\rVert} \leq \max_{x\neq 0} \frac{\lVert Mx\rVert + \lVert Nx\rVert}{\lVert x\rVert} \\
                     &=& \max_{x\neq 0} \frac{\lVert Mx\rVert}{\lVert x\rVert} + \max_{x\neq 0} \frac{\lVert Nx\rVert}{\lVert x\rVert} = \lVert M\rVert + \lVert N\rVert

Property :math:`(4)` is slightly trickier to show. First, a lemma:

.. topic:: Lemma

    If :math:`\lVert\cdot\rVert` is a matrix norm induced by a vector
    norm :math:`\lVert\cdot\rVert`, then

    .. math::
        \lVert Ax\rVert \leq \lVert A\rVert\cdot \lVert x\rVert
        :label: vector-norm-inequality

    *Proof:* Since :math:`\lVert A\rVert = \max_{x\neq 0}\lVert Ax\rVert/\lVert x\rVert`, we have that for an arbitrary :math:`y\in\mathbb R^n (y\neq 0)`

    .. math::
        \lVert A\rVert = \max_{x\neq 0}\frac{\lVert Ax\rVert}{\lVert x\rVert}\geq \frac{\lVert Ay\rVert}{\lVert y\rVert} \Rightarrow \lVert Ay\rVert \leq \lVert A\rVert\cdot\lVert y\rVert

    This holds for :math:`y\neq 0`, but we can see that it is also true for :math:`y=0`.

Now property :math:`(4)` can be easily proved using the above lemma:

.. math::
    \lVert MN\rVert &=& \max_{\lVert x\rVert=1} \lVert MNx\rVert \leq \max_{\lVert x\rVert=1} \lVert M\rVert\cdot \lVert Nx\rVert \\
                    &=& \lVert M\rVert\cdot \max_{\lVert x\rVert=1} \lVert Nx\rVert = \lVert M\rVert\cdot\lVert N\rVert \\
    \Rightarrow \lVert MN\rVert &\leq& \lVert M\rVert\cdot\lVert N\rVert

Note that when writing an expression such as :eq:`vector-norm-inequality`, the
matrix norm :math:`\lVert A\rVert` is understood to be the inferred norm from the
vector norm used in :math:`\lVert Ax\rVert` and :math:`\lVert x\rVert`. Thus,

.. math::
    \lVert Ax\rVert_1 \leq \lVert A\rVert_1\cdot \lVert x\rVert_1

and

.. math::
    \lVert Ax\rVert_\infty \leq \lVert A\rVert_\infty\cdot \lVert x\rVert_\infty

are both valid, but we *cannot* mix and match, for example:

.. math::
    \lVert Ax\rVert_\infty \leq \lVert A\rVert_2\cdot \lVert x\rVert_1

Although the definition of an induced norm allowed us to prove certain
properties, it does not necessarily provide a convenient formula for evaluating
the matrix norm. Fortunately, such formulas do exist for the :math:`L_1` and
:math:`L_\infty` induced matrix norms. Given here (without proof):

.. math::
    \lVert A\rVert_1        &=& \max_j \sum_{i=1}^n \vert A_{ij}\vert \enspace\enspace\enspace\mbox{(maximum absolute column sum)} \\
    \lVert A\rVert_\infty   &=& \max_i \sum_{i=1}^n \vert A_{ij}\vert \enspace\enspace\enspace\mbox{(maximum absolute row sum)}

The formula for the :math:`L_2` induced matrix norm is more complicated. We will see it when we study eigenvalues.

Condition Numbers
~~~~~~~~~~~~~~~~~

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
  *are* some special cases where an estimate of :math:`\lVert A^{-1}\rVert` can be obtained.

A Different Source of Error
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Sometimes, the right hand side :math:`b` of the system of equations :math:`Ax=b`
has errors that make it deviate from its intended value. For example, if each
component of :math:`b` was defined as :math:`b_i=f(x_i)`, where :math:`f` is an
unknown function, then an error in a 
measuring device that was supposed to sample :math:`f(x)` could lead to
erroneous readings :math:`b_i^\star (\neq b_i)`. Thus,
measuring inaccuracies can lead to the right hand side vector :math:`b` being
misrepresented as :math:`b^\star`. In this case, instead of the
intended solution :math:`x=A^{-1}b`, we compute the solution to a
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
error in :math:`b`. This multiplicative constant :math:`\kappa (A)=\lVert A\rVert\cdot\lVert A^{-1}\rVert`
is called the *condition number* of :math:`A`, and is an important measure of
the sensitivity of a linear system :math:`Ax=b` to being solved on a computer
in the presence of inaccurate values.

Why is all this relevant?
~~~~~~~~~~~~~~~~~~~~~~~~~

Simply put, *any* :math:`b` will have *some* small relative error due to the
fact that it is represented on a computer only up to machine precision. The relative
error will be at least as much as the machine epsilon due to round-off.

.. math::
    \frac{\lVert\delta b\rVert_\infty}{\lVert b\rVert_\infty} \geq\varepsilon\approx 10^{-7} \enspace\enspace\enspace\enspace\mbox{(in single precision)}

But how bad can the condition number get? *Very bad* at times. For example,
`Hilbert matrices <https://en.wikipedia.org/wiki/Hilbert_matrix>`_
:math:`H_n\in\mathbb R^{n\times n}` are defined as:

.. math::
    (H_n)_{ij} = \frac{1}{i+j-1}

Considering a specific instance for :math:`n=5`,

.. math::
    H_5=\left[\begin{array}{ccccc}
    1 & 1/2 & 1/3 & 1/4 & 1/5 \\
    1/2 & 1/3 & 1/4 & 1/5 & 1/6 \\
    1/3 & 1/4 & 1/5 & 1/6 & 1/7 \\
    1/4 & 1/5 & 1/6 & 1/7 & 1/8 \\
    1/5 & 1/6 & 1/7 & 1/8 & 1/9
    \end{array}\right], \enspace\enspace\enspace\enspace\enspace \kappa_\infty(H_5) = \lVert H_5\rVert_\infty\cdot\lVert H_5^{-1}\rVert_\infty\approx 10^{6}

Thus, any attempt at solving :math:`H_5 x = b` would be subject to a relative
error of up to :math:`10\%` *just due to* round-off errors in :math:`b`! Another
case is that of near-singular matrices, for example:

.. math::
    A=\left[\begin{array}{cc}
    1 & 2 \\
    3 & 6+\varepsilon
    \end{array}\right]

As :math:`\varepsilon\rightarrow 0`, the matrix :math:`A` becomes *singular*
(non-invertible). In this case, :math:`\kappa (A)\rightarrow\infty`.

So far, we have considered upper bounds on the condition number. One may also
ask what is the best case scenario for :math:`\kappa (A)`? Before we answer this
question, a lemma:

.. topic:: Lemma

    For any vector-induced matrix norm, :math:`\lVert I\rVert = 1`.

    *Proof:*  From the definition,

    .. math::
        \lVert I\rVert = \max_{x\neq 0}\frac{\lVert Ix\rVert}{\lVert x\rVert} = \max_{x\neq 0} \frac{\lVert x\rVert}{\lVert x\rVert} = 1

Using property (4) of matrix norms, we have:

.. math::
    I = A\cdot A^{-1} \Rightarrow 1 = \lVert I\rVert = \lVert A\cdot A^{-1}\rVert \leq \lVert A\rVert\cdot\lVert A^{-1}\rVert

Thus, :math:`\kappa (A)\geq 1`. The "best" conditioned matrices are of the form
:math:`A=c\cdot I`, where :math:`c\in\mathbb R` is a non-zero constant, and have
:math:`\kappa (A)=1`. The ``linalg`` package of `NumPy <http://www.numpy.org/>`_
has an in-built function ``cond`` for computing the condition number of any square matrix, as
shown below. The second parameter specifies the particular norm to use
for evaluating the condition number. ::

    >>> a = np.matrix([[1,0,-1],[0,1,0],[1,0,1]])
    >>> a
    matrix([[ 1,  0, -1],
            [ 0,  1,  0],
            [ 1,  0,  1]])
    >>> np.linalg.cond(a,1)
    2.0
    >>> np.linalg.cond(a,2)
    1.4142135623730951
    >>> np.linalg.cond(a,np.inf)
    2.0
