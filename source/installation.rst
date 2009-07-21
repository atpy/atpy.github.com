.. toctree::
  :maxdepth: 2
  
Installation
------------

ATpy relies on a number of different packages to support reading and writing to
different file or database formats. However, the only compulsory package is
NumPy. All other requirements are optional - if they are not present, the
relevant read/write methods will be disabled but will not otherwise prevent
ATpy from functioning.

Below is a table showing what ATpy depends on for full functionality and what
may need to be installed. We suggest that the user employs Python 2.5 at the
minimum for this module. Python 2.6 is preferred as SQLite is included by
default.

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

Setuptools
^^^^^^^^^^
Before installing ATpy, you will need setuptools_ installed. This is a Python package that many users now use to install packages. If you're already using the easy_install command to install Python packages on your computer, then setuptools is already installed! Visit the setuptools_ page on the Python Cheese shop if want directions on downloading and installing setuptools.  

Aside from making Python packages easier to install with setuptools we use a robust program (pkg_resources) in setuptools. The program rigorously checks ATpy dependencies to make sure they are correctly installed and up to date. This will save ATpy users a lot of headaches if ATpy is not behaving as expected.  

ATpy
^^^^

To install ATpy itself, run::

    easy_install atpy

or, if easy_install is not available::

    tar xvzf ATpy-X-X.X.tar.gz
    cd ATpy-X.X.X/
    python setup.py install




NumPy
^^^^^

ATpy requires numpy-1.3.0 or later. There are three different ways to install numpy_.

If you are starting off with python, you should consider using the Enthought
Python Distribution (EPD_), which is an easy-to-install python distribution
that contains many packages including the NumPy, SciPy (a bonus), and
Matplotlib modules (another bonus!).

Alternatively, you can download the required packages from the numpy_ website
and install it the standard way::

    tar xvzf numpy-1.3.0.tar.gz
    cd numpy-1.3.0
    python setup.py install

Finally, a third alternative, if you have easy_install installed, is::

    easy_install numpy

PyFITS
^^^^^^

In order to read/write FITS files, APLpy requires pyfits-2.1 or later to be
installed. The pyfits_ module is developed at the Space Telescope Science
Institute (STScI). Once you have the tar file downloaded, you can either
install it using the standard installation method::

    tar xvzf pyfits-2.1.1.tar.gz
    cd pyfits-2.1.1
    python setup.py install

or using easy_install::

     easy_install pyfits-2.1.1.tar.gz 

vo
^^

To read/write VO tables you need to have STScI's vo_ package installed (version
0.3 or greater). The vo-0.3.tar.gz package is broken at the moment, so it's
suggested to install the vo_ package from subversion::

    easy_install https://www.stsci.edu/svn/ssb/astrolib/trunk/vo

or alternatively::

    svn co https://www.stsci.edu/svn/ssb/astrolib/trunk/vo
    cd vo
    python setup.py install

SQL
^^^

In the SQL domain ATpy supports three database types: MySQL, PostgreSQL, and
SQLite. The first two are typical SQL database managers. SQLite_ falls into its
own category as does not need special access or installation to get it working.
As of Python 2.6 or above, SQLite_ is installed by default. If you are working
from Python 2.5 and do not have it installed you can use easy_install::

    easy_install pysqlite

If you have MySQL already installed and want to access the DB manager with ATpy
you will need to have MySQL-python (1.2.2 or greater) installed. Using
easy_install you can do the following::

    easy_install mysql-python

Similarly, if PostgreSQL is installed you will need to install PyGreSQL_
(version 4.0 or greater)::

    easy_install pygresql

Testing your ATpy Installation
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

If you have ATpy and the desired dependencies installed you can run a smoke
test to verify that the features are working. Here's how you test your ATpy
installation::

    cd ATpy-X.X.X/
    python test/test.py

The output should look like the following:: 

    WARNING - MySQL-python 1.2.2 or later required. MySQL table reading/writing has been disabled
    WARNING - PyGreSQL 3.8.1 or later required. PostGreSQL table reading/writing has been disabled
    Reading IPAC Table ...  passed
    Writing VO Table ...  passed
    Writing FITS Table ...  passed
    ...
    ...
    ...
    Reading in FITS Table set ...  passed
    Writing VO Table ...  passed
    Writing FITS Table ...  passed
    Writing IPAC Table ...  passed
    Converting to PostGreSQL database ...  failed
    Converting to SQLite database ...  passed
    Converting to MySQL database ...  failed

The "WARNING" messages should correlate to the "failed" tests. For example, the
output from above states that the MySQL-python and PyGreSQL requirements are
not met. Hence these features are disabled and the tests using these modules
will naturally fail. If the "passed" tests correlate to your desired ATpy
features, then you're all set.

.. _pyfits: http://www.stsci.edu/resources/software_hardware/pyfits
.. _vo: http://www.stsci.edu/trac/ssb/astrolib
.. _mysql: mysql-python <http://sourceforge.net/projects/mysql-python
.. _pygresql: http://www.pygresql.org/
.. _PyGreSQL: http://www.pygresql.org/
.. _NumPy: http://numpy.scipy.org/
.. _SQLite: http://docs.python.org/library/sqlite3.html
.. _EPD: http://www.enthought.com/products/epd.php
.. _setuptools: http://pypi.python.org/pypi/setuptools/

