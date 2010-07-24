====================================
ATpy - Astronomical Tables in Python 
====================================

`Sourceforge <http://sourceforge.net/projects/atpy/>`_ - `Download <https://sourceforge.net/projects/atpy/files/>`_ - `Mailing List <http://lists.sourceforge.net/lists/listinfo/atpy-announce>`_ - `Twitter <http://twitter.com/astropython/>`_ - `Forums <http://sourceforge.net/apps/phpbb/atpy/>`_  - `Report Bugs <https://sourceforge.net/tracker/?group_id=259666&atid=1280111>`_ - `Requests Features <https://sourceforge.net/tracker/?group_id=259666&atid=1280112>`_

ATpy is a high-level Python package providing a way to manipulate tables of
astronomical data in a uniform way. The two main features of ATpy are:

* It provides a Table class that contains data stored in a NumPy structured
  array, along with meta-data to describe the columns, and methods to
  manipulate the table (e.g. adding/removing/renaming columns, selecting rows,
  changing values, sorting, ...).

* It provides built-in support for reading and writing to several common
  file/database formats, including FITS, VO, HDF5, and ASCII tables, and
  SQLite, MySQL and PostgreSQL databases, with a very simple API.

In addition, ATpy provides a TableSet class that can be used to contain
multiple tables, and supports reading and writing to file/database formats
that support this (FITS, VO, and SQL databases).

Finally, ATpy provides support for user-written read/write functions for
file/database formats not supported by default. We encourage users to send
us custom read/write functions to read commonly used formats, and would be
happy to integrate them into the main distribution.

The following example shows how ATpy can be used to read, convert, and
write a data file from FITS format to VO, HDF5, IPAC, and SQLite formats::

    import atpy
    tbl = atpy.Table('some_fits_table_file.fits')
    
    # ATpy will automatically try to detect which type of file you're writing.
    tbl.write('new_votable.xml')                 # VO Table
    tbl.write('new_ipactable.tbl')               # IPAC table
    tbl.write('new_ipactable.hdf5')              # HDF5 table
    tbl.write('sqlite','new_sqlitetable.db')     # SQLite database
    
    # You can easily access and modify data in the table:
    tbl.some_column[3] = 4.5
    tbl.remove_column('some_other_column')

This is only a small fraction of ATpy's functionality. We strongly recommend that users read through the documentation, which is available below. For a quick introduction, we recommend the :ref:`tables` and :ref:`data` sections. For information about format-specific features, see :ref:`formats`.

Documentation
-------------

.. toctree::
  :maxdepth: 2

  installation.rst
  tables.rst
  data.rst
  manipulating.rst
  table_sets.rst
  masking.rst
  developers.rst
  formats.rst
  api_table.rst
  api_tableset.rst
