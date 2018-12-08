Smoke - Your Starting Point
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Quick Start
-----------
You can start using the library with just a few lines of code, as seen in this quick example:

.. code-block:: python

   # first, we initialize Smoke class
   from smoke import Smoke
   s = Smoke()

Importing your Smoke Account
============================
`smoke-python` comes with a BIP38 encrypted wallet, which holds your private keys.



Alternatively, you can also pass required WIF's to ``Smoke()`` initializer.

::

    from smoke import Smoke
    s = Smoke(keys=['<private_posting_key>', '<private_active_key>'])

Using the encrypted wallet is however a recommended way.

Please check :doc:`cli` to learn how to set up the wallet.

Interfacing with smoked
=======================
``Smoke()`` inherits API methods from ``Smoked``, which can be called like so:

.. code-block:: python

   s = Smoke()

   s.get_account('stoner')
   s.get_block(8888888)
   s.get_content('author', 'permlink')
   s.broadcast_transaction(...)
   # and many more

You can see the list of available methods by calling ``help(Smoke)``.
If a method is not available trough the Python API, we can call it manually using ``s.exec()``:

.. code-block:: python

   s = Smoke()

   # this call
   s.get_followers('betgames', 'abit', 'blog', 10)

   # is same as
   s.exec('get_followers',
          'betgames', 'abit', 'blog', 10,
           api='follow_api')

Commit and Wallet
=================
``Smoke()`` comes equipped with ``Commit`` and ``Wallet``, accessible via dot-notation.

.. code-block:: python

   s = Smoke()

   # accessing Commit methods
   s.commit.transfer(...)

   # accessing Wallet methods
   s.wallet.get_active_key_for_account(...)

Please check :doc:`core` documentation to learn more.


Smoke
-----

As displayed in the `Quick Start` above, ``Smoke`` is the main class of this library. It acts as a gateway to other components, such as
``Smoked``, ``Commit``, ``Wallet`` and ``HttpClient``.

Any arguments passed to ``Smoke`` as ``kwargs`` will naturally flow to sub-components. For example, if we initialize
Smoke with ``smoke = Smoke(no_broadcast=True)``, the ``Commit`` instance is configured to not broadcast any transactions.
This is very useful for testing.

.. autoclass:: smoke.smoke.Smoke
   :members:


Smoked API
----------

Smoked contains API generating utilities. ``Smoked``'s methods will be automatically available to ``Smoke()`` classes.
See :doc:`smoke`.

.. _smoked-reference:

.. automodule:: smoke.smoked
   :members:


Setting Custom Nodes
--------------------

There are 3 ways in which you can set custom ``smoked`` nodes to use with ``smoke-python``.

**1. Global, permanent override:**
You can use ``smokepy set nodes`` command to set one or more node URLs. The nodes need to be separated with comma (,)
and shall contain no whitespaces.

    ::

        ~ % smokepy config
        +---------------------+--------+
        | Key                 | Value    |
        +---------------------+--------+
        | default_vote_weight | 100      |
        | default_account     | betgames |
        +---------------------+--------+
        ~ % smokepy set nodes https://gtg.smoke.house:8090/
        ~ % smokepy config
        +---------------------+-------------------------------+
        | Key                 | Value                          |
        +---------------------+-------------------------------+
        | default_account     | betgames                       |
        | default_vote_weight | 100                            |
        | nodes               | https://gtg.smoke.house:8090/  |
        +---------------------+-------------------------------+
        ~ % smokepy set nodes https://gtg.smoke.house:8090/,https://api.smoke.io
        ~ % smokepy config
        +---------------------+----------------------------------------------------------+
        | Key                 | Value                                                    |
        +---------------------+----------------------------------------------------------+
        | nodes               | https://gtg.smoke.house:8090/,https://api.smoke.io       |
        | default_vote_weight | 100                                                      |
        | default_account     | betgames                                                 |
        +---------------------+----------------------------------------------------------+
        ~ %


To reset this config run ``smokepy set nodes ''``.

**2. For Current Python Process:**
You can override default `Smoked` instance for current Python process, by overriding the `instance` singleton.
You should execute the following code when your program starts, and from there on out, all classes (Blockchain, Account,
Post, etc) will use this as their default instance.

    ::

        from smoke.smoked import Smoked
        from smoke.instance import set_shared_smoked_instance

        smoked_nodes = [
            'https://gtg.smoke.house:8090',
            'https://api.smoke.io',
        ]
        set_shared_smoked_instance(Smoked(nodes=smoked_nodes))


**3. For Specific Class Instance:**
Every class that depends on smoked comes with a ``smoked_instance`` argument.
You can override said smoked instance, for any class you're initializing (and its children).

This is useful when you want to contain a modified ``smoked`` instance to an explicit piece of code (ie. for testing).

    ::

        from smoke.smoked import Smoked
        from smoke.account import Account
        from smoke.Blockchain import Blockchain

        smoked_nodes = [
            'https://gtg.smoke.house:8090',
            'https://api.smoke.io',
        ]
        custom_instance = Smoked(nodes=smoked_nodes)

        account = Account('furion', smoked_instance=custom_instance)
        blockchain = Blockchain('head', smoked_instance=custom_instance)
