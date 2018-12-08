************
Installation
************

`smoke-python` requires Python 3.5 or higher. We don't recommend usage of Python that ships with OS.
If you're just looking for a quick and easy cross-platform solution, feel free to install Python 3.x via easy to use
`Anaconda <https://www.continuum.io/downloads>`_ installer.


Afterwards, you can install `smoke-python` with `pip`:

::

    $ pip install smoke

You can also perform the installation manually using `setup.py`:

::

    $ git clone https://github.com/betgames/betgames-smoke-python/tree/smoke-python
    $ cd smoke-python
    $ make install

Upgrade
#######

::

   $ pip install -U smoke



Namespace Collision
===================

If you have used a piston stack before v0.5, please remove it before installing official version of ``python-smoke``.

::

   curl https://github.com/betgames/betgames-smoke-python/tree/smoke-python/scripts/nuke_legacy.sh | sh
