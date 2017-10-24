Overdetermined Systems
----------------------

So far, we considered linear systems :math:`Ax=b` with the *same* number of
equations and unknowns (i.e., :math:`A\in\mathbb R^{n\times n}`). In the case where
:math:`A\in\mathbb R^{m\times n}`, with :math:`m>n` (more equations than unknowns) the existence of a
true solution is not guaranteed, in this case we look for the "best possible"
substitute for a solution. Before analyzing what that means, let's look at how
such problems arise.

As an example, in an experiment, we measure the pressure of a gas in a closed container as a
function of the temperature. From Physics, we know that

.. math::
    pV &=& \enspace nR\frac{5}{9}(T+459.67) \\
    \Rightarrow p&=& \enspace\alpha T+\beta, \enspace\enspace\enspace \alpha=\frac{5nR}{9V}, \beta=\frac{5nR\cdot 459.67}{9V}

What are :math:`\alpha` and :math:`\beta`? Experimentally, the measurements should ideally
lie on a straight line :math:`y=c_1x+c_0`, but do not, due to measurement error. If we
have :math:`n` measurement pairs :math:`(x_1,y_1),\ldots,(x_n,y_n)` we would have wanted:

.. math::
    \left.
    \begin{array}{ccccc}
    y_1 & = & c_1x_1 & + & c_0 \\
    y_2 & = & c_1x_2 & + & c_0 \\
        & \vdots & & & \\
    y_n & = & c_1x_n & + & c_0
    \end{array}\right\}\Rightarrow\left[
    \begin{array}{cc}
    x_1 & 1 \\
    x_2 & 1 \\
    \vdots & \\
    x_n & 1
    \end{array}
    \right]\left[
    \begin{array}{c}
    c_1 \\
    c_0
    \end{array}
    \right]=\left[
    \begin{array}{c}
    y_1 \\
    y_2 \\
    \vdots \\
    y_n
    \end{array}
    \right]

Here, :math:`A_{n\times2}x_{2\times1}=b_{n\times1}` is a rectangular system. We cannot
hope to find a true solution to this system. Instead, lets try to find an
"approximate" solution, such that :math:`Ax\approx b`. Lets look at the residual of
this "interpolation". The residual of the approximation of each data point is:

.. math::
    r_i=y_i-f(x_i)=y_i-c_1x_i-c_0

If we write the vector of all residuals:

.. math::
    r=\left[
    \begin{array}{c}
    r_1 \\
    r_2 \\
    \vdots \\
    r_n
    \end{array}
    \right]=\left[
    \begin{array}{c}
    y_1-c_1x_1-c_0 \\
    y_2-c_1x_2-c_0 \\
    \vdots \\
    y_n-c_1x_n-c_0 \\
    \end{array}
    \right]=\left[
    \begin{array}{c}
    y_1 \\
    y_2 \\
    \vdots \\
    y_n
    \end{array}
    \right]-\left[
    \begin{array}{cc}
    x_1 & 1 \\
    x_2 & 1 \\
    \vdots & \\
    x_n & 1
    \end{array}
    \right]\left[
    \begin{array}{c}
    c_1 \\
    c_0
    \end{array}
    \right]=b-Ax

Although we can't find an :math:`x` such that :math:`Ax=b` (thus, :math:`r=0`), we can at least
try to make :math:`r` *small*. As another example, consider the problem of finding the best parabola
:math:`f(x)=c_2x^2+c_1x+c_0` that fits measurements :math:`(x_1,y_1),\ldots,(x_n,y_n)`. We
would like

.. math::
    \left.
    \begin{array}{c}
    f(x_1)\approx y_1 \\
    f(x_2)\approx y_2 \\
    \vdots \\
    f(x_n)\approx y_n \\
    \end{array}
    \right\}=
    \left.
    \begin{array}{c}
    c_2x_1^2+c_1x_1+c_0\approx y_1 \\
    c_2x_2^2+c_1x_2+c_0\approx y_2 \\
    \vdots \\
    c_2x_n^2+c_1x_n+c_0\approx y_n \\
    \end{array}
    \right\}\Rightarrow
    \underbrace{
    \left[
    \begin{array}{ccc}
    x_1^2 & x_1 & 1 \\
    x_2^2 & x_2 & 1 \\
    & \vdots & \\
    x_n^2 & x_n & 1 \\
    \end{array}
    \right]}_A\underbrace{\left[
    \begin{array}{c}
    c_2 \\
    c_1 \\
    c_0
    \end{array}
    \right]}_x\approx\underbrace{\left[
    \begin{array}{c}
    y_1 \\
    y_2 \\
    \vdots \\
    y_n
    \end{array}
    \right]}_b

Once again, we would like to make :math:`r=b-Ax` as small as possible.

How do we quantify :math:`r` being small? :math:`\Rightarrow` using a norm! We could ask
that :math:`\lVert r\rVert_1, \lVert r\rVert_2` or :math:`\lVert r\rVert_\infty` be as small as possible. Any of these
norms would be intuitive to consider for minimization (especially :math:`1`- and
:math:`\infty`-norms are very intuitive). However, we typically use the :math:`2`-norm for
this purpose, because its the easiest to work with in this problem.

.. topic:: Definition

    The *least squares solution* of the
    overdetermined system :math:`Ax\approx b` is the vector :math:`x` that minimizes
    :math:`\lVert r\rVert_2=\lVert b-Ax\rVert_2`.

Define :math:`Q(x)=Q(x_1,x_2,\ldots,x_n)=\lVert b-Ax\rVert_2^2` where
:math:`x=(x_1,\ldots,x_n)` and :math:`A\in\mathbb R^{m\times n}, b\in\mathbb R^m` (:math:`m>n`).
The least squares solution is the set of values :math:`x_1,\ldots,x_n` that
*minimize* :math:`Q(x_1,x_2,\ldots,x_n)`.

.. math::
    Q(x_1,\ldots,x_n) &=& \enspace \lVert b-Ax\rVert_2^2=\lVert r\rVert_2^2=\sum_{i=1}^m r_i^2 \\
    r = b-Ax \Rightarrow r_i &=& \enspace b_i-(Ax)_i\Rightarrow r_i=b_i-\sum a_{ij}x_j \\
    \Rightarrow Q(x_1,\ldots,x_n) &=& \sum_{i=1}^m\left(b_i-\sum_{j=1}^n a_{ij}x_j\right)^2

If :math:`x_1\ldots,x_n` are those that *minimize* :math:`Q`, then:

.. math::
    \frac{\partial Q}{\partial x_1}=0,\frac{\partial Q}{\partial x_2}=0,\ldots,\frac{\partial Q}{\partial x_n}=0

in order to guarantee a minimum.

.. math::
    
    \frac{\partial Q}{\partial x_k} &=& \frac{\partial}{\partial x_k}\left(\sum_{i=1}^m \left(b_i-\sum_{j=1}^n a_{ij}x_j\right)^2\right) \\
                                    &=& \sum_{i=1}^m \frac{\partial}{\partial x_k}\left(b_i-\sum_{j=1}^n a_{ij}x_j\right)^2 \\
                                    &=& \sum_{i=1}^m 2\underbrace{\left(b_i-\sum_{j=1}^n a_{ij}x_j\right)}_{r_i}\frac{\partial}{\partial x_k}\left(b_i-\sum_{j=1}^n a_{ij}x_j\right) \\
                                    &=& \sum_{i=1}^m -2r_ia_{ik} = -2\sum_{i=1}^m [A^T]_{ki}r_i = -2[A^Tr]_k=0 \\
                                    &\Rightarrow& \enspace [A^Tr]_k=0

Thus,

.. math::

    \left.
    \begin{array}{ccccccc}
    \partial Q/\partial x_1 & = & 0 & \Rightarrow & [A^Tr]_1 & = & 0 \\
    \partial Q/\partial x_2 & = & 0 & \Rightarrow & [A^Tr]_2 & = & 0 \\
                                    &   &   & \vdots      &          &   & \\
    \partial Q/\partial x_n & = & 0 & \Rightarrow & [A^Tr]_n & = & 0 \\
    \end{array}
    \right\}\Rightarrow
    \boxed{A^Tr=0}

Since :math:`r=b-Ax`, we have:

.. math::
    0=A^Tr=A^T(b-Ax)=A^Tb-A^TAx\Rightarrow\boxed{A^TAx=A^Tb}

The system above is called the *normal equations system*; it is a *square*
system that has as solution the least-squares approximation of :math:`Ax\approx b`.

.. math::

    \underbrace{A^T_{n\times m}A_{m\times n}}_{n\times n} \underbrace{x_{n\times 1}}_{n\times 1}=\underbrace{A^T_{n\times m}b_{m\times 1}}_{n\times 1}

The normal equations *always* have a solution (with the simple condition
that the columns of :math:`A` have to be linearly independent, which is usually true).

:math:`QR` factorization
~~~~~~~~~~~~~~~~~~~~~~~~

While the normal equations can adequately compute the least squares solution,
the condition number of :math:`A^TA` is the *square* of that of :math:`A` (if
:math:`A` was a square matrix). An alternative method that does not suffer from
this problematic conditioning is :math:`QR` factorization.

.. topic:: Definition

    An :math:`n\times n` matrix :math:`Q` is called *orthonormal* if and only if

    .. math::

        Q^TQ=QQ^T=I

.. topic:: Theorem

    Let :math:`A\in\mathbb R^{m\times n}` (:math:`m>n`) have linearly independent columns. Then
    a decomposition :math:`A=QR` exists, such that :math:`Q\in\mathbb R^{m\times m}` is
    orthonormal and :math:`R\in\mathbb R^{m\times n}` is upper triangular, i.e.,

    .. math::
        
        R=\left(
        \begin{array}{c}
        \hat R \\
        O
        \end{array}
        \right)

    where :math:`\hat R` is an :math:`n\times n` upper triangular matrix. Additionally, given
    that :math:`A` has linearly independent columns, all diagonal elements :math:`r_{ii}\neq 0`.

Now, let us write

.. math::
    
    Q=\left[
    \begin{array}{c|c}
    \hat Q & Q^\star
    \end{array}
    \right]

where :math:`\hat Q\in\mathbb R^{m\times n}` contains the first :math:`n` columns of :math:`Q` and
:math:`Q^\star\in\mathbb R^{m\times (m-n)}`  contains the last :math:`(m-n)` columns.
Respectively, we write:

.. math::

    R=\left(
    \begin{array}{c}
    \hat R \\
    O
    \end{array}
    \right)

where :math:`\hat R\in\mathbb R^{n\times n}` (and upper triangular) contains the first
:math:`n` rows of :math:`R`. :math:`\hat R` is also *non-singular* because it has linearly
independent columns. We can verify the following:

.. math::

    \hat Q^T\hat Q=I_{n\times n}\enspace\enspace\enspace(\mbox{although } \hat Q\hat Q^T\neq I_{m\times m}!)

The factorization :math:`A=\hat Q\hat R` is the so-called *economy size* :math:`QR`
factorization. Once we have :math:`\hat Q` and :math:`\hat R` computed, we observe that the
normal equations can be written as:

.. math::

    A^TAx &=& \enspace A^Tb \nonumber \\
    \Rightarrow \hat R^T\underbrace{\hat Q^T\hat Q}_{=I_{m\times m}}\hat Rx &=& \enspace \hat R^T\hat Q^Tb \nonumber \\
    \Rightarrow \hat R^T\hat Rx &=& \enspace \hat R^T\hat Q^Tb \nonumber \\
    \Rightarrow \boxed{\hat Rx=\hat Q^Tb}

The last equality follows because :math:`\hat R` is invertible. The benefit of using the :math:`QR` factorization
is that :math:`\textsf{cond}(A^TA)=[\textsf{cond}(\hat R)]^2`.
Thus, the resulting equation is *much better* conditioned than the
normal equations.
