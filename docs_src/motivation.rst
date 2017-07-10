Motivation
----------

In many instances, we are faced with mathematical problems where the conventional
method "on paper" does not perform as well when implemented on the computer.
Take, for example, the quadratic equation:

.. math::
    
    ax^2 + bx + c = 0

In theory, we have a perfectly conclusive method for determining the roots of
this equation; simply use the quadratic formula:

.. math::
    
    x_{1,2} = \frac{-b\pm\sqrt{b^2-4ac}}{2a}

In fact, let us consider a very specific example:

.. math::

    0.0501x^2 -98.78x +5.015 = 0

The actual roots of this equation, rounded to :math:`10` digits of accuracy, are

.. math::
    x_1 = 1971.605916, \enspace\enspace\enspace\enspace x_2 = 0.05077069387
