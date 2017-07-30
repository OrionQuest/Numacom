``if/else`` Statements
----------------------

Similar to other high-level languages, `Python <https://www.python.org/>`_ provides ``if/else``
statements to support conditional branching. If the condition within the ``if``
clause evaluates to ``True``, the ``if`` block is executed, otherwise the ``else`` block is executed (if it exists).
`Python <https://www.python.org/>`_ recognizes the keywords ``True``
and ``False`` to correspond to true and false boolean values.
An ``else`` block is not mandatory,
and similar to ``for`` loops, all statements within the ``if/else`` blocks
should be indented. For example: ::

    >>> a = [i for i in range(1,6)]
    >>> for i in a:
    ...     if i==5:
    ...         print 'Key found: %d'%i
    ...     else:
    ...         print 'Key not found: %d'%i
    ...
    Key not found: 1
    Key not found: 2
    Key not found: 3
    Key not found: 4
    Key found: 5


The ``if`` and ``else`` clauses were indented inside the ``for`` loop, but the statements inside these blocks were indented *again*.
This is necessary to let `Python <https://www.python.org/>`_ know the intended code structure, as there is no explicit scoping
available via the use of curly braces (``{}``) as supported in `Java <https://en.wikipedia.org/wiki/Java_(programming_language)>`_
or `C++ <https://en.wikipedia.org/wiki/C%2B%2B>`_. The ``==`` operator above
denotes a *conditional test*, as opposed to the ``=`` operator, which denotes
assignment. (Note that ``!=`` denotes the "not equals" operator in `Python <https://www.python.org/>`_.)
The ``print`` statements above
use the ``%`` operator to pass in an integer value, while the associated string had a
generic argument ``%d`` inside it to specify that the value being passed in was an integer. Such a usage of ``print`` statements is quite
common in `Python <https://www.python.org/>`_ and can also be used to pass in
multiple values of different types. We will see many more examples of this usage
in later sections. `Python <https://www.python.org/>`_ provides the ``in`` operator to test membership
within a list. In fact, the ``in`` operator can be used above to
remove the ``for`` loop altogether. ::

    >>> a = [i for i in range(1,6)]
    >>> i = 5
    >>> if i in a:
    ...     print 'Key found: %d'%i
    ... else:
    ...     print 'Key not found: %d'%i
    ...
    Key found: 5

Similar to the ``in`` operator, `Python <https://www.python.org/>`_ also
provides a ``not in`` operator to test non-membership within a list. For example: ::

    >>> a = [i for i in range(1,6)]
    >>> a
    [1, 2, 3, 4, 5]
    >>> i = 10
    >>> if i not in a:
    ...     print 'Key %d not found'%i
    ... else:
    ...     print 'Key %d found'%i
    ... 
    Key 10 not found

The ``not`` keyword is an example of a *logical* operator in `Python <https://www.python.org/>`_. Other logical
operators are specified by the ``and`` and ``or`` keywords
which can be used to check multiple conditions at the same time. The ``and``
operator returns true if all the conditions being checked are
*simultaneously* true. The ``or`` operator, on the other hand, returns true if *any
one* of the conditions being checked is true. ::

    >>> i = 10
    >>> i>=1 and i<=10
    True
    >>> i>=1 or i<=5
    True
    >>> i>=1 and i<=5
    False

Often times one needs to check more than two possible situations, i.e.,
one ``if-else`` branch is not sufficient and deeper nesting is required.
`Python <https://www.python.org/>`_ makes this possible using the ``if-elif-else``
construct, where the last ``else`` block can be skipped if desired. As soon as
`Python <https://www.python.org/>`_ finds one condition that is satisfied, it
skips the rest. ::

    >>> i = 4
    >>> if i<=1:
    ...     print 'Value %d is less than or equal to 1'%i
    ... elif i>1 and i<=5:
    ...     print 'Value %d is greater than 1 and less than or equal to 5'%i
    ... elif i>5 and i<=10:
    ...     print 'Value %d is greater than 5 and less than or equal to 10'%i
    ... else:
    ...     print 'Value %d is greater than 10'%i
    ...
    Value 4 is greater than 1 and less than or equal to 5

So far, we have only worked with non-empty lists, but a list can be empty as
well. `Python <https://www.python.org/>`_ allows the name of a list to be used
in place of a condition in an ``if`` statement. In this case, the result is ``True``
if the list is not empty, otherwise the result is ``False``. ::

    >>> a = []
    >>> if a:
    ...     print 'The list is non-empty'
    ... else:
    ...     print 'The list is empty!'
    ...
    The list is empty!
