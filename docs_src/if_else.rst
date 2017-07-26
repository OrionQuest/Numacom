``if/else`` Statements
----------------------

Similar to other high-level languages, `Python <https://www.python.org/>`_ provides ``if/else``
statements to support conditional branching. If the condition within the ``if``
clause evaluates to ``True``, the ``if`` block is executed, otherwise the ``else`` block is executed (if it exists).
`Python <https://www.python.org/>`_ recognizes the keywords ``True``
and ``False`` to correspond to true and false boolean values.
An ``else`` block is not mandatory,
although similar to ``for`` loops, all statements within the ``if/else`` blocks
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
available via the use of curly braces (``{}``) as in `Java <https://en.wikipedia.org/wiki/Java_(programming_language)>`_
or `C++ <https://en.wikipedia.org/wiki/C%2B%2B>`_. The ``==`` operator above
denotes a *conditional test*, as opposed to the ``=`` operator, which denotes
assignment.
The ``print`` statements above
use the ``%`` operator to pass in an integer value, while the associated string had a
generic argument ``%d`` inside it to specify that the value being passed in was an integer. Such a usage of ``print`` statements is quite
common in `Python <https://www.python.org/>`_ and can also be used to pass in
*multiple* values of different types. We will see many more examples of this usage
in later sections. `Python <https://www.python.org/>`_ provides the ``in`` operator to test membership
within a list. In fact, the ``in`` operator can be used to
remove the ``for`` loop above altogether. ::

    >>> a = [i for i in range(0,10)]
    >>> i = 5
    >>> if i in a:
    ...     print 'Key found: %d'%i
    ... else:
    ...     print 'Key not found: %d'%i
    ...
    Key found: 5
