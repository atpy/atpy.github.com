ATpy - Astronomical Tables in Python 
======================

`Sourceforge <http://sourceforge.net/projects/atpy/>`_ - `Download <https://sourceforge.net/projects/atpy/files/>`_ - `Mailing List <http://lists.sourceforge.net/lists/listinfo/atpy-announce>`_ - `Twitter <http://twitter.com/astropython/>`_ - `Forums <http://sourceforge.net/apps/phpbb/atpy/>`_ 

ATpy is a high-level package providing a way to treat tables of astronomical
data in a uniform and consistent way. A table is defined by any number of
columns of data, each characterized by a column name, unit, null value, and
description (the last three being optional), and can be supplemented with
metadata in the form of keywords or comments. ATpy can be used to manipulate
single tables as well as sets of tables.

Example code for reading, converting, and writing a data file from FITS table
to VO table, IPAC table, and SQLite::

    import atpy
    tbl = atpy.Table()
    tbl.read('some_fits_table_file.fits')
    
    # ATpy will automatically try to detect which type of file you're writing.
    tbl.write('new_votable.xml')                 # VO Table
    tbl.write('new_ipactable.tbl')               # IPAC table
    tbl.write('sqlite','new_sqlitetable.db')     # SQLite database
    
    # You can easily access and modify data in the table:
    tbl.data['some_column'][3] = 4.5
    tbl.remove_column('some_other_column')

It is also possible for example to create tables from scratch, add columns,
select rows from the table, override the automatically detected input/output
type, read/write tables in table sets rather than individual tables, etc. For
more details see the documentation below.

.. toctree::
  :maxdepth: 3

  installation.rst
  single_tables.rst
  table_sets.rst
  formats.rst

