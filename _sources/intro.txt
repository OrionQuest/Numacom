Introduction
============

This section gives a broad overview of the concepts from linear algebra that
will be used throughout the course. It is intended as a review of background
material. While most students may already be familiar with these
topics, they are still encouraged to briefly skim through the material
so as to take note of all the programming concepts that are introduced.

We will be working almost exclusively with the set :math:`\mathbb R` of all `real numbers <https://en.wikipedia.org/wiki/Real_number>`_. In particular, we will
consider the *Cartesian product* of two sets :math:`A` and :math:`B` defined as:

.. math::
    A\times B = \{(a,b) : a\in A \mbox{ and } b\in B\}

The Cartesian product can be used to define *powers* of sets as follows:

.. math::
    A^n = \underbrace{A \times A\times \ldots \times A}_{n \mbox{ times}}

Vectors
-------

This yields the space :math:`\mathbb R^n` of all :math:`n`-dimensional *vectors*,
defined as:

.. math::
    \mathbb R^n = \{(a_1,a_2,\ldots,a_n) : a_i\in\mathbb R \mbox{ for all } 1\leq i\leq n\}

Thus, an :math:`n`-dimensional vector :math:`v` is represented as an ordered set
of :math:`n` real numbers :math:`a_i`, where :math:`1\leq i\leq n`. Each element :math:`a_i`
is called a *component* of :math:`v`. In what follows, we will exclusively refer
to the :math:`i`-th component of a vector :math:`v` as :math:`v_i`, so :math:`v` can be written as :math:`v=(v_1,v_2,\ldots,v_n)`.
A vector of dimension :math:`1` is commonly referred to as a *scalar*.
In `Python <https://www.python.org/>`_
vectors are particularly easy to define with `NumPy <http://www.numpy.org/>`_
using ``arrays``. The example below defines a :math:`4`-dimensional vector ``x``: ::

    >>> import numpy as np
    >>> x = np.array([2,3,1,0])
    >>> x
    array([2, 3, 1, 0])

Two vectors can be added together in a component-wise fashion to define a new vector,
i.e., if :math:`v` and :math:`w` are two vectors, we can define a new vector
:math:`v+w` as follows:

.. math::
    v+w = (v_1+w_1,v_2+w_2,\ldots,v_n+w_n)

It follows from the above definition that :math:`v+w = w+v`, showing that vector
addition is `commutative <https://en.wikipedia.org/wiki/Commutative_property>`_.
Vector addition is supported in `Python <https://www.python.org/>`_, as shown in
the following example: ::

    >>> v = np.array([2,3,1,0])
    >>> w = np.array([5,4,2,7])
    >>> v+w
    array([7, 7, 3, 7])

Note that vector addition is *not defined* when the two vectors being added
together have different dimensions. If you tried to add together two vectors of
different dimensions in `Python <https://www.python.org/>`_, you will get an error: ::

    >>> u = np.array([3,4,2])
    >>> v = np.array([2,3,1,0])
    >>> u+v
    Traceback (most recent call last):
      File "<stdin>", line 1, in <module>
    ValueError: operands could not be broadcast together with shapes (3,) (4,)

A vector :math:`v` can also be multiplied with a scalar :math:`c` to define a
new vector as follows:

.. math::
    c\cdot v = (cv_1,cv_2,\ldots,cv_n)

Once again, the order does not matter for scalar multiplication, i.e.,
:math:`c\cdot v = v\cdot c`. Scalar multiplication is also supported in `Python <https://www.python.org/>`_,
as shown here: ::

    >>> v = np.array([2,3,1,0])
    >>> v*5
    array([10, 15,  5,  0])
    >>> 5*v
    array([10, 15,  5,  0])

Vector addition and scalar multiplication can together be used to define vector
*subtraction*, i.e., if :math:`v` and :math:`w` are two vectors, then they can be
subtracted together to define a new vector as follows:

.. math::
    v - w = v + (-1)\cdot w = (v_1-w_1,v_2-w_2,\ldots,v_n-w_n)

Again, note that vector subtraction is not defined when the two vectors being
subtracted together have different dimensions. Together, these operations
allow us to define a *linear combination* of a set of vectors :math:`\{v^k\}`
as a weighted sum:

.. math::
    w = \sum_k a_k v^k

where :math:`a_k\in\mathbb R`.
