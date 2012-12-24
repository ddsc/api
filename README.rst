API
------

This repository holds the DDSC Lizard API documentation.

Documentation: https://ddsc.github.com/api/


BUILD
------

To build the API documentation::

  $ pip install nensbuild
  $ nensbuild
  $ bin/sphinx

Sphinx needs a html directory to write the html files in. This bites the way gh-pages work. To work around this the file ``html`` is a symbolic link to this directory. 

Update the Documentation
--------------------------

The reStructeredText source can be found in the doc directory.
To update the documentation after a commit of the rst files::

  $ bin/sphinx
  $ git commit -a
  $ git push

The documentation will be updated and available at: https://ddsc.github.com/api/


