# The purpose of this docker file is to provide a shell with
# smoke-python pre-installed for interactive testing purposes.
#
# Usage:
# docker build -t smokepy .
# docker run -it smokepy

FROM python:3.5.3
MAINTAINER betgames <_@betgames.me>

# set default password for BIP38 encrypted wallet
ENV UNLOCK test123

RUN pip install ipython
RUN pip install git+git://github.com/betgames/betgames-smoke-python/tree/smoke-python

CMD "ipython"