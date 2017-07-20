Lists
-----

A *list* is an ordered collection of items, and is indicated in `Python <https://www.python.org/>`_ via square brackets (``[]``),
all individual elements being separated by commas. There need not be any
particular relation between the elements, and each element can be of a different
data type as well. Some examples are given below: ::

    >>> a = ['hello',2,float(5)]
    >>> a
    ['hello', 2, 5.0]

The elements within a list are indexed starting from ``0`` and can be accessed using the
square bracket (``[]``) operator, as shown below. Unlike arrays in `Java <https://en.wikipedia.org/wiki/Java_(programming_language)>`_
or `C++ <https://en.wikipedia.org/wiki/C%2B%2B>`_, negative elements are *also*
valid and point to elements from the end of the list. For example: ::

    >>> print a[1]
    2
    >>> print a[-1]
    5.0

Individual elements can be modified in a straightforward manner by using the
assignment operator (``=``). Elements can be added to the end of the list using
the ``append`` operator, and anywhere within the list using the ``insert``
operator. Likewise, elements can be deleted from the end by using the ``pop`` operator, or
anywhere within the list by using the ``del`` keyword. ::

    >>> a[0] = 4
    >>> a
    [4, 2, 5.0]
    >>> a.append('wow')
    >>> a
    [4, 2, 5.0, 'wow']
    >>> a.pop()
    'wow'
    >>> a
    [4, 2, 5.0]
    >>> del a[1]
    >>> a
    [4, 5.0]

Note that, unlike the ``append`` operator, the ``pop`` operator returns back the element deleted from the list.
