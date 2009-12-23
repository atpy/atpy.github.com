Single Tables
=============

A ``Table`` is the basic entity in ATpy. It is composed of a Numpy array, that stores the data, and metadata that describes the contents of the table. This metadata includes units, null values, and column descriptions. Data can be stored using many of the Numpy types, including booleans, 8, 16, 32, and 64-bit signed and unsigned integers, 32 and 64-bit floats, and strings. Not all formats support reading and writing all of these types -- for more information, see [ref]. The simplest way to create an instance of the ``Table`` is to call the class with no arguments::

  >>> t = atpy.Table()
  >>> 

The table can then be populated either manually or by reading data from a file or database.

Reading data from a file
------------------------

``Table`` instances can be filled by reading data from a file or database. To do this, simply call the ``read()`` method::

  >>> t.read(...)

The arguments to pass to read depend on the file or database type. For file formats, such as FITS, VO, and IPAC tables, the only required argument is the filename. For example, to read a VO table called ``sometable.xml``, simply use::

  >>> t.read('sometable.xml')
  Auto-detected input type: VO table
  >>>
  
The ``read()`` method will in most cases correctly identify the format of the file. As seen above, the default behavior is to specifically tell the user what format is being assumed, but this can be disabled with the ``verbose`` argument:

  >>> t.read('sometable.xml', verbose=False)
  >>>
  
In some cases, ``read()`` will fail to determine the input type. In this case, or to override the automatically selected type, the input type can be specified using the ``type`` argument::

    t.read('sometable.xml',type='vo')
    
A list of valid file formats is given in [ref]. The ``read`` method n addition to the ``verbose`` and ``type`` arguments



Adding columns to a table
-------------------------


Quick start
-----------

Initialization
^^^^^^^^^^^^^^^

The easiest way to create a single table object is to call the ``Table`` class with no arguments::

    t = Table()

Manually filling a table
^^^^^^^^^^^^^^^^^^^^^^^^

A table can be filled manually using the ``add_column`` method. For example, the following can be used to add a column named `time` where the variable `time_array` is a numpy array::

    t.add_column('time',time_array,unit='seconds')

Reading in data from a file or database
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Alternatively, the ``read()`` method can be used to read in data from a file or database. This method automatically determines the file or database type and reads in the data. For example, a VO table can be read in using::

    t.read('somedata.xml')
    
while a FITS table can be read in using::

    t.read('somedata.fits')

In some cases, ``read()`` will fail to determine the input type. In this case, or to override the automatically selected type, the input type can be specified using the type argument::

    t.read('somedata.fits.gz',type='fits')
    
Reading in data when creating a table
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Any arguments passed to ``Table()`` when creating a table instance are passed to the ``read()`` method. This can be used to create a ``Table()`` instance and fill it with data in a single line. For example, the following::

    t = Table('somedata.xml')
    
is equivalent to::

    t = Table()
    t.read('somedata.xml')
    
Writing a table to a file or database
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
    
Similarly, data can be output to a file or database using the ``write()`` method. As for ``read``, the output type is automatically determined, but if this fails or to override the automatic choice, the ``type`` argument should be used::

    t.write('somedata.xml')
    t.write('somedata',type='ipac')    

Accessing table data
^^^^^^^^^^^^^^^^^^^^

Data is stored in dictionary named ``data``. Each element in the dictionary is a 1-D array (or 2-D in the case of vector columns). Therefore, the data is accessed using ``Table.data[column_name][element]`` where ``column_name`` is a string and ``element`` is an integer denoting the row. To access the fifth row of a column named ``wavelength``, one would then use::

    t.data['wavelength'][4]
    
For column names that are considered acceptable python variable names can also by calling the table with the column name as a table attribute, so that the above can also be written::

    t.wavelength[4]
    
Only column names consisting of letters (uppercase or lowercase), numbers, and the underscore symbol are acceptable. Column names with spaces, starting with a number, or containing other symbols cannot be called in this way.

Manipulating tables
^^^^^^^^^^^^^^^^^^^

A number of methods are available to manipulate tables, for example to add or remove columns, to select rows from a table and create a new table, to rename columns, or to add comments and keywords. The full API for the ``Table`` class methods is given below.

Full API
--------

The following methods are available:

.. automodule:: atpy
    
Input/Output
^^^^^^^^^^^^

.. automethod:: Table.read
.. automethod:: Table.write

To browse the API of the ``read()`` and ``write()`` methods for the different table types, see :doc:`formats`.  
    
Column manipulation
^^^^^^^^^^^^^^^^^^^

.. automethod:: Table.add_column
.. automethod:: Table.remove_column
.. automethod:: Table.remove_columns
.. automethod:: Table.keep_columns
.. automethod:: Table.rename_column

Meta-data
^^^^^^^^^

.. automethod:: Table.add_comment
.. automethod:: Table.add_keyword
.. automethod:: Table.describe

Row selection
^^^^^^^^^^^^^

.. automethod:: Table.where
