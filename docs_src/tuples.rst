Tuples
------

:ref:`sec-lists` allow storage of items that can change over time. However,
sometimes the developer requires a list that remains constant over time.
`Python <https://www.python.org/>`_ defines *tuples* to accommodate this need,
and this is also the reason why tuples are faster than lists.
Objects that remain constant over time are referred to as *immutable* in `Python <https://www.python.org/>`_.
Thus, a tuple can be defined as an *immutable list*. In terms of code, a tuple
looks just like a list except the square brackets are replaced by
parentheses. For example: ::

    >>> a = (100,20,'a')
    >>> print a[0]
    100
    >>> print a[2]
    'a'
    >>> a[2] = 9
    Traceback (most recent call last):
      File "<stdin>", line 1, in <module>
    TypeError: 'tuple' object does not support item assignment

As shown above, the individual elements can be accessed by specifying the element index within square brackets, exactly as lists. Note how `Python <https://www.python.org/>`_
reports an error whenever an attempt is made to alter the value of an element. While the elements within a tuple cannot be changed, the variable holding the tuple can *always*
be assigned a new tuple, as shown below: ::

    >>> a = (100,20,'a')
    >>> a = (0,1,2,3,4)
    >>> a
    (0, 1, 2, 3, 4)
