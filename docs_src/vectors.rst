Vectors
-------

This Cartesian product on :math:`\mathbb R` allows us to define the space :math:`\mathbb R^n` of all :math:`n`-dimensional *vectors*
as follows:

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
:math:`v+w` as:

.. math::
    v+w = (v_1+w_1,v_2+w_2,\ldots,v_n+w_n)

It follows from the above definition that :math:`v+w = w+v`, showing that vector
addition is `commutative <https://en.wikipedia.org/wiki/Commutative_property>`_.
Vector addition is supported in `Python <https://www.python.org/>`_, as shown below: ::

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
subtracted together to define a new vector :math:`v-w` as:

.. math::
    v - w = v + (-1)\cdot w = (v_1-w_1,v_2-w_2,\ldots,v_n-w_n)

Again, note that vector subtraction is not defined when the two vectors being
subtracted have different dimensions. Together, these operations
allow us to define a *linear combination* of a set :math:`S` of vectors :math:`\{v^k\}`
as a weighted sum:

.. math::
    w = \sum_k a_k v^k

where :math:`a_k\in\mathbb R` for all :math:`k`. The set of all linear combinations of vectors in
:math:`S` constitute the *span* of :math:`S`, denoted as :math:`\textsf{span } S`, i.e.,

.. math::
    \textsf{span }S \equiv \{a_1v^1+\ldots+a_kv^k : v^i\in S\mbox{ and }a_i\in\mathbb R\mbox{ for all }1\leq i\leq k\}

Perhaps you may recall that any :math:`3`-dimensional vector :math:`v` can be written as
a linear combination of the three unit vectors :math:`(1,0,0)`, :math:`(0,1,0)`,
and :math:`(0,0,1)`. Thus, the span of these three unit vectors is the entire
:math:`3`-dimensional Euclidean space :math:`\mathbb R^3`. The notion of linear
combination, in turn, allows us to define *linear independence*. A set :math:`S` of vectors :math:`\{v^k\}`
is said to be linearly independent if every non-trivial linear combination of
vectors in :math:`S` is
non-zero. More formally, whenever the sum :math:`a_1v^1+\ldots+a_kv^k = 0`, then the coefficients :math:`a_i = 0`
for all :math:`1\leq i\leq k`. A set of vectors is said to be *linearly dependent*
if they are not linearly independent. We will discuss linear
combinations and linear independence in much more detail when we study :ref:`sec-matrices`.

Finally, the space :math:`\mathbb R^n` also comes equipped with a function
:math:`f:\mathbb R^n\times\mathbb R^n\rightarrow\mathbb R` called the *dot
product*, denoted as :math:`v\cdot w` for two vectors :math:`v` and :math:`w`, and formally defined as:

.. math::
    v\cdot w = \sum_{i=1}^k v_iw_i

`NumPy <http://www.numpy.org/>`_ has a function ``dot`` that allows us to
easily compute the dot product of two vectors, as shown below: ::

    >>> v = np.array([3,1,4])
    >>> w = np.array([2,5,7])
    >>> np.dot(v,w)
    39

The dot product allows us to define the familiar *Euclidean* or :math:`L_2`-norm on
:math:`\mathbb R^n` as follows:

.. math::
    \|v\|_2 = \sqrt{v\cdot v} = \sqrt{v_1^2+\ldots+v_n^2}

`NumPy <http://www.numpy.org/>`_ has a package called ``linalg`` that allows us
to directly compute the :math:`L_2`-norm of a vector, as shown below: ::

    >>> v = np.array([3,1,4,5,2,7])
    >>> np.linalg.norm(v)
    10.198039027185569

Apart from the Euclidean norm, several other kinds of norms can also be defined
for a vector :math:`v\in\mathbb R^n`. Two different kinds that we will frequently encounter in
subsequent sections are the :math:`L_1`-norm (denoted as :math:`\|v\|_1`) and
the :math:`L_\infty`-norm (denoted as :math:`\|v\|_\infty`), defined as follows:

.. math::
    \|v\|_1         &=& \enspace |v_1|+|v_2|+\ldots+|v_n| \\
    \|v\|_\infty    &=& \enspace \textsf{max }|v_i|\mbox{, where }1\leq i\leq n

Interestingly, the ``linalg`` package in `NumPy <http://www.numpy.org/>`_ can
compute all these different kinds of norms for a given vector, as shown below.
Here, the second parameter specifies the particular norm that we wish to compute
(in our case, the :math:`L_1` norm, :math:`L_2` norm, or :math:`L_\infty` norm, respectively): ::

    >>> v = v = np.array([3,1,4,5,2,7])
    >>> np.linalg.norm(v,1)
    22
    >>> np.linalg.norm(v,2)
    10.198039027185569
    >>> np.linalg.norm(v,np.inf)
    7
