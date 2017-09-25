Upper Triangular Systems
------------------------

The simplest system to solve is a *triangular* system :math:`Ux=b`, where

.. math::
    U = \left[\begin{array}{cccc}
    u_{11} & u_{12} & \ldots & u_{1n} \\
    0 & u_{22} & \ldots & u_{2n} \\
    \vdots & O & \ddots & \vdots \\
    0 & \ldots & 0 & u_{nn}
    \end{array}\right]

is an upper triangular matrix. Here is an example, illustrating how such systems
are easy to solve:

.. math::
    \left[\begin{array}{ccc}
    1 & 2 & 2 \\
    0 & -4 & -6 \\
    0 & 0 & -1
    \end{array}
    \right]\left[\begin{array}{c}
    x_1 \\
    x_2 \\
    x_3
    \end{array}
    \right]=\left[\begin{array}{c}
    3 \\
    -6 \\
    1
    \end{array}
    \right]

From the third row, solve :math:`x_3=-1` and replace :math:`x_3` in the previous
(second) equation to give:

.. math::
    \left[\begin{array}{ccc}
    1 & 2 & 0 \\
    0 & -4 & 0 \\
    0 & 0 & 1 \\
    \end{array}
    \right]\left[\begin{array}{c}
    x_1 \\
    x_2 \\
    x_3
    \end{array}
    \right]=\left[\begin{array}{c}
    5 \\
    -12 \\
    -1
    \end{array}\right]

From the second row, solve :math:`x_2=3` and replace :math:`x_2` in the previous
(first) equation to give:

.. math::
    \left[\begin{array}{ccc}
    1 & 0 & 0 \\
    0 & 1 & 0 \\
    0 & 0 & 1
    \end{array}\right]\left[\begin{array}{c}
    x_1 \\
    x_2 \\
    x_3
    \end{array}\right]=\left[\begin{array}{c}
    -1 \\
    -3 \\
    -1
    \end{array}\right]

We can write this procedure formally in code: ::

    import numpy as np
    
    # Back substitution for upper triangular system
    def Back_Substitution(A,b,x):
        m=A.shape[0]
        n=A.shape[1]
        if(m!=n):
            print 'Matrix is not square!'
            return
        for j in range(n-1,-1,-1):
            if A[j,j] == 0:
                print 'Matrix is singular!'
                return          # matrix is singular
            x[j] = b[j]/A[j,j]
            for i in range(0,j):
                b[i] = b[i] - A[i,j]*x[j]
    
    def main():
        A=np.matrix([[1,2,2],[0,-4,-6],[0,0,-1]])
        b=np.array([3,-6,1])
        x=np.zeros(3)
        Back_Substitution(A,b,x)
        print 'x:',
        for i in range(0,3):
            print x[i],
    
    if __name__ == "__main__":
        main()

By counting how many times the loops are executed, we see that :math:`n`
divisions are required, and :math:`\sum_{j=1}^n (j-1) = O(n^2)` multiplications
and substractions. Overall, the cost of back substitution is :math:`O(n^2)`.
