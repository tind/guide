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

.. _manage-user-rights:

Manage User Rights
=======================

1. Introduction
-----------------------

There are three important terms regarding user rights in Invenio:

  - **User** are the physical persons having access to Invenio.
  - **Action** identifies a task a user can perform.
  - **Roles** works as an intermediate between the users and actions, allowing several users to perform several actions.



|tag-cloud for document mng-user/001|

.. |tag-cloud for document mng-user/001| image:: /_static/librarian/manage-user-rights1.png

2. Create new collection and add the collection to the tree
-----------------------------------------------------------

Users are connected to roles that cover different areas of access. I.e administrator of the photo
  collection or system librarian. Users can be active in
  different areas and of course connected to as many roles as needed.

An action . It can be defined to take any number of

arguments in order to more clearly describe what you are allowing
  connected users to do.

  For example the system librarian can be allowed to run bibindex on
  the different indexes. To allow system librarians to run the
  bibindex indexing on the field author we connect role system
  librarian with action runbibindex using the argument
  index='author'.

  Additionally, roles could have firewall-like role
  definitions. A definition is a formal description of which
  users are entitled to belong to the role. So you have two ways for
  connecting users to roles. Either linking explicitly a user with the
  role or describing the characteristics that makes users belong to
  the role.

  WebAccess is based on allowing users to perform actions. This means
  that only allowed actions are stored in the access control engine's
  database.


