.. _cmd-fs-adv:

Advanced File System Commands
=============================

database.select
---------------

**database.select** retrieves fields from files in directories based on field values
or file metadata values specified in the **Where statement**. Additional statements
such as **Limit, Sort, Count or Distinct** can be used to further filter the query
result. Multiple field comparison can be seperated by **Or** (**And** is implied).

Field value comparison operators are:

    * equal: ``==``
    * not equal: ``!=``
    * greater than: ``>``
    * greater than or equal: ``>=``
    * less than: ``<``
    * less than or equal: ``<=``

Field inclusion/exclusion operators are:

    * inclusive of: ``in``
    * exclusive of: ``nin``

Field functions available are:

    * type of field: ``typeof([FIELD])`` (supported types are 'string', 'int')
    * existance of field: ``exists([FIELD])``
    * field regular expression: ``regex([FIELD], REGEX_OPTION)``. Valid REGEX_OPTION
      values can be found in the mongodb documentation.

Special Field values are:

    * file name: ``file_name``
    * file privacy: ``file_ispublic``

**Return Value**:

.. code-block:: javascript

    {
        "status": "ok",
        "data": [
            {
                "path": "/.../...",
                "content": {...}
            },
            ...
        ]
    }

**Example**::

    @db1.select "age" in /users /staff limit 20

    @db1.select "name" "course.room" in /students where "year">=1 "status"=="active"

    @db1.select "date" in /logs where "event"=="failure" limit 50

    @db1.select "" in /users where regex(file_name, "i") == "^j" distinct "age"

    @db1.select "" in /members count
    @db1.select "" in /members distinct "country"

    @db1.select "name" in /banned_users sort asc "date_joined"
    @db1.select "name" in /banned_users sort desc "date_joined"

    @db1.select "status" in /users where typeof("children")=="int"

database.set
------------

**database.set** sets file field values in a directory based on **Where statement**
as specified in the **database.select** command.

**Return Value**:

.. code-block:: javascript

    {
        "status": "ok",
        "data": [number of affected files]
    }

**Example**::

    @db1.set "country"="Ghana" in /users where "country"=="gh"

database.unset
--------------

**database.unset** unsets (or removes) file field values in a directory based on
**Where statement** as specified in the **database.select** command.

**Return Value**:

.. code-block:: javascript

    {
        "status": "ok",
        "data": [number of affected files]
    }

**Example**::

    @db1.unset "country" in /users where "country"=="gh"