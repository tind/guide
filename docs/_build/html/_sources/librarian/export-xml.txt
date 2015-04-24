..  This file is part of Invenio
    Copyright (C) 2014 CERN.

    Invenio is free software; you can redistribute it and/or
    modify it under the terms of the GNU General Public License as
    published by the Free Software Foundation; either version 2 of the
    License, or (at your option) any later version.

    Invenio is distributed in the hope that it will be useful, but
    WITHOUT ANY WARRANTY; without even the implied warranty of
    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU
    General Public License for more details.

    You should have received a copy of the GNU General Public License
    along with Invenio; if not, write to the Free Software Foundation, Inc.,
    59 Temple Place, Suite 330, Boston, MA 02111-1307, USA.

.. _export-xml:

Export data
===========

1. Overview
-----------

This guide gives describes how data can be exported from Invenio. 

2. Export records as xml.-files
-------------------------------

There are predominantly two methods of exporting records as xml.-files in Invenio: 

  - The first method has the advantage of finding the desired records fast, but has the disadvantage
    of being slow to load the search result as MARCXML. This is only a problem if the result contains many records.
  - The second method is quick to run after it is set up but has the disadvantage of requiring access as a system librarian.

2.1 By the user interface
~~~~~~~~~~~~~~~~~~~~~~~~~

It is possible to export both multiple and single records as MARCXML from the user interface.
Single records are exported from the detailed view, while multiple records are exported
in brief view. For multiple records, first query the desired records, example ``980:"ARTICLE" AND author:"Polyakov, A M" AND 962__r:"002"``.
Then choose export format MARCXML.  

|tag-cloud for document export-xml/001|

.. |tag-cloud for document export-xml/001| image:: /_static/librarian/export-xml1.png

The url will look similar to this:

.. code-block:: console

    https://yoursite.com/search?sf=&so=d&rg=10&sc=1&c=Article&c=&of=xm&ln=en&cc=Article&p=980%3A%22ARTICLE%22+AND+962__r%3A%002%22&f=``


``rg=10``  means number of records displayed in the search results at ones. 
This number can be set to be equal to the numbers of records in the search result. 

The url can be further modified to export the exact data-fields that is wanted:
by adding ``ot=001,245,260`` only data-field 001, 245 and 260 will be export exported.


Afterwords, save the page as an xml.-file.

 

2.2 By BibExport
~~~~~~~~~~~~~~~~

First change this config file: ``/opt/invenio/etc/bibexport/marcxml.cfg``

The MARCXML exporting method export all the records
matching a particular search query, zip them and move them to the
requested folder. The output of this exporting method is similar to
what one would get by listing the records in MARCXML from the web
search interface. 

Default configurations are given below. The job would have exported all records from the Book 
collection into one xml.-file and all articles with the author "Polyakov, A M" into another.  

::

    [export_job]
    export_method = marcxml
    [export_criterias]
    books = 980__a:BOOK
    polyakov_articles = 980__a:ARTICLE and author:"Polyakov, A M"
    


the job is run by this command:

.. code-block:: console

    /opt/invenio/bin/bibexport -u admin -wmarcxml


Default folder for storing is:

.. code-block:: console

    /opt/invenio/var/www/export/marcxml


2. Export records in Excel
--------------------------
It is possible to export the data in Excel. Follow the instruction from section 2.1 and 
as the last step, change out ``of=xm`` with ``of=excel``

.. code-block:: console

    https://yoursite.com/search?sf=&so=d&rg=10&sc=1&c=Article&c=&of=excel&ln=en&cc=Article&p=980%3A%22ARTICLE%22+AND+962__r%3A%002%22&f=``



