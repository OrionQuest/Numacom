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

