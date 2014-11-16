.. _http-api:

HTTP API
========

Bytengine HTTP API allows you to interact with the server using your favorite
HTTP client library or application.

Quick reference
---------------

+--------------------------------------+-----------+-----------------------------+
| URL                                  | HTTP Verb | Functionality               |
+======================================+===========+=============================+
| `/`                                  | GET       | :ref:`http-api-welcome`     |
+--------------------------------------+-----------+-----------------------------+
| `/bfs/token`                         | POST      | :ref:`http-api-auth`        |
+--------------------------------------+-----------+-----------------------------+
| `/bfs/query`                         | POST      | Send a BQL request          |
+--------------------------------------+-----------+-----------------------------+
| `/bfs/uploadticket`                  | POST      | Get a file upload ticket    |
+--------------------------------------+-----------+-----------------------------+
| `/bfs/writebytes/:ticket`            | POST      | Upload file                 |
+--------------------------------------+-----------+-----------------------------+
| `/bfs/readbytes`                     | POST      | Download file               |
+--------------------------------------+-----------+-----------------------------+
| `/bfs/direct/:layer/:database/*path` | GET       | Content static serve        |
+--------------------------------------+-----------+-----------------------------+

.. _http-api-welcome:

Welcome message
---------------

Returns a welcome message from Bytengine. This url is usefull for checking if 
you're connected to the server when writing clients in your prefered language.

**Example**::

    curl -X GET http://localhost:8500/

**Return Value**:

.. code-block:: javascript

    {
        "bytengine": "Welcome",
        "version": "0.2.0"
    }

.. _http-api-auth:

Get an authentication token
---------------------------

Gets an authentication token from the server that must be included in POST requests
to interact with content.

**Example**::

    curl -X POST \
        -d 'username=admin&password=password' \
        http://localhost:8500/bfs/token

**Return Value**:

.. code-block:: javascript

    {
        "data": [token as a string],
        "status": "ok"
    }