..  Copyright (C) 2014 TIND Technologies AS.

.. _use-of-marc:

MARC Fields
=====================


1. Overview
-----------

Invenio 1.x are using marc as the bibliographic layer.

2. Default marc field used by TIND
-----------

Use of 001, 005, 020, 022, 084



=====  =====  =========
MARC   Articl Preprints 
=====  =====  =========
001    x	  x
020	   x	  x
022	   x	  x
084	   x	  x
=====  =====  =========

asf

=====  =====  =======
A      B      A and B
=====  =====  =======
False  False  False
True   False  False
False  True   False
True   True   True
=====  =====  =======