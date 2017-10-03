User Inputs
-----------

`Python <https://www.python.org/>`_ provides a convenient mechanism for
accepting all inputs given by the user via the ``raw_input`` command, which
interprets all inputs as a *string* value. For example: ::

    >>> name = raw_input("Welcome to CS 323! To get started, please enter your name: ")
    Welcome to CS 323! To get started, please enter your name: John
    >>> print 'Hi %s!'%name
    Hi John!

.. note::
    
    If you are using Python 3, then you should use the ``input`` command instead
    of the ``raw_input`` command described above, which has the same syntax. The
    ``raw_input`` command is valid for Python 2.7. While there is an ``input``
    command in Python 2.7 as well, it interprets the user input as Python code
    and tries to execute it.

As mentioned above, the output of the ``raw_input`` command is a *string*
value. Quite often, we wish to ask for an integer or floating-point value
from the user. In this case, the output should be explicitly type casted into the
desired format, as shown below: ::

    >>> value = raw_input("Please enter your score from Homework 1: ")
    Please enter your score from Homework 1: 90
    >>> score = int(value)
    >>> print score
    90
    >>> value = raw_input("Which version of Python are you using? ")
    Which version of Python are you using? 2.7
    >>> version = float(value)
    >>> print version
    2.7

