Floating-point Arithmetic
-------------------------

As shown in the previous section, fractional numbers are a common
occurence in scientific computing, which naturally brings up the
question of how much *precision* is sufficient for a particular application.
Digital computers use the *floating-point* number system to represent the set of real
numbers :math:`\mathbb R` using the "scientific notation". For any decimal
number :math:`x` (assuming :math:`x` is a terminating decimal number, with
finite non-zero digits) we can write:

.. math::
    x=a\times 10^b, \enspace\enspace\enspace\mbox{where}\enspace\enspace1\leq\vert a\vert<10

The only exception is :math:`x=0`, where we simply set :math:`a=b=0`. Every
decimal (or base :math:`10`) number can be written as:

.. math::
    a_k a_{k-1} \ldots a_2 a_1 a_0 . a_{-1} a_{-2} a_{-3}\ldots a_{-m} = \sum_{i=-m}^k a_i 10^i

Note how the decimal point moves, or *floats*, as the power of :math:`10`
changes. Some examples are given below:

.. math::
    \begin{array}{|c|c|c|c|c|c|c|c|}
    \hline
    x & a_3 & a_2 & a_1 & a_0. & a_{-1} & a_{-2} & a_{-3} \\
    \hline
    3.14 & & & & 3 & 1 & 4 & \\
    0.037 & & & & & & 3 & 7 \\
    2012 & 2 & 0 & 1 & 2 & & & \\
    \hline
    \end{array}

Similarly, binary (base :math:`2`) fractional numbers can be written as:

.. math::
    b_k b_{k-1} \ldots b_2 b_1 b_0 . b_{-1} b_{-2} b_{-3}\ldots b_{-m} = \sum_{i=-m}^k b_i 2^i

where every digit :math:`b_i` is now only allowed to equal :math:`0` or :math:`1`. For example:

* :math:`5.75_{(10)} = 4+1+0.5+0.25 = 1\times2^2 + 1\times 2^0 + 1\times 2^{-1} +1\times 2^{-2} = 101.11_{(2)}`
* :math:`17.5_{(10)} = 16 + 1 + 0.5 = 1\times 2^4 + 1\times 2^0 + 1\times 2^{-1} = 10001.1_{(2)}`

Note that certain numbers that are finite (terminating) decimals actually are
periodic in binary, e.g.

.. math::
    0.4_{(10)} = 0.01100110011\ldots_{(2)} = 0.011\overline{0011}_{(2)}

.. toctree::
    :hidden:
    :maxdepth: 2

    Machine Numbers <machine>
