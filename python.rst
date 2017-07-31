Python Coding Conventions and Idioms
====================================

.. contents::

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

- *Name generators like ``things``*

  The name of the function makes it explicit that it is not returning a sequence, avoiding errors.

  For example, if in the examples section the first function was called just ``even_numbers``, one could be mislead and write 
  ``even_numbers(10)[2]`` in order get the third even number. This would raise an error.
  
- *Name generators like ``things_iter``*
  
  To be consistent with ``dict`` methods ``iterkeys``, ``itervalues`` and so on.
  
  
Function docstrings
-------------------

Should follow PEP257_ fully complemented with the conventions explained in the examples. If something is not well explained,
adapt from `Google docstrings style`_.

Examples
^^^^^^^^

Full example:

.. code-block:: python

   def get_furfles_value(foo, bar=3, prefix=None):
       u"""Get the furfles value.
       
       The furfles value is computed by adding `foo` and `bar` and optionally prefixing it with an
       string.
       
       Explain details in these opening paragraphs in order to make the other sections (Arguments, 
       Return, etc) more succint.
       
       Note: Maybe add a note.
           Which can span more than one line, indentend.
           
           Maybe another paragraph.
           
           - Any kind of rST markup, but keep it simple.
           - Like lists, which are ok.
           
           Other arbitrary free-form sections like this can be added, like "Implementation details" and 
           "Caching".
           
           The following sections, which are more common, must be kept in the end.
                    
       Arguments:
       foo (float) -- Foo value.
       bar (Optional[int]) -- Bar value. Do not write the default value. It's already in the
           function signature.
           
           Maybe you'll need another paragraph to describe an argument. But try to avoid.           
       prefix (Optional[str]) -- Text to be inserted before the value.                     
       
       Return (str): The computed furfles value.
           If a second line is necessary then it's identend.
           
       Raises:
       `ValueError` -- If some condition is not met. 
       `RuntimeError` -- If other condition is not met.
           Second line is indented.
       """
       return '{}{}'.format((label or ''), foo + bar)

Anything can be ommited, if it's obvious: type specs, arguments descriptions (sometimes the name is sufficient). Sometimes
only the function descriptions is sufficent. And sometimes the entire dosctring is superfulous.

Example ommiting obvious information:

.. code-block:: python

   def get_furfles_value(foo, bar=3, prefix=None):
       u"""Get the furfles value.
       
       Note: In the Arguments section bellow we ommit the descriptions. If we wanted to ommit the type as well 
           then it would be better to ommit the whole section. Listing only the arguments names is useless since
           we already have the function signature.

       Arguments:
       foo (float)
       bar (Optional[int])
       prefix (Optional[str])           
       
       Return (str)
       """
       return '{}{}'.format((label or ''), foo + bar)

Rationale
^^^^^^^^^

- Follow PEP257_ fully.
- Keep consistency with current style which is based on examples given in PEP257_.
- Borrow ideas from `Google docstrings style`_.
- Use PEP484_ to specify types, when desired.
- Nothing is required. You can ommit what is obvious.
- Do not repeat what is in the function signature, eg: default values.
  
.. References:

.. _PEP8: https://www.python.org/dev/peps/pep-0008
.. _PEP257: https://www.python.org/dev/peps/pep-0257
.. _PEP484: https://www.python.org/dev/peps/pep-0484/
.. _`Google docstrings style`: https://sphinxcontrib-napoleon.readthedocs.io/en/latest/example_google.html
