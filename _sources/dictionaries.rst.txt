Dictionaries
------------

A dictionary is a mapping from a set of keys to a set of values. The data type
of a key or a value is not restricted in any way, and they can be either
integers, floats, or strings. Unlike a list, a dictionary begins with
curly braces ``({})``, where each key-value pair is specified using the ``:`` operator.
For example: ::

    >>> scorecard = {'class':'CS 323','hw':92,'midterm':85,'final':95,'grade':'A'}
    >>> scorecard
    {'final': 95, 'grade': 'A', 'midterm': 85, 'class': 'CS 323', 'hw': 92}

The square bracket operator ``([])`` can be used
to retrieve the value associated with a given key. If the key is not already
present in the dictionary, then a new key-value pair is added to it, otherwise the original
value is modified to the newly specified value. ::

    >>> scorecard['class']
    'CS 323'
    >>> scorecard['hw']
    92
    >>> scorecard['class-participation'] = 0    # Very bad! :-(
    >>> scorecard
    {'midterm': 85, 'grade': 'A', 'class-participation': 0, 'hw': 92, 'class': 'CS 323', 'final': 95}
