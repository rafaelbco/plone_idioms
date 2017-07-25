plone_idioms
============

Naming of generators 
--------------------


A generator is a `"a function which returns an iterator"`__. Should be named like ``iter_something``, where ``something`` should
refere to the thing that wil be returned in each iteration.

.. __: py2doc-glossary-generator


Examples
^^^^^^^^

.. code-block:: python

   def iter_even_numbers(max):
       for i in xrange(max + 1):
           if i % 2 == 0:
               yield i

   def iter_odd_numbers(max):
       return (i for i in xrange(max) if i % 2 != 0)


Rationale
^^^^^^^^^

* The name of the function makes it explicit that it is not returning a sequence, which can prevent errors. 

  For example, if in the example above the first function was called just ``even_numbers`` one could be mislead write 
  ``even_numbers(10)[2]`` in order get the third even number.

* In the stdlib there are the dict methods ``iteritems``, ``itervalues`` etc.

* Why not ``something_iter``? To maintain consistence with the well known dict methods mentioned above.

.. References:

.. py2doc-glossary-generator: https://docs.python.org/2/glossary.html#term-generator
