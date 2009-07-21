ATpy - Astronomical Tables in Python 
======================

ATpy is a high-level package providing a way to treat tables of astronomical data with a uniform and consistent API. A table is defined by any number of columns of data, each characterized by a column name, unit, null value, and description (the last three being optional), and can be supplemented with metadata in the form of keywords or comments. ATpy can be used to manipulate single tables as well as sets of tables.

Example code for reading, converting, and writing a data file from FITS table to VO table, IPAC table, and SQLite::

    import atpy
    tbl = atpy.Table()
    tbl.read('some_fits_table_file.fits')
    
    # ATpy will automatically try to detect which type of file you're writing.
    tbl.write('new_votable.xml')
    tbl.write('new_ipactable.tbl')
    
    # If you would prefer, you can tell ATpy what type you want to write. 
    tbl.write('new_sqlitetable.db',type='sql')


.. toctree::
  :maxdepth: 2

  installation.rst
  single_tables.rst
  table_sets.rst
  formats.rst
