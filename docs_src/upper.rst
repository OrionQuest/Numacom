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

    # Back substitution for upper triangular system
    for j in range(n,0,-1):
        if u[j,j] == 0: return        # matrix is singular
        x[j] = b[j]/u[j,j]
        for i in range(1,j):
            b[i] = b[i] - u[i,j]*x[j]

By counting how many times the loops are executed, we see that :math:`n`
divisions are required, and :math:`\sum_{j=1}^n (j-1) = O(n^2)` multiplications
and substractions. Overall, the cost of back substitution is :math:`O(n^2)`.
