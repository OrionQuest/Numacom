Order Notation
--------------

Let :math:`f,g:\mathbb R\rightarrow\mathbb R` be two functions.
We say that :math:`f(n) = O(g(n))`, read as ":math:`f` is *big-oh* of :math:`g`"
or ":math:`f` is of *order* :math:`g`", if there is a positive constant :math:`C`
such that

.. math::
    \vert f(n)\vert\leq C\vert g(n)\vert
    
for all sufficiently large :math:`n`. For example,

.. math::
    2n^3 + 3n^2 + n = O(n^3)

because as :math:`n` becomes large, the terms of order lower than :math:`n^3`
become relatively insignificant. While the above definition is based on the
function argument increasing in magnitude, the order notation can also be
defined when the function argument keeps decreasing in magnitude. Indeed, in
many applications we are interested in the behavior as some quantitiy :math:`h`
(such as a *step size* or *mesh spacing*) becomes very small. We say that

.. math::
    f(h) = O(g(h))

if there is a positive constant :math:`C` such that

.. math::
    \vert f(h)\vert \leq C\vert g(h)\vert

for all sufficient small :math:`h`. For example,

.. math::
    \frac{1}{1-h} = 1+h+h^2+h^3+\ldots = 1+h+O(h^2)

because as :math:`h` becomes small, the omitted terms beyond :math:`h^2` become
relatively insignificant. Note that the above two definitions are equivalent if
:math:`h=1/n`.
