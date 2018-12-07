Transactions and Accounts
~~~~~~~~~~~~~~~~~~~~~~~~~

Commit
======

The Commit class contains helper methods for `posting, voting, transferring funds, updating witnesses` and more.
You don't have to use this class directly, all of its methods are accessible trough main ``Smoke`` class.

.. code-block:: python

   # accessing commit methods trough Smoke
   s = Smoke()
   s.commit.transfer(...)

   # is same as
   c = Commit(smoke=Smoke())
   c.transfer(..)

.. autoclass:: smoke.smoke.Commit
   :members:

--------


TransactionBuilder
==================

.. autoclass:: smoke.transactionbuilder.TransactionBuilder
   :members:

--------

Wallet
======

Wallet is a low-level utility.
It could be used to create 3rd party cli and GUI wallets on top of ``smoke-python``'s infrastructure.

.. automodule:: smoke.wallet
   :members:
