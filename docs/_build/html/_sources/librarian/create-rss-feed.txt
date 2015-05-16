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

.. _create-rss-feed:

Create RSS feed
===============

Two procedures for creating a RSS feed is described in this chapter; based on the search 
query itself, or the content added to your personal or public baskets.


1. Create a RSS feed for the content in your personal or public basket
----------------------------------------------------------------------

Please check out :ref:`manage-baskets` for how to add content to a basket.

For both personal and public basket, a new RSS feed is created by selecting "RSS" in the 
menu for export formats. 

|tag-cloud for document cre-rss/001|

.. |tag-cloud for document cre-rss/001| image:: /_static/librarian/create-rss-feed1.png

Dependent of your browser either a text based site, or a html friendly site is displayed.


**Firefox**

|tag-cloud for document cre-rss/002|

.. |tag-cloud for document cre-rss/002| image:: /_static/librarian/create-rss-feed2.png

**Chrome**

|tag-cloud for document cre-rss/003|

.. |tag-cloud for document cre-rss/003| image:: /_static/librarian/create-rss-feed3.png

Copy the URL and past it into your favorite RSS reader.

.. note::

    A RSS feed created from a private basket is only updated while the user is logged in. 
    A public basket is necessary if the RSS feed will be shared. A public basket
    is also recommended if the user uses an external application (not a plug-in 
    to the browser) which does not have the functionality to authenticate the user.

.. note::

    The RSS feed in Invenio contains the following information as default: title, link, 
    description, author, publication date, publisher and creation date/ date issued.
    Which information which is displayed in the reader is dependent of the available 
    metadata and the reader itself.  

2. Create a RSS feed from the search query
------------------------------------------


Invenio support RSS feeds based on the search query. Only items that matches the query
will update the RSS reader. This gives the users the opportunity to only subscribe for 
content of interest by creating advances queries, example 
``author:"ILO" AND subject:"child labour"`` .

A button to subscribe for a RSS feed is found at the bottom of every search results 
(brief view). 

|tag-cloud for document cre-rss/004|

.. |tag-cloud for document cre-rss/004| image:: /_static/librarian/create-rss-feed4.png





.. note::

    Invenio support empty queries, which will display all items in the database. A limit
    of 25 items have been set as default for the RSS feed. Therefore, subscribing for 
    a RSS feed based on a empty query will only display the last 25 items in the 
    database. Such a subscription will notify the user of all new items in the database.
    

