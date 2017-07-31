Python Coding Conventions and Idioms
====================================

Naming of generators 
--------------------

A generator is a `"a function which returns an iterator"`__. Should be named like ``iter_things``, where ``things`` should
refere to the things that wil be returned in each iteration.

__ https://docs.python.org/2/glossary.html#term-generator

Examples
^^^^^^^^

.. code-block:: python

   def iter_even_numbers(max):
       """Return an iterator over the even numbers up to `max`."""
       # Example using yield.
       for i in xrange(max + 1):
           if i % 2 == 0:
               yield i

   def iter_odd_numbers(max):
      """Return an iterator over the odd numbers up to `max`."""
       # Better style, returning a generator expression.
       return (i for i in xrange(max) if i % 2 != 0)

.. NOTE::
   The phrasing of the docstrings is based on ```dict.iteritems`` documentation`__ and is also recommended.
   
__ https://docs.python.org/2/library/stdtypes.html#dict.iteritems

Rationale
^^^^^^^^^

We follow what exists in the stdlib, in the ``dict`` class. There you have ``values``, ``keys`` and ``items`` methods,
which return sequences. There are also the generator version of theses methods: ``itervalues``, ``iterkeys`` and ``iteritems``. 

Of course we also follow PEP8_, which is not always followed in the stdlib. In order to conform to this recommendation the `dict` 
generator methods would be called  ``iter_values``, ``iter_keys`` and ``iter_items``.

Alternatives
^^^^^^^^^^^^

* *Name generators like ``things``*

  The name of the function makes it explicit that it is not returning a sequence, avoiding errors.

  For example, if in the examples section the first function was called just ``even_numbers``, one could be mislead and write 
  ``even_numbers(10)[2]`` in order get the third even number. This would raise an error.
  
* *Name generators like ``things_iter``*
  
  To be consistent with ``dict`` methods ``iterkeys``, ``itervalues`` and so on.
  
.. References:

.. PEP8: https://www.python.org/dev/peps/pep-0008
