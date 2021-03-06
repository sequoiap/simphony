.. _howto-build-docs:

============================================
Building the Simphony API and reference docs
============================================

We currently use Sphinx_ for generating the API and reference
documentation for Simphony.  
.. You will need Sphinx >= 2.2.0.

If you only want to get the documentation, note that pre-built
versions can be found at

    https://simphonyphotonics.readthedocs.io/

in several different formats.

.. _Sphinx: http://www.sphinx-doc.org/


Instructions
------------

Building the documentation requires the Sphinx extension
`plot_directive`, which is shipped with Matplotlib_. This Sphinx extension can
be installed by installing Matplotlib. You will also need Python>=3.6.

Since large parts of the main documentation are obtained from Simphony via
``import simphony`` and examining the docstrings, you will need to first build
Simphony, and install it so that the correct version is imported.

Simphony has dependencies on other Python projects. Be sure to install its
requirements, listed in ``requirements.txt``.

Note that you can eg. install Simphony to a temporary location and set
the PYTHONPATH environment variable appropriately.
Alternatively, if using Python virtual environments (via e.g. ``conda``,
``virtualenv`` or the ``venv`` module), installing Simphony into a
new virtual environment is recommended.
All of the necessary dependencies for building the Simphony docs can be installed
with::

    pip install -r doc_requirements.txt

Now you are ready to generate the docs, so write::

    make html

in the ``doc/`` directory. If all goes well, this will generate a
``build/html`` subdirectory containing the built documentation. 

Note that building the documentation on Windows is currently not actively
supported, though it should be possible. (See Sphinx_ documentation
for more information.)

To build the PDF documentation, do instead::

   make latex
   make -C build/latex all-pdf

You will need to have Latex installed for this, inclusive of support for
Greek letters.  For example, on Ubuntu xenial ``texlive-lang-greek`` and
``cm-super`` are needed.  Also ``latexmk`` is needed on non-Windows systems.

Instead of the above, you can also do::

   make dist

which will rebuild Simphony, install it to a temporary location, and
build the documentation in all formats. This will most likely again
only work on Unix platforms.

The documentation for Simphony distributed at 
https://simphonyphotonics.readthedocs.io/ in html and
pdf format is also built with ``make dist``.  See `HOWTO RELEASE`_ for details
on how to update https://simphonyphotonics.readthedocs.io/.

.. _Matplotlib: https://matplotlib.org/
.. _HOWTO RELEASE: https://simphonyphotonics.readthedocs.io/

.. FIXME: Update the link for HOWTO RELEASE

Sphinx extensions
-----------------

Simphony's documentation uses several Sphinx extensions. While the
code docstrings are written using the `numpydoc`_ standard, we
actually use Sphinx's built-in `napolean`_ extension to parse
our files. Napolean has been included in the standard Sphinx since
version 1.3, so no special parsing extensions are required to generate this
documentation.

.. _numpydoc: https://python.org/pypi/numpydoc
.. _napolean: https://www.sphinx-doc.org/en/master/usage/extensions/napoleon.html
