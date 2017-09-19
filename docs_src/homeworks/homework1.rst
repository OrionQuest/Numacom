Homework #1
===========

For all programming assignments, please turn in your code along with your
solution. Submissions should be made on Sakai.

.. topic:: Problem 1

    What are the approximate absolute and relative errors in approximating
    :math:`\pi` by each of the following quantities?

    (a) :math:`3`
    (b) :math:`3.14`
    (c) :math:`22/7`

    You can use either single or double precision for your computations. Please
    state your choice.

.. topic:: Problem 2

    In either single or double precision, is the machine epsilon the smallest number :math:`\varepsilon`
    that can be stored on the computer, such that :math:`1+\varepsilon\neq 1`? Justify your answer.

.. topic:: Problem 3

    Write a program to compute the absolute and relative errors in Stirling's
    approximation

    .. math::
        n! \approx \sqrt{2\pi n}(n/e)^n

    for :math:`n=1,2,\ldots,10`. Does the absolute error grow or shrink as
    :math:`n` increases? Does the relative error grow or shrink as :math:`n`
    increases? Is the result affected when using double precision instead of
    single precision?

.. topic:: Problem 4

    Let :math:`x\in\mathbb R^n` be an :math:`n`-dimensional vector. Show that
    :math:`\lVert x\rVert_2` and :math:`\lVert x\rVert_\infty` are equivalent.

.. topic:: Problem 5

    Consider the image blurring example discussed in class, and suppose we
    denote the matrix of grayscale pixel values as :math:`I`. Modify the Python script
    ``blur.py`` to use the following operation instead:

    .. math::

        I[i,j] \enspace &=& \enspace \frac{1}{16}(8\cdot I[i,j] + I[i-1,j] + I[i-1,j-1] + I[i-1,j+1] + I[i,j-1] \\
               \enspace &+& \enspace I[i,j+1] + I[i+1,j] + I[i+1,j-1] + I[i+1,j+1])

    Compute the blurred image after :math:`20` iterations of this modified
    scheme.
