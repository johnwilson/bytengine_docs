.. _cmd-user:

User Commands
=============

user.new
--------

**user.new** creates a new (non-root) server user.

**Return Value**:

.. code-block:: javascript

    {
        "status": "ok",
        "data": true
    }

**Example**::

    user.new "username" "password"

user.all
--------

**user.all** lists all server users (usernames).

**Options**::

    --regex: regular expression string

**Return Value**:

.. code-block:: javascript

    {
        "status": "ok",
        "data": [
            "user_1",
            ...,
            "user_n"
        ]
    }

**Example**::

    user.all
    user.all --regex="^ad"

user.about
----------

**user.about** returns information about a user (databases, status, etc...).

**Return Value**:

.. code-block:: javascript

    {
        "status": "ok",
        "data": {
            "active": true,
            "databases": [],
            "root": false,
            "username": "user1"
        }
    }

**Example**::

    user.about "username"

user.delete
-----------

**user.delete** deletes a user from the server.

**Return Value**:

.. code-block:: javascript

    {
        "status": "ok",
        "data": true
    }

**Example**::

    user.delete "username"

user.passw
----------

**user.passw** changes user's password.

**Return Value**:

.. code-block:: javascript

    {
        "status": "ok",
        "data": true
    }

**Example**::

    user.passw "username" "newpassword"

user.access
-----------

**user.access** grants/denies user access to the server.

**Return Value**:

.. code-block:: javascript

    {
        "status": "ok",
        "data": true
    }

**Example**::

    user.access "username" grant
    user.access "username" deny

user.db
-------

**user.db** grants/denies user access to a database on the server.

**Return Value**:

.. code-block:: javascript

    {
        "status": "ok",
        "data": true
    }

**Example**::

    user.db "username" "database" grant
    user.db "username" "database" deny

user.whoami
-----------

**user.whoami** show current user's information.

**Return Value**:

.. code-block:: javascript

    {
        "status": "ok",
        "data": {
            "databases": [],
            "isroot": false,
            "username": "user1"
        }
    }

**Example**::

    user.whoami