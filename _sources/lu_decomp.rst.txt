LU Decomposition
----------------

The forward and backward substitution algorithms can be used to solve a
*non-triangular* system by virtue of the following factorization property:

.. topic:: Theorem 1

    If :math:`A` is an :math:`n\times n` matrix, it can be (generally) written as a product

    .. math::
        A = LU

    where :math:`L` is a lower triangular matrix and :math:`U` is an upper
    triangular matrix. Furthermore, it is possible to construct :math:`L` such
    that all diagonal elements :math:`l_{ii}=1`.

The code below outlines the *Gaussian Elimination* algorithm to compute the :math:`LU` factorization of an
:math:`n\times n` matrix. ::

    import numpy as np

    # LU decomposition of square systems
    def Gaussian_Elimination(A):
        m=A.shape[0]
        n=A.shape[1]
        if(m!=n):
            print 'Matrix is not square!'
            return
        for k in range(0,n-1):
            if A[k,k] == 0:
                return
            for i in range(k+1,n):
                A[i,k]=A[i,k]/A[k,k]
            for j in range(k+1,n):
                for i in range(k+1,n):
                    A[i,j]-=A[i,k]*A[k,j]

Note that the algorithm above executes *in-place*, i.e., the matrix :math:`A` is
*replaced by* its :math:`LU` factorization, in compact form. More specifically,
this algorithm produces a factorization :math:`A=LU`, where:

.. math::

    L=\left[
    \begin{array}{cccccc}
    1 & & & & & \\
    l_{21} & 1 & & & O & \\
    l_{31} & l_{32} & 1 & & & \\
    l_{41} & l_{42} & l_{43} & 1 & & \\
    \vdots & \vdots & \vdots & & \ddots & \\
    l_{n1} & n_{n2} & l_{n3} & \ldots & l_{n,n-1} & 1
    \end{array}
    \right],\enspace\enspace U=\left[
    \begin{array}{ccccc}
    u_{11} & u_{12} & u_{13} & \ldots & u_{1n} \\
    & u_{22} & u_{23} & \ldots & u_{2n} \\
    & & u_{33} & \ldots & u_{3n} \\
    & O & & \ddots & u_{n-1,n} \\
    & & & & u_{nn}
    \end{array}
    \right]

After the in-place factorization algorithm completes, :math:`A` is replaced by
the following *compacted* encoding of :math:`L` and :math:`U` together:

.. math::
    A=\left[
    \begin{array}{ccccc}
    u_{11} & u_{12} & u_{13} & \ldots & u_{1n} \\
    l_{21} & u_{22} & u_{23} & \ldots & u_{2n} \\
    l_{31} & l_{32} & u_{33} & \ldots & u_{3n} \\
    \vdots & \vdots & \vdots & \ddots & \vdots \\
    l_{n1} & l_{n2} & \ldots & l_{n-1,n} & u_{nn}
    \end{array}
    \right]

.. topic:: Example

    Consider the matrix shown below. 

    .. math::
        \left[\begin{array}{ccc}
        2 & 4 & -2 \\
        4 & 9 & -3 \\
        -2 & -3 & 7
        \end{array}\right]

    Let us append the following code to the
    Gaussian Elimination algorithm outlined above to compute the corresponding :math:`LU` factorization: ::

        def main():
            A=np.matrix([[2,4,-2],[4,9,-3],[-2,-3,7]])
            Gaussian_Elimination(A)
            print A
        
        if __name__ == "__main__":
            main()

    Upon execution, it produces the following result: ::

        [[ 2  4 -2]
         [ 2  1  1]
         [-1  1  4]]
       
    As stated above, the factorization is *in-place*, and so the result should be
    interpreted as:

    .. math::
        L = \left[\begin{array}{ccc}
        1 & 0 & 0 \\
        2 & 1 & 0 \\
        -1 & 1 & 1
        \end{array}\right],\enspace\enspace\enspace
        U=\left[\begin{array}{ccc}
        2 & 4 & -2 \\
        0 & 1 & 1 \\
        0 & 0 & 4
        \end{array}\right]

Elimination Matrices
~~~~~~~~~~~~~~~~~~~~

Here is a slightly different algorithm for computing the :math:`LU`
factorization of an :math:`n\times n` matrix by using *elimination matrices*.
Define the :math:`n\times 1` basis vector :math:`e_k` as

.. math::
    e_k=\left(
    \begin{array}{c}
    0 \\
    \vdots \\
    0 \\
    1 \\
    0 \\
    \vdots \\
    0
    \end{array}
    \right)

where the :math:`1` is in the :math:`k^{th}` row and the length of
:math:`e_k` is :math:`n`. In order to perform Gaussian Elimination on the
:math:`k^{th}` column :math:`a_k` of :math:`A`, we define the
:math:`n\times n` elimination matrix :math:`M_k = I-m_ke_k^T` where

.. math::
    m_k=\frac{1}{a_{kk}}\cdot\left(
    \begin{array}{c}
    0 \\
    \vdots \\
    0 \\
    a_{k+1,k} \\
    \vdots \\
    a_{n,k}
    \end{array}
    \right)

:math:`M_k` adds multiples of row :math:`k` to rows with index greater than :math:`k` in order to create zeroes. As an
example, for :math:`a_k=(2,4,-2)^T`

.. math::
    M_1a_k=\left[
    \begin{array}{ccc}
    1 & 0 & 0 \\
    -2 & 1 & 0 \\
    1 & 0 & 1
    \end{array}
    \right]
    \left[
    \begin{array}{c}
    2 \\
    4 \\
    -2
    \end{array}
    \right]=\left[
    \begin{array}{c}
    2 \\
    0 \\
    0
    \end{array}
    \right]

Similarly,

.. math::
    M_2a_k=\left[
    \begin{array}{ccc}
    1 & 0 & 0 \\
    0 & 1 & 0 \\
    0 & 1/2 & 1
    \end{array}
    \right]
    \left[
    \begin{array}{c}
    2 \\
    4 \\
    -2
    \end{array}
    \right]=\left[
    \begin{array}{c}
    2 \\
    4 \\
    0
    \end{array}
    \right]

The inverse of an elimination matrix is defined as
:math:`L_k=M_k^{-1}=I+m_ke_k^T`. For example,

.. math::
    L_1=M_1^{-1}=\left[
    \begin{array}{ccc}
    1 & 0 & 0 \\
    2 & 1 & 0 \\
    -1 & 0 & 1
    \end{array}
    \right],\enspace\mbox{and}\enspace L_2=M_2^{-1}=\left[
    \begin{array}{ccc}
    1 & 0 & 0 \\
    0 & 1 & 0 \\
    0 & -1/2 & 1
    \end{array}
    \right]

The algorithm now proceeds as follows. Consider the example:

.. math::
    \left[
    \begin{array}{ccc}
    2 & 4 & -2 \\
    4 & 9 & -3 \\
    -2 & -3 & 7
    \end{array}
    \right]
    \left[
    \begin{array}{c}
    x_1 \\
    x_2 \\
    x_3
    \end{array}
    \right]=\left[
    \begin{array}{c}
    2 \\
    8 \\
    10
    \end{array}
    \right]

First, we eliminate the lower triangular portion of :math:`A` one column at a time
using :math:`M_k` to get :math:`U=M_{n-1}\ldots M_1A`. Note that we also carry out the
operations on :math:`b` to get a new system of equations :math:`M_2M_1Ax=M_2M_1b` or
:math:`Ux=M_2M_1b` which can be solved for via back substitution.

.. math::
    M_1A=\left[
    \begin{array}{ccc}
    1 & 0 & 0 \\
    -2 & 1 & 0 \\
    1 & 0 & 1
    \end{array}
    \right]\left[
    \begin{array}{ccc}
    2 & 4 & -2 \\
    4 & 9 & -3 \\
    -2 & -3 & 7
    \end{array}
    \right]=\left[
    \begin{array}{ccc}
    2 & 4 & -2 \\
    0 & 1 & 1 \\
    0 & 1 & 5
    \end{array}
    \right]

.. math::

    M_1b=\left[
    \begin{array}{ccc}
    1 & 0 & 0 \\
    -2 & 1 & 0 \\
    1 & 0 & 1
    \end{array}
    \right]\left[
    \begin{array}{c}
    2 \\
    8 \\
    10
    \end{array}
    \right]=\left[
    \begin{array}{c}
    2 \\
    4 \\
    12
    \end{array}
    \right]

.. math::

    M_2M_1A=\left[
    \begin{array}{ccc}
    1 & 0 & 0 \\
    0 & 1 & 0 \\
    0 & -1 & 1
    \end{array}
    \right]\left[
    \begin{array}{ccc}
    2 & 4 & -2 \\
    0 & 1 & 1 \\
    0 & 1 & 5
    \end{array}
    \right]=\left[
    \begin{array}{ccc}
    2 & 4 & -2 \\
    0 & 1 & 1 \\
    0 & 0 & 4
    \end{array}
    \right]

.. math::

    M_2M_1b=\left[
    \begin{array}{ccc}
    1 & 0 & 0 \\
    0 & 1 & 0 \\
    0 & -1 & 1
    \end{array}
    \right]\left[
    \begin{array}{c}
    2 \\
    4 \\
    12
    \end{array}
    \right]=\left[
    \begin{array}{c}
    2 \\
    4 \\
    8
    \end{array}
    \right]

Finally, solve the following system via back substitution.

.. math::

    \left[
    \begin{array}{ccc}
    2 & 4 & -2 \\
    0 & 1 & 1 \\
    0 & 0 & 4
    \end{array}
    \right]\left[
    \begin{array}{c}
    x \\
    y \\
    z
    \end{array}
    \right]=\left[
    \begin{array}{c}
    2 \\
    4 \\
    8
    \end{array}
    \right]

Note that we can write :math:`LU=(L_1\ldots L_{n-1})(M_{n-1}\ldots M_1A)=A`
using the fact that the :math:`L` matrices are inverses of the :math:`M` matrices,
where :math:`L=L_1\ldots L_{n-1}` can be formed trivially from the :math:`M_k` to obtain:

.. math::

    L=L_1L_2=\left[
    \begin{array}{ccc}
    1 & 0 & 0 \\
    2 & 1 & 0 \\
    -1 & 0 & 1
    \end{array}
    \right]\left[
    \begin{array}{ccc}
    1 & 0 & 0 \\
    0 & 1 & 0 \\
    0 & 1 & 1
    \end{array}
    \right]=\left[
    \begin{array}{ccc}
    1 & 0 & 0 \\
    2 & 1 & 0 \\
    -1 & 1 & 1
    \end{array}
    \right]

And thus, although we never needed it to solve the equations, the :math:`LU`
factorization of :math:`A` is

.. math::
    A=\left[
    \begin{array}{ccc}
    2 & 4 & -2 \\
    4 & 9 & -3 \\
    -2 & -3 & 7
    \end{array}
    \right]=\left[
    \begin{array}{ccc}
    1 & 0 & 0 \\
    2 & 1 & 0 \\
    -1 & 1 & 1
    \end{array}
    \right]\left[
    \begin{array}{ccc}
    2 & 4 & -2 \\
    0 & 1 & 1 \\
    0 & 0 & 4
    \end{array}
    \right]=LU

Existence and Uniqueness
~~~~~~~~~~~~~~~~~~~~~~~~

When computing the :math:`LU` factorization, the algorithm will *halt* if the
diagonal element :math:`a_{kk}=0`. This can be avoided by swapping rows of
:math:`A` prior to computing the :math:`LU` factorization. This is done to
always select the largest :math:`a_{kk}` from the equations that follow. As an
example, consider the matrix :math:`A` and the action of the permutation matrix
:math:`P` on it.

.. math::
    A=\left[
    \begin{array}{cccc}
    1 & 2 & 5 & -1 \\
    0 & 0 & 3 & 1 \\
    0 & 4 & 1 & -2 \\
    0 & -6 & 0 & 3
    \end{array}
    \right],\enspace\enspace P=\left[
    \begin{array}{cccc}
    1 & 0 & 0 & 0 \\
    0 & 0 & 0 & 1 \\
    0 & 0 & 1 & 0 \\
    0 & 1 & 0 & 0
    \end{array}
    \right],\enspace\enspace PA=\left[
    \begin{array}{cccc}
    1 & 2 & 5 & -1 \\
    0 & -6 & 0 & 3 \\
    0 & 4 & 1 & -2 \\
    0 & 0 & 3 & 1
    \end{array}
    \right]

This is *pivoting*: the pivot :math:`a_{kk}` is selected to be non-zero. In this
process, we can guarantee existence and uniqueness of the :math:`LU` factorization.

.. topic:: Theorem 2

    If :math:`P` is a permutation matrix such that all pivots in the Gaussian
    Elimination of :math:`PA` are non-zero, then the :math:`LU` factorization
    exists and is unique.

    .. math::
        PA = LU

So far, we have seen two ways of solving the system :math:`Ax=b`:

* Without pivoting:
    
    .. math::

        A = L\underbrace{Ux}_{=y} = b

    (1) Solve :math:`Ly = b` through forward substitution.

    (2) Solve :math:`Ux = y` through backward substitution to obtain the
        solution :math:`x`.

    Note that if we have multiple systems :math:`Ax_i = b_i`, we only need to
    incur the cost of computing an :math:`LU` decomposition of :math:`A` once.

* With pivoting:

    .. math::

        Ax = b \Longleftrightarrow PAx = Pb

    (1) Solve :math:`Ly = Pb` using forward substitution.

    (2) Solve :math:`Ux = y` using backward substitution to obtain the solution
        :math:`x`.

Note that switching two rows twice puts the rows back, so :math:`P` is its own
inverse. Also, note that :math:`P` is an *orthogonal* matrix, i.e., :math:`P^{-1} = P^T`,
so in general, :math:`P^{-1} = P^T = P`. The process shown above is called
*partial pivoting* because it switches rows to always get the largest diagonal
element. This is in contrast to *full pivoting* (see below) which can switch
both rows and columns to obtain the largest diagonal element. Partial pivoting
gives :math:`A=LU`, where :math:`U=M_{n-1}P_{n-1}\ldots M_1P_1A` and
:math:`L=P_1L_1\ldots P_{n-1}L_{n-1}`. Note that :math:`U` is upper triangular, but
:math:`L` is a permutation of a lower triangular matrix. It turns out that we
can write :math:`L` as :math:`L=P_1\ldots P_{n-1}L_1^P\ldots L_{n-1}^P` where
each :math:`L_k^P=I+(P_{n-1}\ldots P_{k+1}m_k)e_k^T` has the same form as
:math:`L_k`. Thus, we can write :math:`PA = L^PU` where :math:`L^P=L_1^P\ldots L_{n-1}^P`
is *lower triangular* and :math:`P=P_{n-1}\ldots P_1` is the total permutation
matrix.

Full Pivoting
~~~~~~~~~~~~~

In this case, when we are in the :math:`k^{th}` step of the Gaussian
Elimination/:math:`LU` procedure, we pick the pivot element among the *entire*
:math:`(n-k+1)\times (n-k+1)` lower rightmost submatrix of :math:`A`. For
example, if :math:`k=2` and :math:`Ax=b`

.. math::

    \left[
    \begin{array}{cccc}
    1 & 2 & 5 & -1 \\
    0 & \boxed{0} & 3 & 1 \\
    0 & 4 & 1 & \boxed{-8} \\
    0 & -6 & 0 & 3
    \end{array}
    \right]\left[
    \begin{array}{c}
    x_1 \\
    x_2 \\
    x_3 \\
    x_4
    \end{array}
    \right]=\left[
    \begin{array}{c}
    4 \\
    7 \\
    8 \\
    2
    \end{array}
    \right]

In this case, we can bring :math:`(-8)` to the pivot position :math:`a_{22}` by
permuting *both* rows :math:`2-3` *and* columns :math:`2-4`. Naturally, we will
respectively swap rows :math:`2-3` of the right hand side :math:`b`, and rows
:math:`2-4` of the vector of unknowns :math:`x`. Thus, the equivalent system
becomes

.. math::
    \left[
    \begin{array}{cccc}
    1 & -1 & 5 & 2 \\
    0 & -8 & 1 & 4 \\
    0 & 1 & 3 & 0 \\
    0 & 3 & 0 & -6
    \end{array}
    \right]\left[
    \begin{array}{c}
    x_1 \\
    x_4 \\
    x_3 \\
    x_2
    \end{array}
    \right]=\left[
    \begin{array}{c}
    4 \\
    8 \\
    7 \\
    2
    \end{array}
    \right]

This process is encoded in the LU factorization using *two* permutation matrices
:math:`P` and :math:`Q` such that :math:`\boxed{PAQ=LU}`. The solution is then
computed via

.. math::
    
    Ax=b\Rightarrow PA\underbrace{QQ^T}_{=I}x=Pb\Rightarrow (LU)(Q^Tx)=Pb

(1) Solve :math:`Ly = Pb` using forward substitution.

(2) Solve :math:`Uz = y` using backward substitution.

(3) Finally, :math:`Q^Tx = z \Rightarrow QQ^T x = Qz \Rightarrow \boxed{x=Qz}`
    gives the solution.

To summarize:

* *Partial pivoting* permutes rows, such that the pivot element in the
  :math:`k^{th}` iteration is the largest number in the :math:`(n-k+1)` lower
  entries of the :math:`k^{th}` column. It is written, in the context of
  :math:`LU` decomposition as

  .. math::

    PA=LU\enspace\enspace\enspace\mbox{($P =$ permutation)}

* *Full pivoting* selects the pivot element in the :math:`k^{th}` iteration as
  the largest element of the :math:`(n-k+1)\times (n-k+1)` lower rightmost
  sub-matrix of :math:`A`. It operates by permuting rows *and* columns and leads
  to an :math:`LU` decomposition of

  .. math::

    PAQ = LU

However, there are certain categories of matrices for which we can safely use
Gaussian elimination or :math:`LU` decomposition *without* the need for pivoting
(i.e., the pivot elements will never be problematically small).

.. topic:: Definition

    A matrix :math:`A` is called *diagonally dominant
    by columns* if the magnitude of every diagonal element is larger than the sum of
    the magnitudes of all other entries in the same column, i.e., for every
    :math:`i=1,2,\ldots, n` we have
    
    .. math::

        |a_{ii}|>\sum_{j\neq i} |a_{ji}|

    If the diagonal element exceeds in magnitude the sum of magnitudes of all other
    elements in its *row*, i.e., for every :math:`i=1,2,\ldots, n` we have
    
    .. math::

        |a_{ii}|>\sum_{j\neq i} |a_{ij}|

    then the matrix is called *diagonally dominant by rows*.

.. topic:: Definition

    A symmetric matrix :math:`A\in\mathbb R^{n\times n}` is
    called *positive definite* (in short SPD for "symmetric positive definite"),
    if for any :math:`x\in\mathbb R^n, x\neq 0` we have :math:`x^TAx>0`. If for any :math:`x\in\mathbb R^n, x\neq 0`
    we have :math:`x^TAx\geq0`, the matrix is called positive semi-definite. If the
    respective properties are :math:`x^TAx<0` (or :math:`x^TAx\leq 0`) the matrix is called
    negative (semi) definite.

.. topic:: Definition

    The :math:`k^{th}` *leading principal minor* of a
    matrix :math:`A\in\mathbb R^{n\times n}` is the determinant of the top-leftmost
    :math:`k\times k` sub-matrix of :math:`A`. Thus, if we denote this minor by :math:`M_k`:
    
    .. math::

        M_1=|a_{11}|, \enspace\enspace M_2=
        \left|
        \begin{array}{cc}
        a_{11} & a_{12} \\
        a_{21} & a_{22}
        \end{array}
        \right|,\enspace\enspace \ldots \enspace\enspace
        M_k=\left|
        \begin{array}{ccc}
        a_{11} & \ldots & a_{1k} \\
        \vdots & & \vdots \\
        a_{k1} & \ldots & a_{kk}
        \end{array}
        \right|

.. topic:: Theorem 1

    If *all* leading principal minors (i.e., for :math:`k=1,2,3,\ldots,n`) of the
    symmetric matrix :math:`A` are positive, then :math:`A` is positive definite. If :math:`M_k<0` for
    :math:`k = \mbox{odd}` and :math:`M_k>0` for :math:`k = \mbox{even}`, then :math:`A` is negative
    definite.

.. topic:: Theorem 2

    Pivoting is *not* necessary when :math:`A` is diagonally dominant by columns, or
    symmetric and positive (or negative) definite.


These "special" classes of matrices (which appear quite often in engineering
and applied sciences) not only make :math:`LU` decomposition more robust, but also
open some additional possibilities for solving :math:`Ax=b`.
