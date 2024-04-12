.. This Source Code Form is subject to the terms of the Mozilla Public
.. License, v. 2.0. If a copy of the MPL was not distributed with this
.. file, You can obtain one at http://mozilla.org/MPL/2.0/.
=======
find404
=======

``find404`` is a small CLI tool for finding a 404 response from an HTTP server.

Rationale
=========

Finding a username that is available for a web site is not easy.
Sometimes web sites do not assist you to find an alternative.
Sometimes they suggest a username with numbers appended.
But there is no guarantee that the number is the lowest possible.
This CLI tool is intended to help you find that lowest number under certain conditions.
Some web sites make the users' profiles addressable via a URL.
And return a response with HTTP status code 404 if a requested user does not exist.
Starting from a provided URL this tool will make HTTP requests,
appending an incremented number to the given URL,
until it receives a 404 response (or a counter is exhausted).

But why create this tool?
Can't the same outcome be achieved through existing tools and/or shell scripting?
Most probably "yes", but...

The secondary objective of this project is to practise
GitHub actions and
the modern approaches to distributing a Python package.

Example
=======

.. code::

    $ find404 https://example.net/profile/martin
    200  https://example.net/profile/martin
    200  https://example.net/profile/martin0
    200  https://example.net/profile/martin1
    200  https://example.net/profile/martin2
    404  https://example.net/profile/martin4

Usage
=====

This tool is **not** created with malicious intent.
Thus, it limits the total number of requests performed,
as well as it intentionally waits between each of them.

Roadmap
=======

The following are intentions about future changes:

The behaviour to be controlled via options:

``--count, -c``
    How many requests to be attempted before giving up.
    Defaults to ``10``.

``--interval, -i``
    How many seconds to wait between requests.
    Defaults to ``5`` (seconds).

``--start-at``
    What should be the first appended number.
    Defaults to ``0``.

.. code::

    $ find404 -c 3 -i 10 --start-at 20 https://example.net/profile/martin
    200  https://example.net/profile/martin
    200  https://example.net/profile/martin20
    200  https://example.net/profile/martin21
