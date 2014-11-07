.. _cmd-server:

Server Commands
===============

Server commands can only be run by a user who has **root** access.

server.init
-----------

**server.init** removes all file system content and returns the names of databases
deleted from the server.

**Return Value**:

.. code-block:: javascript

    {
        "status": "ok",
        "data": [
            db_1,
            db_2,
            ...,
            db_n
        ]
    }

**Example**::

    server.init

server.newdb
-------------

**server.newdb** creates a new database.

**Return Value**:

.. code-block:: javascript

    {
        "status": "ok",
        "data": true
    }

**Example**::

    server.newdb "db1"

server.listdb
-------------

**server.listdb** list all databases on the server.

**Options**::

    --regex: regular expression string

**Return Value**:

.. code-block:: javascript

    {
        "status": "ok",
        "data": [
            db_1,
            db_2,
            ...,
            db_n
        ]
    }

**Example**::

    server.listdb
    server.listdb --regex="^j"

server.dropdb
-------------

**server.dropdb** deletes a database.

**Return Value**:

.. code-block:: javascript

    {
        "status": "ok",
        "data": true
    }

**Example**::

    server.dropdb "db1"
