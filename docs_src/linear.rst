Linear Systems of Equations
===========================

We will consider the solution of (square) systems of linear equations described in the form

.. math::
    Ax=b

where :math:`A` is an :math:`n\times n` matrix, and :math:`x,b` are :math:`n\times 1` vectors.
Such a system admits a unique solution if all columns of :math:`A` are *linearly
independent*, or in other words, the matrix :math:`A` is *invertible*. We first consider
direct methods, where our general strategy will be to transform this system
into an equivalent, but easier system (or systems) to solve.

.. toctree::
    :hidden:
    :maxdepth: 2

    Upper Triangular Systems <upper>
    Lower Triangular Systems <lower>
    LU Decomposition <lu_decomp>
    Iterative Methods <iterative>
