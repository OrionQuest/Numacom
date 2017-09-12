Dictionaries
------------

A dictionary is a mapping from a set of keys to a set of values. The data type
of a key or a value is not restricted in any way, and they can be either
integers, floats, strings, lists, or even another dictionary (although in this
case it is typically the value that is a dictionary, not the key). Unlike a list, a dictionary begins with
curly braces ``({})``, where each key-value pair is specified using the colon ``:`` operator.
For example: ::

    >>> scorecard = {'class':'CS 323','hw':92,'midterm':85,'final':95,'grade':'A'}
    >>> scorecard
    {'final': 95, 'grade': 'A', 'midterm': 85, 'class': 'CS 323', 'hw': 92}

The square bracket operator ``([])`` can be used
to retrieve the value associated with a given key. If the key is not already
present in the dictionary, then a new key-value pair is added to it, otherwise the original
value is modified to the newly specified value. Similar to lists, entries within a dictionary
can also be deleted using the ``del`` operator. ::

    >>> scorecard['class']
    'CS 323'
    >>> scorecard['hw']
    92
    >>> scorecard['class-participation'] = 0    # Very bad! :-(
    >>> scorecard
    {'midterm': 85, 'grade': 'A', 'class-participation': 0, 'hw': 92, 'class': 'CS 323', 'final': 95}
    >>> del scorecard['midterm']
    >>> scorecard
    {'grade': 'A', 'class-participation': 0, 'hw': 92, 'class': 'CS 323', 'final': 95}

`Python <https://www.python.org/>`_ provides an ``items`` function in every
dictionary which returns a list of all stored key-value pairs, and can be used to
conveniently loop over all the individual entries.
Note that the variable names ``key`` and ``value`` are not fixed, and one can
choose any other name as well. Since both the keys and the values can be of any
arbitrary data type, we explicitly convert them into a string for ease of
display. If only the keys are desired, but not the values, then the function
``keys`` can be used instead, which returns a list of all keys in the
dictionary. Likewise, if only the values are desired but not the keys, then the
function ``values`` can be used which returns a list of all values in the
dictionary. ::

    >>> for key,value in scorecard.items():
    ...     print 'Key: '+str(key)+', Value: '+str(value)
    ... 
    Key: grade, Value: A
    Key: class-participation, Value: 0
    Key: hw, Value: 92
    Key: class, Value: CS 323
    Key: final, Value: 95
    >>> scorecard.keys()
    ['grade', 'class-participation', 'hw', 'class', 'final']
    >>> scorecard.values()
    ['A', 0, 92, 'CS 323', 95]
