Installation
------------

ATpy relies on a number of different packages to support different table formats. To install ATpy itself, running::

    easy_install atpy
    
or manually installing using::

    python setup.py install
    
will be sufficient.

 
                                             
=============    ================================
  Format         Required Package                
=============    ================================
   IPAC          none                            
   FITS          pyfits_                         
   VO            vo_                      
   SQLite        sqlite3 (built into Python 2.6) 
   MySQL         mysql_                          
   PostGreSQL    pygresql_                     
=============    ================================
   
.. _pyfits: http://www.stsci.edu/resources/software_hardware/pyfits
.. _vo: http://www.stsci.edu/trac/ssb/astrolib
.. _mysql: mysql-python <http://sourceforge.net/projects/mysql-python
.. _pygresql: http://www.pygresql.org/