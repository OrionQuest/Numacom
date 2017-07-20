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
or `C++ <https://en.wikipedia.org/wiki/C%2B%2B>`_, negative indices are *also*
valid and point to elements from the end of the list. ::

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
    >>> a.insert(2,'hello')
    >>> a
    [4, 2, 'hello', 5.0]
    >>> del a[1]
    >>> a
    [4, 'hello', 5.0]

Note that, unlike the ``append`` operator, the ``pop`` operator returns back the element deleted from the list. If an index is supplied to the ``pop``
operator, then it can also be used for deleting an element from anywhere inside the list. Elements can also be deleted *by value* using the ``remove``
operator. For example: ::

    >>> mystring = "Old McDonald had a farm, Duda!"
    >>> words = mystring.split()
    >>> words
    ['Old', 'McDonald', 'had', 'a', 'farm,', 'Duda!']
    >>> words.pop(0)
    'Old'
    >>> words
    ['McDonald', 'had', 'a', 'farm,', 'Duda!']
    >>> words.remove('Duda!')
    >>> words
    ['McDonald', 'had', 'a', 'farm,']

Note how we used the ``split`` operator to generate a list of all the words in a string. A list can also be sorted using the ``sort`` operator. Elements
can be arranged in either ascending or descending order, depending on whether the ``reverse`` argument is set. A list can also be easily reversed using
the ``reverse`` operator. For example: ::

    >>> a = [5,2,7,4,9]
    >>> a.sort()
    >>> a
    [2, 4, 5, 7, 9]
    >>> a.sort(reverse=True)
    >>> a
    [9, 7, 5, 4, 2]
    >>> mystring = "Old McDonald had a farm, Duda!"
    >>> words = mystring.split()
    >>> words.sort()
    >>> words
    ['Duda!', 'McDonald', 'Old', 'a', 'farm,', 'had']
    >>> words = mystring.split()
    >>> words.reverse()
    >>> words
    ['Duda!', 'farm,', 'a', 'had', 'McDonald', 'Old']

Similar to `Java <https://en.wikipedia.org/wiki/Java_(programming_language)>`_ or `C++ <https://en.wikipedia.org/wiki/C%2B%2B>`_,
`Python <https://www.python.org/>`_ assigns an `ASCII <https://en.wikipedia.org/wiki/ASCII>`_ code to all `alphanumeric <https://en.wikipedia.org/wiki/Alphanumeric>`_ characters,
where all capitalized letters have a lower ASCII code compared to their non-capitalized counterparts. This is why, for example, ``'Old'`` appears before ``'a'``
in the sorted list above.
The ``sort`` operator sorts all the elements of a list *in-place*,
so the order of the elements does change. One can also use the ``sorted``
operator that acts on a list and returns another list which is the sorted
version of the original list. Elements can also be sorted in reverse if the
``reverse`` argument is set. Finally, the length of a list can be obtained by
using the ``len`` keyword. ::

    >>> a = [5,2,7,4,9]
    >>> b = sorted(a)
    >>> b
    [2, 4, 5, 7, 9]
    >>> b = sorted(a,reverse=True)
    >>> b
    [9, 7, 5, 4, 2]
    >>> a
    [5, 2, 7, 4, 9]
    >>> len(a)
    5
