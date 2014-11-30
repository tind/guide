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

.. _restrict-documents:

Make documents restricted
=========================

There are several ways to restrict documents in Invenio. Three of the procedures are shown below. The examples below assume a bibliographic record already exists. 

Note: Documents becomes restricted if they have a restriction status in marc field 856__r, example ``856__r = Private``. The restriction status is selectable, but it is important that it matches the restriction status defined in WebAccess for the specific role.

1. Change the restriction status in Document File Manager
---------------------------------------------------------

It is possible to add restriction to a file through "Document File Manager".  This can be done for new and existing files. The default restriction status is "Private" and cannot be changed.


|tag-cloud for document restr-cod/001|

.. |tag-cloud for document restr-cod/001| image:: /_static/librarian/restrict-documents1.png



2. Upload xml.-file through Batch Uploader
------------------------------------------

If you would like to add a file to an existing record, the xml.-file should look like this:

Afterwords run the "correct" mode in Batch Uploader.

::

	<record>
  		<controlfield tag="001">310</controlfield>
			<datafield tag="FFT">
			<subfield code="a">https://tools.tind.io/uploads/pdf/Demo document.pdf</subfield>
			<subfield code="r">Private</subfield>
		</datafield>
	</record>

Afterwords run the "append" mode in Batch Uploader. 


If the file is already in the database, the xml.-file should look like this:

::

	<record>
		<controlfield tag="001">310</controlfield>
		<datafield tag ="FFT" ind1=" " ind2=" ">
			<subfield code="n">1407</subfield>
			<subfield code="f">.pdf</subfield>
			<subfield code="d">KEEP-OLD-VALUE</subfield>
			<subfield code="z">KEEP-OLD-VALUE</subfield>
			<subfield code="r">restricted</subfield>
		</datafield>
	</record>

Here it creates a restriction status for an existing file named 1407.pdf belonging to record 310. 

Afterwords run the "correct" mode in Batch Uploader.

This step should be used together with a xml creation tools. See example of how it can be done with `TIND xml manipulation <xml-manipulation>`__ 

Check out `TIND xml manipulation <tools/xml-manipulation>`__ for more help.

3. Change the restriction Command based
---------------------------------------

The command below creates an xml as above and runs the “correct”-mode automatically.

The command ``sudo -u www-data /opt/invenio/bin/bibdocfile -r 310 --set-restriction=Private``
will set restriction for all the files attached to the given record.

The command ``sudo -u www-data /opt/invenio/bin/bibdocfile -c Preprints --set-restriction=Private``
will make all the files attached to records which are in the collection Preprint restricted. 

This procedure is recommended if you would like to give several records the same restriction status. Contact your system administrator to do this for you.



