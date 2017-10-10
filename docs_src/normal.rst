Overdetermined Systems
----------------------

So far, we considered linear systems :math:`Ax=b` with the *same* number of
equations and unknowns (i.e., :math:`A\in\mathbb R^{n\times n}`). In the case where
:math:`A\in\mathbb R^{m\times n}`, with :math:`m>n` (more equations than unknowns) the existence of a
true solution is not guaranteed, in this case we look for the "best possible"
substitute for a solution. Before analyzing what that means, let's look at how
such problems arise.

As an example, in an experiment, we measure the pressure of a gas in a closed container as a
function of the temperature. From Physics, we know that

.. math::
    pV &=& \enspace nR\frac{5}{9}(T+459.67) \\
    \Rightarrow p&=& \enspace\alpha T+\beta, \enspace\enspace\enspace \alpha=\frac{5nR}{9V}, \beta=\frac{5nR\cdot 459.67}{9V}
