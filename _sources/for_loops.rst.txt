.. _sec-for-loops:

``for`` Loops
-------------

``for`` loops provide a very convenient way for iterating over the individual
elements in a list. For example: ::

    >>> a = [1,2,3,4,5,6,7,8,9]
    >>> for i in a:
    ...     print i,
    ...
    1 2 3 4 5 6 7 8 9

The dots above signify a continuation from the previous line.
``for`` loops require *indentation*, which is why we use a ``tab`` space
immediately after the line specifying the ``for`` loop. It is customary to leave
an empty line after all commands of the loop have been specified, as this
notifies `Python <https://www.python.org/>`_ about the particular block that
lies inside the loop. Needless to say, if any of these conventions are not
followed, then `Python <https://www.python.org/>`_ will report a syntax error.
Note the comma after the ``print`` statement. Had we
omitted it, all the numbers would have been printed on a *separate* line.
As noted in the previous section, multiplying a list by a constant does not
have the effect of scaling all the individual elements, but this can be
easily achieved using ``for`` loops, as shown below: ::

    >>> a = [1,2,3,4,5,6,7,8,9]
    >>> b = [2*i for i in a]
    >>> b
    [2, 4, 6, 8, 10, 12, 14, 16, 18]

`Python <https://www.python.org/>`_ also provides a ``range`` function for
conveniently generating a list of consecutive numbers. If only one parameter is
provided, it is interpreted as the ``end`` of the list. In this case, the output
of ``range`` are all numbers between ``0`` and ``end-1`` (endpoints inclusive). If two arguments are
provided, the first is interpreted as the ``start`` of the list, while the
second is interpreted as the ``end`` of the list. In this case, the output of
``range`` are all numbers between ``start`` and ``end-1``. Using the ``range`` function,
the ``for`` loop above can be reimplemented as shown below: ::

    >>> a = range(10)
    >>> a
    [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
    >>> a = range(2,10)
    >>> a
    [2, 3, 4, 5, 6, 7, 8, 9]
    >>> for i in range(1,10):
    ...     print i,
    ...
    1 2 3 4 5 6 7 8 9

There are several built-in functions in `Python <https://www.python.org/>`_ for
computing simple statistics on a list of numbers. Note that, unlike basic data
types such as ``int``, ``float``, or ``string``,  the assignment
operator (``=``) gives a *reference* for lists, i.e., both variables refer to the
*same* list. So any modifications to either variable is reflected in the
original list as well. For example: ::

    >>> a = range(1,10)
    >>> min(a)
    1
    >>> max(a)
    9
    >>> sum(a)
    45
    >>> a
    [1, 2, 3, 4, 5, 6, 7, 8, 9]
    >>> b = a
    >>> b.append(10)
    >>> a
    [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
