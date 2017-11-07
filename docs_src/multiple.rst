Multiple Roots
~~~~~~~~~~~~~~

So far we have ignored the case :math:`f'(a)=0`. This case is typically described as a
*multiple root* because if :math:`f(x)` is a polynomial and
:math:`f(a)=f'(a)=f''(a)=\ldots =f^{(k-1)}(a)=0`, this would imply that :math:`(x-a)^k` is a
factor of :math:`f(x)` (in other words, :math:`a` is a root with multiplicity of :math:`k`).
Let us now assume that :math:`f(a)=f'(a)=f''(a)=\ldots =f^{(k-1)}(a)=0`, but
:math:`f^{(k)}(a)\neq 0`. At first, it may appear that Newton's method would be
inapplicable in this case, because the denominator :math:`f'(x)` becomes near-zero
close to the solution. Consider, however, the example:

.. math::
    f(x)=(x-1)^3(x+2)

Newton's method would give:

.. math::
    g(x)=x-\frac{f(x)}{f'(x)}=x-\frac{(x-1)^3(x+2)}{3(x-1)^2(x+2)+(x-1)^3}=x-\frac{(x-1)(x+2)}{4x+5}

whose denominator remains non-zero near the solution :math:`x=1`. In fact, we can show
that :math:`g` remains a contraction near :math:`a` in this case.

    *Proof:* Remember that
    
    .. math::
        g'(x)=\frac{f(x)f''(x)}{[f'(x)]^2}
    
    Taylor's theorem applied on :math:`f(x)` yields:
    
    .. math::
        f(x)=\underbrace{f(a)}_{=0}+\underbrace{f'(a)}_{=0}(x-a)+\ldots +\underbrace{\frac{f^{(k-1)}(a)}{(k-1)!}}_{=0}(x-a)^{k-1}+\underbrace{\frac{f^{(k)}(c_1)}{k!}}_{\neq 0}(x-a)^k
    
    Applying Taylor's formula on the *derivative* :math:`f'(x)` gives
    
    .. math::
        f'(x)=\underbrace{f'(a)}_{=0}+\underbrace{f''(a)}_{=0}(x-a)+\ldots +\underbrace{\frac{f^{(k-1)}(a)}{(k-2)!}}_{=0}(x-a)^{k-2}+\underbrace{\frac{f^{(k)}(c_2)}{(k-1)!}}_{\neq 0}(x-a)^{k-1}
    
    And one more on the second derivative :math:`f''(x)`
    
    .. math::
        f''(x)=\underbrace{f''(a)}_{=0}+\underbrace{f'''(a)}_{=0}(x-a)+\ldots +\underbrace{\frac{f^{(k-1)}(a)}{(k-3)!}}_{=0}(x-a)^{k-3}+\underbrace{\frac{f^{(k)}(c_3)}{(k-2)!}}_{\neq 0}(x-a)^{k-2}
    
    where :math:`c_1, c_2, c_3` are some numbers between :math:`x` and :math:`a`. Combining the last three
    equations gives
    
    .. math::
        g'(x)=\frac{\frac{f^{(k)}(c_1)}{k!}(x-a)^k\frac{f^{(k)}(c_3)}{(k-2)!}(x-a)^{k-2}}{\left[\frac{f^{(k)}(c_2)}{(k-1)!}(x-a)^{k-1}\right]^2}\xrightarrow{x\rightarrow a}\frac{\left[f^{(k)}(a)\right]^2}{\left[f^{(k)}(a)\right]^2}\frac{[(k-1)!]^2}{k!(k-2)!}=\frac{k-1}{k}
    
    Since :math:`g'(a)=(k-1)/k<1`, there is an interval :math:`(a-\delta,a+\delta)` where :math:`|g'(x)|\leq L<1` and thus, :math:`g` is a contraction.

However, in all these cases, convergence is limited to be *only linear*,
since :math:`g'(a)\neq 0`.

**Caution:** If we know, or suspect, that :math:`f(x)` may have a multiple root,
then Newton's method is only safe (albeit slow) when we can write an analytic
formula for :math:`f(x)/f'(x)` and perform any cancellations "on paper" to avoid
division by zero. Otherwise, for example in the case where both :math:`f` and :math:`f'` are
given as black-box computer functions, any roundoff error in the value of the
numerator or denominator could cause severe instabilities, by dividing two
(inaccurate) near-zero quantities.
