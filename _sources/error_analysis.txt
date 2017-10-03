Error Analysis
--------------

Let :math:`x` and :math:`y` be two real numbers, and :math:`\bar x` and :math:`\bar y`
be their corresponding machine number representations. We will assume that
whenever :math:`\bar x` and :math:`\bar y` are combined using an arithmetic
operation :math:`\odot`, the result :math:`\bar x\odot\bar y` is first computed *exactly* and then
discretized using machine precision. It follows from :eq:`machine-error` that
there exist real numbers :math:`0\leq\delta_1,\delta_2,\delta_3\leq\varepsilon`, such that:

.. math::
    \bar x \enspace &=& \enspace x(1+\delta_1) \\
    \bar y \enspace &=& \enspace y(1+\delta_2) \\
    \overline{\bar x\odot\bar y} \enspace &=& \enspace (\bar x\odot\bar y)(1+\delta_3) = (x(1+\delta_1) \odot y(1+\delta_2))(1+\delta_3)
    :label: general-operation

.. topic:: Example 1

    To illustrate this process, let us use a decimal machine operating with five
    significant digits in its floating-point number representation, and
    determine the relative errors in adding, subtracting, multiplying, and
    dividing the two machine numbers
        
    .. math::
        x=0.31426\times 10^3\enspace\enspace\enspace\enspace y=0.92577\times 10^5

    Using a higher precision accumulator (double in length) for the intermediate
    results gives

    .. math::
        x+y \enspace &=&        \enspace 0.9289126000\times 10^5 \\
        x-y \enspace &=&        \enspace -0.9226274000\times 10^5 \\
        x*y \enspace &=&        \enspace 0.2909324802\times 10^8 \\
        x/y \enspace &\approx&  \enspace 0.3394579647\times 10^{-2}

    The computer with five significant digits stores these in rounded form as

    .. math::
        x+y \enspace &=&        \enspace 0.92891\times 10^5 \\
        x-y \enspace &=&        \enspace -0.92263\times 10^5 \\
        x*y \enspace &=&        \enspace 0.29093\times 10^8 \\
        x/y \enspace &\approx&  \enspace 0.33946\times 10^{-2}

    The relative errors in these results are :math:`2.8\times 10^{-6}, 2.8\times
    10^{-6}, 8.5\times 10^{-6},` and :math:`6.0\times 10^{-6}`, respectively --
    all less than :math:`10^{-5}`.

While the above example gives comparable results for all four operations of addition,
subtraction, multiplication, and division, it does not provide any insight into
the size of the relative error. Let us try to theoretically analyze
each of these operations.

Addition
~~~~~~~~

Using equation :eq:`general-operation`, we have

.. math::
    \overline{\bar x + \bar y} = (x(1+\delta_1)+y(1+\delta_2))(1+\delta_3)

Subsituting :math:`\delta=\max\{\delta_1,\delta_2,\delta_3\}` in the above
equation gives

.. math::
    \overline{\bar x + \bar y}                                  \enspace &\leq& \enspace (x+y)(1+\delta)^2 \\
    \Rightarrow \frac{\overline{\bar x + \bar y} - (x+y)}{x+y}  \enspace &\leq& \enspace (1+\delta)^2 - 1 = 2\delta + \delta^2

Since :math:`|\delta|\leq \varepsilon`, the relative error in addition is
on the order of the machine epsilon. Thus, the addition operation is as accurate
as it can be with the available precision.

Subtraction
~~~~~~~~~~~

We will show that there is no bound on the relative error. Let :math:`x=a+\theta`
and :math:`y=\theta`, so :math:`x-y=\theta`. Then,

.. math::
    \bar x - \bar y                         \enspace &=& \enspace (a+\theta)(1+\delta_1)-a(1+\delta_2) = \theta + a(\delta_1 - \delta_2) + \theta\delta_1 \\
    \Rightarrow \overline{\bar x - \bar y}  \enspace &=& \enspace \theta(1+\delta_3) + a(\delta_1 - \delta_2)(1+\delta_3) + \theta\delta_1(1+\delta_3)

Then the relative error is given by

.. math::
    \frac{\overline{\bar x - \bar y} - (x-y)}{x-y} \enspace &=& \enspace \frac{\theta(1+\delta_3) + a(\delta_1 - \delta_2)(1+\delta_3) + \theta\delta_1(1+\delta_3) - \theta}{\theta} \\
    &=& \enspace \delta_3 + \delta_1(1+\delta_3) + \frac{a}{\theta}(\delta_1 - \delta_2)(1+\delta_3)

which becomes unbounded as :math:`\theta\rightarrow 0`.

.. topic:: Example 2

    Suppose we wish to subtract two real numbers :math:`x` and :math:`y` whose
    exact value in the decimal representation is as follows:

    .. math::
        x = 3.212435, \enspace\enspace\enspace\enspace y = 3.21243499999

    Assume that the floating-point number system on the computer only allows for
    :math:`5` significant digits. So :math:`x` and :math:`y` will have the
    following values in machine precision:

    .. math::
        \bar x = 3.21244, \enspace\enspace\enspace\enspace \bar y = 3.21243

    The difference :math:`\bar x - \bar y = 10^{-5}` can be stored exactly in machine
    precision. However, the actual difference is :math:`x-y = 10^{-11}`. Thus,
    the relative error in subtracting :math:`y` from :math:`x` is:

    .. math::
        \frac{\overline{\bar x - \bar y} - (x-y)}{x-y} = \frac{10^{-5} - 10^{-11}}{10^{-11}} \approx 10^6

    Note that the relative error can grow arbitrarily if we add more digits with
    value :math:`9` in the decimal representation of :math:`y`.

Multiplication
~~~~~~~~~~~~~~

Using equation :eq:`general-operation`, we have

.. math::
    \overline{\bar x\cdot\bar y} = x\cdot y(1+\delta_1)(1+\delta_2)(1+\delta_3)

Subsituting :math:`\delta=\max\{\delta_1,\delta_2,\delta_3\}` in the above
equation gives

.. math::
    \overline{\bar x\cdot\bar y} \enspace &\leq& \enspace  x\cdot y (1+\delta)^3 \\
    \Rightarrow \frac{\overline{\bar x\cdot\bar y} - x\cdot y}{x\cdot y} \enspace &\leq& \enspace (1+\delta)^3-1 = 3\delta + 3\delta^2 + \delta^3

Since :math:`|\delta|\leq \varepsilon`, the relative error in multiplication is
on the order of the machine epsilon. Thus, similar to addition, the multiplication operation is as accurate
as possible with the available precision.

Division
~~~~~~~~

Using equation :eq:`general-operation`, we have

.. math::
    \overline{\frac{\bar x}{\bar y}} = \frac{x(1+\delta_1)}{y(1+\delta_2)}(1+\delta_3)
    :label: division-operation

The denominator in the above equation can be eliminated by using the following
geometric series

.. math::
    \frac{1}{1-\theta} = 1+\theta+\theta^2+\theta^3+\ldots

where :math:`|\theta|<1`. Substituting the above series in equation
:eq:`division-operation`, gives

.. math::
    \overline{\frac{\bar x}{\bar y}} = \frac{x}{y}(1+\delta_1)(1+\delta_3)(1-\delta_2+\delta_2^2-\delta_2^3+\delta_4^2-\ldots)

Let :math:`\delta=\max\{\delta_1,\delta_2,\delta_3\}`. Computing the relative
error using the above expression gives a result on the order of :math:`\delta`,
which is comparable to the machine epsilon. Thus, similar to addition and
multiplication, division is also as accurate as possible with the available
precision.
