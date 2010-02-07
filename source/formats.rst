.. _formats:

=================
Supported Formats
=================

Unless stated otherwise below, all table types support the following types:

* ``np.bool``: booleans
* ``np.int8``, ``np.int16``, ``np.int32``, ``np.int64``: 8-, 16-, 32-, and 64- bit signed integer numbers.
* ``np.uint8``, ``np.uint16``, ``np.uint32``, ``np.uint64``: 8-, 16-, 32-, and 64- bit unsigned integer numbers.
* ``np.float32``, ``np.float64``: 32- and 64-bit floating point numbers.
* ``np.str``: ASCII strings

Below are the descriptions of the options available for the built-in datatypes. Note that the functions should not be called directly - all reading and writing should be done through the ``read()`` and ``write()`` methods for ``Table`` and ``TableSet``:

.. automodule:: atpy
    
FITS Table
----------

.. autofunction:: atpy.fitstable.read
.. autofunction:: atpy.fitstable.write

FITS Table Set
--------------

.. autofunction:: atpy.fitstable.read_set
.. autofunction:: atpy.fitstable.write_set

IPAC Table
----------

.. autofunction:: atpy.ipactable.read
.. autofunction:: atpy.ipactable.write

VO Table
--------

.. autofunction:: atpy.votable.read
.. autofunction:: atpy.votable.write

VO Table Set
------------

.. autofunction:: atpy.votable.read_set
.. autofunction:: atpy.votable.write_set

SQL Table
---------

.. autofunction:: atpy.sqltable.read
.. autofunction:: atpy.sqltable.write

SQL Table Set
-------------

.. autofunction:: atpy.sqltable.read_set
.. autofunction:: atpy.sqltable.write_set

