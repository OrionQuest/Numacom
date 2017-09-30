Lower Triangular Systems
------------------------

Consider a lower triangular matrix :math:`L`:

.. math::
    L = \left[\begin{array}{cccc}
    l_{11} & 0 & \ldots & 0 \\
    l_{21} & l_{22} & \ldots & 0 \\
    \vdots & \vdots & \ddots & 0 \\
    l_{n1} & \ldots & l_{n,n-1} & l_{nn}
    \end{array}\right]

A procedure similar to that for upper triangular systems can be followed to
solve :math:`Lx=b`. The overall complexity is again :math:`O(n^2)`.

.. math::
    \left[\begin{array}{ccc}
    -1 & 0 & 0 \\
    -4 & -6 & 0 \\
    1 & 2 & 2
    \end{array}\right]\left[\begin{array}{c}
    x_1 \\
    x_2 \\
    x_3
    \end{array}\right]=\left[\begin{array}{c}
    3 \\
    -6 \\
    1
    \end{array}\right]

Consider the lower triangular system shown above. The code
below illustrates the forward substitution algorithm on this system. ::

    import numpy as np

    # Forward substitution for lower triangular system
    def Forward_Substitution(A,b,x):
        m=A.shape[0]
        n=A.shape[1]
        if(m!=n):
            print 'Matrix is not square!'
            return
        for j in range(0,n):
            if A[j,j] == 0:
                print 'Matrix is singular!'
                return          # matrix is singular
            x[j] = b[j]/A[j,j]
            for i in range(j+1,n):
                b[i] = b[i] - A[i,j]*x[j]
    
    def main():
        A=np.matrix([[-1,0,0],[-4,-6,0],[1,2,2]])
        b=np.array([3,-6,1])
        x=np.zeros(3)
        Forward_Substitution(A,b,x)
        print 'x:',
        for i in range(0,3):
            print x[i],
    
    if __name__ == "__main__":
        main()
