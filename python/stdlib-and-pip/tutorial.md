---
layout: lesson
root: ../..
title: The Python Standard Library, and PyPI. 
---


# Standard Library

Quoting from the [About Python](http://www.python.org/about/) page, 'Fans of Python use the phrase "batteries included" to describe the standard library, which covers everything from asynchronous processing to zip files.'

The documentation for the Python 2 standard library can be found [here](http://docs.python.org/2/library/). 

Some modules we might find useful for bionformatics include

* String Services 

  * [Common string operations](http://docs.python.org/2/library/string.html)
  * [Regular expressions](http://docs.python.org/2/library/re.html)
  * [Parsing structured binary data](http://docs.python.org/2/library/string.html)

* Data Types

  * [Collections, various high performance container types](http://docs.python.org/2/library/collections.html)
  * [Shallow and deep copying of objects](http://docs.python.org/2/library/copy.html)

* Numeric and Mathematical Modules

  * [Random number generation](http://docs.python.org/2/library/numbers.html)

* Data Persistence

  * [Python object persistence](http://docs.python.org/2/library/shelve.html)
  * [sqlite3 lightweight relational database](http://docs.python.org/2/library/sqlite3.html)

* [Data Compression and Archiving](http://docs.python.org/2/library/archiving.html)

# Python module of the week

An excellent resource for learning more about modules in the standard library is [Python Module Of The Week](http://pymotw.com/2/).

# Installing packages from PyPI

[PyPI or the Python Package Index](https://pypi.python.org/pypi) is a repository for sharing 3rd party python modules, and currently contains more than 35k modules. Currently the prefered tool for installing packages from PyPI is `pip` 

To install a package, simply execute `pip install PackageName`. To install a specific version of a package, `pip install PackageName==Version`. To upgrade to the latest version available in PyPI `pip install --upgrade`. 

By default, pip will attempt to install packages globally, which may require root access, and which may not be available to you on a shared system. As of Python 2.6 per-user package installation is easily supported. Simply add the user option, e.g. `pip install package --user` to install the package under your home directory to a path that will automatically be searched. see [PEP-0370](http://www.python.org/dev/peps/pep-0370/) for more information.