*************
Fizzy Bignami
*************

In Italian a *bignami* is a little book with only formulas. In old days when no
smart* nor electronic device are common, students use *bignami* like quick and
fast method to remember.

This repository has the intent to be used like a *bignami* for `Fizzy`_.

.. contents::
    :local:
    :depth: 1
    :backlinks: none

====
Init
====

In spite of `Fizzy`_ README.md is **really** hassle free, some init commands follow.

.. code-block:: bash

  $ curl -sL https://raw.githubusercontent.com/alem0lars/fizzy/master/build/fizzy | \
  sudo tee /usr/local/bin/fizzy > /dev/null && \
  sudo chmod +x /usr/local/bin/fizzy

Prepare fizzy environment:

.. code-block:: bash

  $ mkdir ~/.fizzy
  $ export FIZZY_DIR=~/.fizzy

Inside ``~/.fizzy`` there will be two directories:

  1. ``cfg``, where will be all configs repositories (*templates*)
  2. ``inst``, where will be parsed and installed configs files

========================================
Basic commands.. use existing repository
========================================

Synchronize configs ``jak3/configs-awesomewm`` to fizzy environment using name
``awesomewm``:

.. code-block:: bash

  $ fizzy cfg s -C awesomewm -U jak3/configs-awesomewm

Instance (*install*) synchronized configs ``awesomewm`` to fizzy environment using name
``awesomewm``:

.. code-block:: bash

  $ fizzy qi -C awesomewm -I awesomewm -V jake-yoroi-linux

**DONE**. Never so easy.

===============================================
Make your own configs repository.. EASY configs
===============================================

Add a ``meta.yml`` file that dictate how and where make *link* (**ln**) from
fizzy ``inst`` directory to the location where RC files should live.

.. code-block:: yaml

   elems:

  - src: elems/(vimperatorrc)$
    dst: ~/.<1>
    only:
      features:
        - vimperator

  - src: elems/vimperator/(.+)$
    dst: ~/.vimperator/<1>
    only:
      features:
				- vimperator_dir

  # vim: set filetype=eruby.yaml :

Create a directory ``vars`` and a directory ``elems``.
Inside ``vars`` setting and hierarchies of them could be made as follow:

1. Generic parent ``generic.yml``:

.. code-block:: yaml

features:
  - vimperator
  - vimperator_dir

**NB**: If meta has *only features* they must be declared here.

2. Specific children (incarnation)

Child one ``jake-slackware.yml``:
.. code-block:: yaml

	# => inherits: generic <= #

	features:
	  - slackware
	  - irssi

Child two ``alem0lars-gentoo``:

.. code-block:: yaml

  # => inherits: generic <= #

  features:
    - gentoo
    - weechat

Inside ``elems`` copy your *rc* files like::

	elems
	├── vimperator
	│   ├── colors
	│   │   ├── jake.vimp
	│   │   ├── zenburn-jake.vimp
	│   │   └── zenburn.vimp
	│   └── plugin
	│       └── noscript.js
	└── vimperatorrc.tt

If you use ``vars`` rename the file with extension ``.tt`` (config template).
Using a template file you could do something like:

.. code-block:: ruby

  ...

  <% if has_feature? :pinboard %>
  map <silent> <leader>m :tabopen https://pinboard.in/u:jak3<CR>
  <% end %>

  ...

The repository is ready to use, steps to follow are already mentioned in section
above.

===============================================
Make your own configs repository.. HARD configs
===============================================

TODO

.. _Fizzy: https://github.com/alem0lars/fizzy
