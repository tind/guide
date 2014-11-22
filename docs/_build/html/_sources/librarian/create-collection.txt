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

.. _create-collection:

Create Collections
=======================

1. Overview
-----------

WebSearch Admin interface will help you to configure the search
collections that the end-users see. The WebSearch Admin functionality
can be basically separated into several parts: (i) how to organize
collections into `collection tree <#2>`__; (ii) how to define and edit
`collection parameters <#3>`__; (iii) how to update collection cache via
the `webcoll daemon <#4>`__; and (iv) how to influence the search engine
behaviour and set various `search engine parameters <#5>`__. 

The first two issues will be described in the rest of this guide. See WebSearch Admin Guide for the last two issues.

2. Edit Collection Tree
-----------------------

Metadata corpus in Invenio is organized into collections. The
collections are organized in a tree. The collection tree is what the
end-users see when they start to navigate at `Atlantis Institute of
Fictive Science <http://localhost:4000>`__. The collection tree is
similar to what other sites call Web Directories that organize Web into
topical categories, such as `Google
Directory <http://www.google.com/dirhp>`__.

Note that Invenio permits every collection in the tree to have either
"regular" or "virtual" sons. In other words, every node in the
collection tree may see either regular or virtual branches growing out
of it. This permits to create a tree with very complex, multi-level,
nested structures of regular and virtual branches, if needed, with the
aim to ease navigation to end-users from one branch to another. The
difference between a regular and a virtual branch will be explained in
detail further below in the `section 2.2 <#2.2>`__.

2.1 Add new collection
~~~~~~~~~~~~~~~~~~~~~~

To add a new collection, enter its default name in the default language
of the installation and click on the ADD button to add it. There are two
important actions that you have to perform after adding a collection:

-  You have to define the set of records that belong to this collection.
   This is done by defining a search engine query that would return all
   records belonging to this collection. See hints on `modify collection
   query <#3.1>`__ below.
-  In order for the collection to appear in the collection navigation
   tree, you will have to attach it to some existing collection in the
   tree. See hints on `add collection to tree <#2.2>`__ below.

After you edit these two things, the collection is fully usable for the
search interface. It will appear in the search interface after the next
run of the `WebColl Daemon <#4>`__.

However, you will probably want to customize further things, like define
collection name translation in various languages, define collection web
page portalboxes, define search options, etc, as explained in this guide
under the section `Edit Collection Parameters <#3>`__.

2.2 Add collection to tree
~~~~~~~~~~~~~~~~~~~~~~~~~~

To attach a collection to the tree, choose first which collection do you
want to attach, then choose the father collection to attach to, and then
choose the fathership relation type between them (regular, virtual).

The difference between the regular and the virtual relationship goes as
follows:

-  **regular relationship**: If collection A is composed of B and C, in
   a way that every document belonging to A is either B or C, then this
   schema corresponds to the regular type of relationship. For example,
   let A equals to "Multimedia" and B and C to "Photos" and "Videos",
   respectively. The latter collections would then be declared as
   regular sons of "Multimedia" and they would appear in the
   left-hand-side regular navigation tree entitled "Narrow by
   Collection" in the collection tree.
-  **virtual relationship**: In addition to the regular decomposition of
   "Multimedia" into "Photos" and "Videos", it may be advantageous to
   present a different, orthogonal point of view on "Multimedia", based
   not on the document type as seen above, but rather on the document
   creator information. Let us consider that some (large) part of the
   multimedia material was created by the "University Multimedia
   Service" and some (small) part by an external TV company such as BBC.
   It may be advantageous to advertize this point of view to the end
   users too, so they they would be able to easily navigate down to the
   kind of multimedia material they are looking for. We can create two
   more collections named "University Multimedia Service" and "BBC
   Pictures and Videos" and declare them as virtual sons of the
   "Multimedia" collection. These collections would then appear in the
   right-hand-side virtual navigation tree entitled "Focus on" in the
   collection tree.

The example presented above would then give us the following picture:

    ::

                M u l t i m e d i a

                Narrow by Collection:        Focus on:
                --------------------         ---------
                [ ] Photos                   University Multimedia Service
                [ ] Videos                   BBC Pictures and Videos

It is important to note that if a collection A is composed of B and C as
its regular sons, and offers X and Y as its virtual sons, then every
document belonging to A must also belong to either B or C. This
requirement does not apply for X and Y, because X and Y offer only a
"focus-on" orthogonal view on a (possibly small) part of the document
corpus of A. If end-users search the collection A, then they are
actually searching inside B and C, not X and Y. If they want to search
inside X or Y, they have to click upon X or Y first. One can consider
virtual branches as a sort of non-essential searching aid to the
end-user that is activated only when users are interested in a
particular "focus-on" relationship, provided that this "virtual" point
of view on A interests her.

2.3 Modify existing tree
~~~~~~~~~~~~~~~~~~~~~~~~

To modify existing tree by WebSearch Admin Interface, click on icons
displayed next to collections. The meaning of icons is as follows:

+--------------------------------------+--------------------------------------+
| |A   |                               | |B |            |C  |                |
| Remove chosen collection with its    | Move chosen collection up or down    |
| subcollections from the collection   | among its brothers and sisters, i.e. |
| tree, but do not delete the          | change the order of collections      |
| collection itself. (For full         | inside the same level of the tree.   |
| deletion of a collection, see        |                                      |
| `section 3.4 <#3.4>`__.)             |                                      |
+--------------------------------------+--------------------------------------+

3. Edit Collection Parameters
-----------------------------

To finalize setting up of a collection, you could and should edit many
parameters, such as define list of records belonging to a collection,
define search fields, define search interface page portalboxes, etc. In
this section we will subsequently describe all the various possibilities
as they are presented in the `Edit
Collection </admin/websearch/websearchadmin.py/editcollection?colID=1>`__
pages of the WebSearch Admin Interface.

3.1 Modify collection query
~~~~~~~~~~~~~~~~~~~~~~~~~~~

The *collection query* defines which documents belong to the given
collection. It is equal to the search term that retrieves all documents
belonging to the given collection, exactly as you would have typed it
into the search interface. For example, to define a collection of all
papers written by Ellis, you could set up your collection query to be
``author:Ellis``.

Usually, the collection query is chosen on the basis of the collection
identifier that we store in MARC tag 980. This tag is indexed in a
logical field called ``collection`` so that a collection of Theses could
be defined via ``collection:THESIS``, supposing that every thesis
metadata record has got the text ``THESIS`` in MARC tag 980. (Nitpick:
we use the term \`collection' in two contexts here: once as a collection
of metadata documents, but also and as a logical field name. We should
have probably called the latter ``collectionidentifier`` or somesuch
instead, but we hope the difference is clear from... the context.)

If a collection does not have any collection query defined, then its
content is defined by means of the content of its descendants
(subcollections). This is the case for composed collections. For
example, the composed collection *Articles & Preprints* (no query
defined) will be defined as a father of *Articles* (query:
``collection:ARTICLE``) and *Preprints* (query:
``collection:PREPRINT``). In this case the collection query for
*Articles & Preprints* can stay empty.

Note that you should avoid defining non-empty collection query in cases
the collection has descendants, since it will prevail and the
descendants may not be taken into account. In the same way, if a
collection doesn't have any query nor any descendants defined, then its
contents will be empty.

To remove the collection query, set the parameter empty.

3.2 Modify translations
~~~~~~~~~~~~~~~~~~~~~~~

You may define translations of collection names into the languages of
your Invenio installation. Moreover, a collection name may be different
in different contexts (e.g. long name, short name, etc), so that prior
to modifying translations you will be asked to select which name type
you want to change.

The translations aren't mandatory to define. If a translation does not
exist in a language chosen by the end user, the end user will be shown
the collection name in the default language of this installation.

Note also that the list of available languages depends on the
compile-time configuration (see the general ``invenio.conf`` file).

3.3 Delete collection
~~~~~~~~~~~~~~~~~~~~~

The collection to be deleted must be first removed from the collection
tree. Any metametadata associated with the collection (such as
association to portalboxes, association to records belonging to this
collection, etc) will be lost, but the metadata itself will be preserved
(such as portalboxes themselves, records themselves, etc). In total,
association to records, output formats, translations, search options,
sort options, search fields, ranking method, and access restriction will
be lost. Use with care!

It may be a good idea only to remove the collection from the end users
interface, but to keep it "hidden" in a corner they don't see and that
they can't search when they search from Home. To achieve this, do not
delete the collection but simply remove it from the collection tree so
that it won't be attached to any father collection. In this case the
search interface page for this collection will stay updated, but won't
be neither shown in the tree nor searchable from Home page. It will only
be accessible via bookmarked URL, for example.

3.4 Modify search fields
~~~~~~~~~~~~~~~~~~~~~~~~

The *search field* is a logical field (such as author, title, etc) that
will be proposed to the end users in Simple and Advanced Search
interface pages. If you do not set any search fields for a collection,
then a default list (author, title, year, etc) will be shown.

Note that if you want to add a new logical field or modify existing
physical MARC tags for a logical field, you have to use the `BibIndex
Admin </admin/bibindex/bibindexadmin.py>`__
interface.

3.5 Modify search options
~~~~~~~~~~~~~~~~~~~~~~~~~

The *search option* is like `search field <#3.6>`__ in a way that it
permits the end user to narrow down his search to some logical field
such as "subject", but unlike with the search field the user is not
required to type his query in a free text form; rather, the search
interface proposes to the end user several interesting predefined values
prepared by the administrators that the end user may choose from. For
example, an "author search" concept is a good example of search field
usage, since there is plenty of author names to be matched, so that the
end users would usually type the name they wish to find in free text
form; while a "subject search" concept is a good example for search
option usage, since usually there is a limited number of subjects in the
system given by local subject classification scheme, that the end users
do not necessarily know about and that they are free to choose from a
list. As a rule of thumb, the search field concept denotes the case of
unlimited number possibilites of distinct values to be matched in a
given field (e.g. author, title, keyword); while the search option
concept denotes the case of only a handful or so distinct values to be
matched in a given field (e.g. subject, division, year).

Search options are shown in the "Advanced Search" interfaces only, while
search fields are shown both in "Simple Search" and "Advanced Search"
interface. (Although if you want to add a search option to the "Simple
Search" interface, you can achieve it by creating appropriate HTML code
in a `portalbox <#3.5>`__.) The search options order, as well as the
order of search option values, may be defined by means of 'move' arrows
in the WebSearch Admin interface.

To add a new search option, a field name must first be chosen (for
example "subject") and then a list of possible field values must be
entered (for example "Mathematics", "Physics", "Chemistry", "Biology",
etc). Note that if you want to add a new logical field or modify
existing physical MARC tags for a logical field, you have to use the
`BibIndex
Admin </admin/bibindex/bibindexadmin.py>`__
interface.

