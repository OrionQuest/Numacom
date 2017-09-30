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
