``while`` Loops
---------------

:ref:`sec-for-loops` either iterate on the contents of a container, such as a
list or a dictionary, or until a given counter exceeds a prespecified threshold.
In contrast, a ``while`` loop runs until a specified condition is true, as shown
below. ::

    >>> counter = 0
    >>> while counter < 5:
    ...     print counter,
    ...     counter+=1
    ...
    0 1 2 3 4

.. warning::

    The above loop would run infinitely if the value of counter was not
    incremented in each iteration. This is a very common pitfall which
    the application developer should watch out for!
   
There are various scenarios where the flexibility of ``while`` loops proves advantageous, such as
when operating with inputs given by the user, or when checking the status of a
boolean flag. Similar to `Java <https://en.wikipedia.org/wiki/Java_(programming_language)>`_
or `C++ <https://en.wikipedia.org/wiki/C%2B%2B>`_, `Python <https://www.python.org/>`_
provides a ``break`` command to exit out of a loop early. This allows us to write loops
where the termination criterion may not be known in advance, or is pretty large
in terms of computational cost. For example: ::

    >>> active_list = [5,9,14,23,31]
    >>> counter = 0
    >>> while counter < 10000:
    ...     if(counter in active_list): break
    ...     else: print counter,
    ...     counter+=1
    ...
    0 1 2 3 4

In the example above, the termination criterion can make the loop run for quite
some time. Instead, we check if the value of counter is present in ``active_list``
and if so, we break out early. This stops the loop in just :math:`5` iterations.
`Python <https://www.python.org/>`_ also provides a ``continue`` command to skip
all statements coming after it in a loop, as shown below. ::

    >>> counter = 0
    >>> while counter<100:
    ...     counter+=1
    ...     if counter in inactive_list: continue
    ...     print counter,
    ...
    1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19

In the example above, note that ``counter`` is incremented before the statement
with ``continue``. If instead, we incremented ``counter`` *afterwards*,
then we would have encountered an infinite loop! Thus, when using ``continue``
or ``while`` loops in general, the application developer should be extremely
mindful of such logical errors. Also note that the commands ``break`` and
``continue`` are *not specific* to ``while`` loops, and can be used with ``for``
loops as well.
