.. _parsingdata:

Parsing Bibliographic Data
==========================

.. note:: For instructions on acquiring bibliographic data from several sources,
          see :ref:`gettingdata`.

Tethne provides several parsing modules, located in :mod:`tethne.readers`. The
recommended pattern for parsing data is to import the parsing module
corresponding to your data type, and use its' ``read`` function to parse your
data. For example:

.. code-block:: python

   >>> from tethne.readers import wos
   >>> myCorpus = wos.read('/path/to/my/data.txt')

By default, ``read`` will return a :class:`.Corpus` object.

.. code-block:: python

   >>> myCorpus
   <tethne.classes.corpus.Corpus object at 0x1046aa7d0>

Depending on which module you use, ``read`` will make assumptions about which
field to use as the primary index for the :class:`.Paper`\s in your dataset.
The default for Web of Science data, for example, is ``'wosid'`` (the value of
the ``UT`` field-tag).

.. code-block:: python

   >>> myCorpus.index_by
   'wosid'

If you'd prefer to index by a different field, you can pass the ``index_by``
parameter.

.. code-block:: python

   >>> myOtherCorpus = wos.read('/path/to/my/data.txt', index_by='doi')
   >>> myOtherCorpus.index_by
   'doi'

The following sections describe the behavior of each of the parsing modules.

.. contents::
   :local:
   :depth: 2

Web of Science
--------------

To parse a Web of Science field-tagged file, or a collection of field-tagged
files, use the :func:`.tethne.readers.wos.read` method.

To parse a single file, provide the path to that data file. For example:

.. code-block:: python

   >>> from tethne.readers import wos
   >>> corpus = wos.read('/path/to/my/data.txt')
