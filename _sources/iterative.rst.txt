Iterative Methods
-----------------

The general idea for iterative methods proceeds as follows:

* We write a (matrix) equation:

  .. math::
    x = Tx + c

  in such a way that this equation is equivalent to solving :math:`Ax=b`.

* We start with an initial guess :math:`x^{(0)}` for the solution of :math:`Ax=b`.

* We iterate

  .. math::
    x^{(k+1)} = Tx^{(k)} + c

* If properly designed the sequence :math:`x^{(0)},x^{(1)},\ldots,x^{(k)},\ldots`
  *converges* to :math:`x^\star`, which satisfies :math:`x^\star = Tx^\star + c`
  and consequently :math:`Ax^\star = b`.

The Jacobi Method
~~~~~~~~~~~~~~~~~

We decompose

.. math::
    A = D - L - U

where :math:`D` is the diagonal part, :math:`L` is the lower triangular part,
and :math:`U` is the upper triangular part. Substituting this expression in
:math:`Ax=b` gives us the following equation:

.. math::
    (D-L-U)x        & = & \enspace b \\
    \Rightarrow Dx  & = & \enspace (L+U)x + b \\
    \Rightarrow x   & = & \enspace \underbrace{D^{-1}(L+U)}_{T}x+\underbrace{D^{-1}b}_c \enspace\enspace\enspace (x=Tx+c)

The above equation can be cast into the iteration :math:`\boxed{x^{(k+1)}=D^{-1}(L+U)x^{(k)}+D^{-1}b}` or :math:`\boxed{Dx^{(k+1)}=(L+U)x^{(k)}+b}`

* **Solution** Easy, since we need to solve a linear system of equations with diagonal coefficient matrix

  .. math::
    \left[
    \begin{array}{cccc}
    d_1 & & & \\
    & d_2 & & \\
    & & \ddots & \\
    & & & d_n
    \end{array}
    \right]
    \left[
    \begin{array}{c}
    x_1^{(k+1)} \\
    x_2^{(k+1)} \\
    \vdots \\
    x_n^{(k+1)}
    \end{array}
    \right]=\left[
    \begin{array}{c}
    c_1 \\
    c_2 \\
    \vdots \\
    c_n
    \end{array}
    \right] \Rightarrow x_i^{(k+1)}=\frac{c_i}{d_i}

* **Convergence** The Jacobi method if *guaranteed* to converge when :math:`A` is
  diagonally dominant by rows.

* **Complexity** Each iteration has a cost associated with:

    1. Solving :math:`Dx^{(k+1)}=c` which requires :math:`n` divisions.
    2. Computing :math:`x=(L+U)x^{(k)}+b` which requires as many additions and
       multiplications as *non-zero* entries in :math:`A` (worst case :math:`O(n^2)`, but
       could be :math:`O(n)` for sparse matrices).

* **Stopping criteria** :math:`||b-Ax^{(k)}||<\varepsilon` or :math:`||x^{(k+1)}-x^{(k)}||<\varepsilon`

There are three forms of this algorithm we will see, for different purposes:

1. Matrix form (for proofs) :math:`Dx^{(k+1)}=(L+U)x^{(k)}+b`.
2. Algorithm form (without in-place update). Each row of :math:`Dx^{(k+1)}=(L+U)x^{(k)}+b` can be written as:

   .. math::

    a_{ii}x_i^{(k+1)} &=& \enspace b_i-\sum_{j\neq i} a_{ij}x_j^{(k)} \\
    \Rightarrow x_i^{(k+1)} &=& \enspace \frac{1}{a_{ii}}\left(b_i-\sum_{j\neq i}a_{ij}x_j^{(k)}\right)

   Note that memory requirements in this version are high, as every iteration
   :math:`k` stores a new copy of the solution vector :math:`x^{(k)}`.

3. In-place algorithm, maintains two copies :math:`x, x^\textsf{new}`
   of the solution vector, and uses the following update rule:

   .. math::

    x_i^{\textsf{new}} \leftarrow \frac{1}{a_{ii}}\left(b_i-\sum_{j\neq i}a_{ij}x_j\right)

The Gauss-Seidel Method
~~~~~~~~~~~~~~~~~~~~~~~

We again employ the decomposition :math:`A = D-L-U` for solving :math:`Ax=b`:

.. math::
    (D-L-U)x            & = & \enspace b \\
    \Rightarrow (D-L)x  & = & \enspace Ux + b

At this point, we place :math:`x^{(k+1)}` on the left hand side and :math:`x^{(k)}` on
the right hand side

.. math::
    \boxed{(D-L)x^{(k+1)}=Ux^{(k)}+b}
    :label: gauss-seidel

The benefit of the Gauss-Seidel method :eq:`gauss-seidel` over Jacobi is
the improved convergence. In terms of complexity, each iteration of equation
:eq:`gauss-seidel` amounts to solving a lower triangular system via forward
substitution, i.e., it incurs a cost of :math:`O(k)`, where :math:`k` is the
number of non-zero entries in :math:`A`. In terms of update, equation
:eq:`gauss-seidel` takes the following form:

* Without in-place update.

  .. math::
    x_i^{(k+1)} \leftarrow \frac{1}{a_{ii}}\left(b_i-\sum_{j<i}a_{ij}x_j^{(k+1)}-\sum_{j>i}a_{ij}x_j^{(k)}\right)

  Once again, this version incurs a high memory overhead because a new solution
  vector :math:`x^{(k)}` is created for every iteration :math:`k`.

* In place update, which as before, maintains only two copies
  :math:`x,x^\textsf{new}` of the solution vector.

  .. math::
    x_i^{\textsf{new}} \leftarrow \frac{1}{a_{ii}}\left(b_i-\sum_{j<i}a_{ij}x_j^{\textsf{new}}-\sum_{j>i}a_{ij}x_j\right)

  Compare the above in-place update with that for Jacobi.

The real difference in performance is that Gauss-Seidel is generally
*serial* in nature (although parallel variants do exist), while Jacobi is
*highly parallel*.
