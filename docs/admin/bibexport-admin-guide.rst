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

.. _bibexport-admin-guide:

BibExport Admin Guide
========================

Introduction
------------
BibExport is a module to easily export data. One of the main tools is to export xml files. 

Configurate and run commands
----------------------------

Below is a commented example configuration to show how one would typically configure the parameters, run the command and retriew the files. 
The details of how this works were explained in the paragraphs above.

::

    # Define what you would like to export in ``/opt/invenio/etc/bibexport/marcxml.cfg``.
    # Default setting are given below. This job would have exported all records from the Book collection into one xml.-file and all articles with the author "Polyakov, A M" into another.  
    [export_job]
    export_method = marcxml
    [export_criterias]
    books = 980__a:BOOK
    polyakov_articles = 980__a:ARTICLE and author:"Polyakov, A M"
    


