Installation
------------

ATpy relies on a number of different packages to support different table formats. To install ATpy itself, run::

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
   

NumPy
-----------
ATpy requires NumPy-1.3.0 or later. There are three different ways to install NumPy_.

If you are starting off with python, you should consider using the Enthought Python Distribution (EPD), which is an easy-to-install python distribution that contains many packages including the NumPy, SciPy (a bonus), and Matplotlib modules (another bonus!). 

Alternatively, you can download the required packages from the NumPy_ and install it the standard way::

    tar xvzf NumPy-1.3.0.tar.gz
    cd NumPy-1.3.0
    sudo python setup.py install

Finally, a third alternative, if you have easy_install installed, is:: 

    easy_install NumPy


PyFITS
-----------
In order to read/write FITS files, APLpy requires pyfits-2.1 or later to be installed. The pyfits_ module is developed at the Space Telescope Science Institute (STScI). Once you have the tar file downloaded, you can either install it using the standard installation method:: 

    tar xvzf pyfits-2.1.1.tar.gz
    cd pyfits-2.1.1
    sudo python setup.py install

or using easy_install::

     easy_install pyfits-2.1.1.tar.gz 


vo
-----------
To read/write VO tables you need to have STScI's vo_ package installed (version 0.3 or greater). The vo-0.3.tar.gz package is broken at the moment, so it's suggested to install the vo_ package from subversion:: 

    easy_install https://www.stsci.edu/svn/ssb/astrolib/trunk/vo

SQL
-----------
In the SQL domain ATpy supports three database types: MySQL, PostgreSQL, and SQLite. The first two are typical SQL database managers. SQLite_ falls into its own category as does not need special access or installation to get it working. As of Python 2.6 or above, SQLite_ is installed by default. If you are working from Python 2.5 and do not have it installed you can use easy_install:: 

    easy_install pysqlite

If you have MySQL already installed and want to access the DB manager with ATpy you will need to have MySQL-python (1.2.2 or greater) installed. Using easy_install you can do the following::

    easy_install mysql-python

Similarly, if PostgreSQL is installed you will need to install PyGreSQL_ (version 4.0 or greater):: 

    easy_install pygresql














.. _pyfits: http://www.stsci.edu/resources/software_hardware/pyfits
.. _vo: http://www.stsci.edu/trac/ssb/astrolib
.. _mysql: mysql-python <http://sourceforge.net/projects/mysql-python
.. _pygresql: http://www.pygresql.org/
.. _PyGreSQL: http://www.pygresql.org/
.. _NumPy: http://numpy.scipy.org/
.. _SQLite: http://docs.python.org/library/sqlite3.html

