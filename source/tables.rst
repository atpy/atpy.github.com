Tables
======

The ``Table`` class is the basic entity. It consists of table data and metadata. The data is stored using a Numpy record array. The metadata includes units, null values, and column descriptions.

Data can be stored in the table using many of the Numpy types, including booleans, 8, 16, 32, and 64-bit signed and unsigned integers, 32 and 64-bit floats, and strings. Not all file formats and databases support reading and writing all of these types -- for more information, see :ref:`File Formats and Numeric Types <formats>`.

Creating a table
----------------

The simplest way to create an instance of the ``Table`` is to call the class with no arguments::

  >>> t = atpy.Table()

Populating the table
--------------------

A table can be populated either manually or by reading data from a file or database. Reading data into a table erases previous content. Data can be manually added once a table has been read in from a file.

Reading data from a file
^^^^^^^^^^^^^^^^^^^^^^^^

The ``read(...)`` method can be used to read in a table from a file. To date, ``ATpy`` supports the following file formats:

  * FITS tables (``fits``)
  * VO tables (``vo``)
  * IPAC tables (``ipac``)
  
When reading a table from a file, the only required argument is the filename. For example, to read a VO table called ``example.xml``, the following should be used::

  >>> t.read('example.xml')
  Auto-detected input type: VO table
  
The ``read()`` method will in most cases correctly identify the format of the file from the extension. As seen above, the default behavior is to specifically tell the user what format is being assumed, but this can be controlled via the ``verbose`` argument.
  
In some cases, ``read()`` will fail to determine the input type. In this case, or to override the automatically selected type, the input type can be specified using the ``type`` argument::

  >>> t.read('example.xml', type='vo')

The ``read`` method supports additional file-format-dependent options. These are described in more detail in the :ref:`Full API <api>`.

Reading data from a database
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Reading a table from a database is very similar to reading a table from a file. The main difference is that for databases, the first argument should be the database type, To date, ``ATpy`` supports the following database types:

  * SQLite (``sqlite``)
  * MySQL (``mysql``)
  * PostGreSQL (``postgres``)
 
The remaining arguments depend on the database type. For example, an SQLite database can be read by specifying the database filename::

  >>> t.read('sqlite','example.db')

For MySQL and PostGreSQL databases, it is possible to specify the database, authentication, and host parameters. The various options are descried in more detail in the :ref:`Full API <api>`. As for files, the ``verbose`` and ``type`` arguments can be used.

Adding data to a table
^^^^^^^^^^^^^^^^^^^^^^

It is possible to add data to an empty or an existing table. Two methods exist for this. The first, ``add_column``, allows users to add an existing array to a column. For example, the following can be used to add a column named ``time`` where the variable ``time_array`` is a Numpy array::

  t.add_column('time', time_array)
  
The ``add_column`` method also optionally takes metadata about the column, such as units, null values, and a description. For example::

  t.add_column('time', time_array, unit='seconds', null=-999.)
  
indicates that the units of the column are seconds, and that values of -999. should be treated as NULL. It is also possible to convert the datatype of an array while adding it to a table by using the ``dtype`` argument. For example, the following stores the column from the above examples as 32-bit floating point values::

  t.add_column('time', time_array, unit='seconds', null=-999., dtype=np.float32)
  
In some cases, it is desirable to add an empty column to a table, and populate it element by element. This can be done using the ``add_empty_column`` method. The only required arguments for this method are the name and the data type of the column::


  t.add_empty_column('id', np.int16)
  
If the column is the first one being added to an empty table, the ``shape`` argument should be used to specify the number of rows. This should either be an integer giving the number of rows, or a tuple in the case of vector columns (see :ref:`Vector Columns <vector_columns>` for more details)


Vector Columns
^^^^^^^^^^^^^^

.. _vector_columns:

As well as using one-dimensional columns is also possible to specify so-called vector columns, which are essentially two-dimensional arrays. Only FITS and VO tables support reading and writing these. The ``add_column`` method accepts two-dimensional arrays as input, and uses these to define vector columns. Empty vector columns can be created by using the ``add_empty_column`` method along with the ``shape`` argument to specify the full shape of the column. This should be a tuple of the form ``(n_rows, n_elements)``.

Accessing the data
------------------

The table data is stored in a Numpy record array, which can be accessed using the ``data`` attribute with the column name passed as a key. This returns the column in question as a Numpy array::

  t.data['column_name']
  
For convenience, columns with names that satisfy the python variable name requirements (essentially starting with a letter and containing no symbols apart from underscores) can be accessed directly as attributes of the table::

  t.column_name
  
Since the returned data is a Numpy array, individual elements can be accessed using::

  t.data['column_name'][row_number]
  
or::

  t.column_name[row_number]
  
Both notations can be used to set data in the table, for example::

  t.knigths[row_number] = 1
  
and::

  t.data['column_name'][row_number] = 1
  
are equivalent, and will set the element at ``row_number`` to 1

Accessing the metadata
----------------------

The metadata is stored in the ``columns`` attribute. To see an overview of the metadata, simply use::

  >>> t.columns
  
The metadata for a specific column can then be accessed by specifying the column name as a key::

  >>> t.columns['some_column']
  
The attributes of this object are ``dtype``, ``unit``, ``description``, ``null``, and ``format``.

Note: while the unit, description and format for a column can be modified using the columns attribute, the dtype and null values should not be modified in this way as the changes will not propagate to the data array.

Manipulating table columns
--------------------------

Columns can also be renamed and removed. To do this, one can use the ``remove_column``, ``remove_columns``, and ``rename_column`` methods. For example, to rename a column ``time`` to ``space``, one can use::

  >>> t.rename_column('time','space')

For more information, see the full API.

Accessing table rows
--------------------

The ``row(...)`` method can be used to access a specific row in a table::

  row = t.row(row_number)
  
This returns the row as a Numpy record. The row can instead be returned as a tuple of elements with python types, by using the ``python_types`` argument:

  row = t.row(row_number, python_types=True)
  
Two more powerful methods are available: ``rows`` and ``where``. The ``rows`` method can be used to retrieve specific rows from a table as a new ``Table`` instance::

  t_new = t.rows([1,3,5,2,7,8])
  
Alternatively, the ``where`` method can be given a boolean array to determine which rows should be selected. This is in fact very powerful as the boolean array can actually be written as selection conditions::

  t_new = t.where((t.id > 10) & (t.ra < 45.4) & (t.flag == 'ok'))

Global Table properties
-----------------------

One can access the number of rows in a table by using the python ``len`` function::

  >>> len(t)
  
In addition, the number of rows and columns can also be accessed with the ``shape`` attribute:

  >>> t.shape
  
where the first number is the number of rows, and the second is the number of columns (note that a vector column counts as a single column)

Writing the data to a file
--------------------------

Writing data to files or databases is done through the ``write`` method. The arguments to this method are very similar to that of the ``read`` data. The only main difference is that the ``write`` method can take an ``overwrite`` argument that specifies whether or not to overwrite existing files.

