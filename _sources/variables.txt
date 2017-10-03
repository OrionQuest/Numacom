Variables and Data Types
------------------------

Unlike `Java <https://en.wikipedia.org/wiki/Java_(programming_language)>`_ or `C++ <https://en.wikipedia.org/wiki/C%2B%2B>`_,
which are `compiler-based <https://en.wikipedia.org/wiki/Compiler>`_ languages, `Python <https://www.python.org/>`_ is an `interpreter-based <https://en.wikipedia.org/wiki/Interpreter_(computing)>`_ language.
This means that each program is executed *line-by-line* with
no preprocessing for speeding up the execution time. As a consequence, the
developer does not have to specify the variable type before a given variable
name. `Python <https://www.python.org/>`_ follows the same rules for
naming variables as `Java <https://en.wikipedia.org/wiki/Java_(programming_language)>`_ or `C++ <https://en.wikipedia.org/wiki/C%2B%2B>`_,
so we will not repeat them here for brevity. The value of any variable can be
printed using the ``print`` keyword. Some examples of variable
assignments are given below: ::

    >>> myint = 7
    >>> myfloat = 7.0
    >>> mystring = "hello"

Strings
~~~~~~~

A string is simply a sequence of characters. All characters inside single or
double quotes constitute a string in `Python <https://www.python.org/>`_. This
gives flexibility in using both quotes and apostrophes within strings, as shown
below: ::

    >>> mystring = '"Come into my parlor", said the spider to the fly.'
    >>> print mystring
    "Come into my parlor", said the spider to the fly.

Two strings can be conveniently concatenated together using the ``+`` operator.
`Python <https://www.python.org/>`_ provides many built-in functions for string processing also, such as ``title``
which capitalizes the first letter of every word, ``upper`` which capitalizes
all letters, ``lower`` which converts all characters to lower case, or ``rstrip``
which deletes all whitespaces, just to name a few. Note that a number can also
be converted into string using the ``str`` keyword, as shown below: ::

    >>> mystring = "Index "+str(23)+" has value: "+str(1.5)
    >>> mystring
    'Index 23 has value: 1.5'

Since scientific computing
algorithms will primarily consider numeric values, we will not dive too deep into
string processing with `Python <https://www.python.org/>`_.

Integers
~~~~~~~~

Integers types are supported in `Python <https://www.python.org/>`_ with all the
usual addition (``+``), subtraction (``-``), multiplication (``*``),
division (``/``), and modulo (``%``) operators. Additionally, one can raise a number to a specified
power using the double-multiplication (``**``) operator. ::

    >>> a = 5
    >>> b = 3
    >>> a+b
    8
    >>> a-b
    2
    >>> a*b
    15
    >>> a/b
    1
    >>> a%b
    2
    >>> a**b
    125

Note that ``a/b`` gives us a value of ``1`` because both the arguments are
integers, so the ``/`` operator corresponds to *integer division*. If we wanted
a floating-point value, we can explicitly convert one argument to ``float``, as
shown below: ::

    >>> float(a)/b
    1.6666666666666667
    >>> a/float(b)
    1.6666666666666667

Floats
~~~~~~

We have already discussed floating-point numbers at length in the previous
chapter. Such numbers support all the usual arithmetic operators as integers.
The modulo (``%``) operator generalizes to *include* the fractional part in this case. A floating-point number can be explicitly
converted to an integer using the ``int`` keyword. This is also useful for
extracting the fractional part, as shown below: ::

    >>> a = 5.3
    >>> int(a)              # integer part
    5
    >>> a-int(a)            # fractional part
    0.2999999999999998
    >>> b = 2
    >>> a%b
    2.3

Comments can be specified by preceding the text with the ``#`` sign, as shown above.
Note how `Python <https://www.python.org/>`_ approximates the simple value of
``0.3`` with the more complex expression ``0.2999999999999998`` as shown above.
As explained in the previous chapter, this happens because of limited precision
available on the computer. In later chapters, we will discuss this issue at length and
specifically study the design of algorithms that do not produce wrong results
because of cancellations between approximate (limited precision)
representations.
