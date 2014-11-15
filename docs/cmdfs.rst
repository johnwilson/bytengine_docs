.. _cmd-fs:

File System Commands
====================

File system commands enable the creation and querying of content. All commands 
commands must be preceeded by the name of the database with a '@' prefix. File
and Directory names cannot include spaces.

database.newdir
---------------

**database.newdir** creates a directory at the given path. Paths are unix/linux 
style paths (i.e. with forward slash separator) and the last element in the path
will be the name of the directory. The **root directory ('/')** is created by 
default and cannot be modified.

**Return Value**:

.. code-block:: javascript

    {
        "status": "ok",
        "data": true
    }

**Example**::

    @db1.newdir /var
    @db1.newdir /var/log

database.newfile
----------------

**database.newfile** creates a file and writes the data to the JSON layer.
Similarily to directories the file will be created at the given path.
Paths are unix/linux style paths (i.e. with forward slash separator) and the
last element in the path will be the name of the file. The data must be a valid 
JSON object.

**Return Value**:

.. code-block:: javascript

    {
        "status": "ok",
        "data": true
    }

**Example**::

    @db1.newfile /var/log/file1.log {"events": []}
    @db1.newfile /var/log/file2.log {}

database.readfile
-----------------

**database.readfile** returns the JSON layer of a file. An array of fields can be
added to limit the returned data.

**Return Value**:

.. code-block:: javascript

    {
        "status": "ok",
        "data": {...}
    }

**Example**::

    @db1.readfile /var/logs/file1.log
    @db1.readfile /var/logs/file1.log ["field1", "field1.field1_1"]

database.modfile
----------------

**database.modfile** overwrites the JSON layer of a file.

**Return Value**:

.. code-block:: javascript

    {
        "status": "ok",
        "data": true
    }

**Example**::

    @db1.modfile /var/logs/file1.log {"field1":{"field1_1": "value"}}

database.deletebytes
--------------------

**database.deletebytes** deletes the Bytes layer content of a file.

**Return Value**:

.. code-block:: javascript

    {
        "status": "ok",
        "data": true
    }

**Example**::

    @db1.deletebytes /var/logs/file1.log

database.listdir
----------------

**database.listdir** lists the contents of a directory. Content is seperated into
directories (dirs), files (files) and files with non-empty 'bytes layer' (bfiles).
The 'regex' option filters the return values.

**Options**::

    --regex: regular expression string

**Return Value**:

.. code-block:: javascript

    {
        "status": "ok",
        "data": [
            "dirs": [],
            "files": [],
            "bfiles": []
        ]
    }

**Example**::

    @db1.listdir / --regex="^v"
    @db1.listdir /var/log/

database.rename
---------------

**database.rename** renames a file or directory. The root directory '/' cannot be
renamed.

**Return Value**:

.. code-block:: javascript

    {
        "status": "ok",
        "data": true
    }

**Example**::

    @db1.rename /var/log "logs"
    @db1.rename /var/logs/file1.log "filelog.1"

database.move
-------------

**database.move** moves a file or directory to a new directory.

**Return Value**:

.. code-block:: javascript

    {
        "status": "ok",
        "data": true
    }

**Example**::

    @db1.move /var/logs/filelog.1 /var

database.copy
-------------

**database.copy** makes a copy of a file or directory. The last element in the new
path will be the name of the copied file/directory.

**Return Value**:

.. code-block:: javascript

    {
        "status": "ok",
        "data": true
    }

**Example**::

    @db1.copy /var/logs /var/file_logs

database.delete
---------------

**database.delete** deletes a file or directory. In the case of a directory it
performs a recursive delete.

**Return Value**:

.. code-block:: javascript

    {
        "status": "ok",
        "data": true
    }

**Example**::

    @db1.delete /var/file_logs

database.info
-------------

**database.info** returns metadata for files/directories such as creation date,
parent directory, type etc...

**Return Value**:

.. code-block:: javascript

    {
        "status": "ok",
        "data": {
            "created": "2014:10:23-17:42:46.5623",
            "type": "file",
            ...
        }
    }

**Example**::

    @db1.info /
    @db1.info /var/logs/filelog.1

.. _cmd-fs-makepublic:

database.makepublic
-------------------

**database.makepublic** makes a file publicly available which means it can be
accessed directly without authentication. View :ref:`direct-access` for further details. All
files are private by default.

**Return Value**:

.. code-block:: javascript

    {
        "status": "ok",
        "data": true
    }

**Example**::

    @db1.makepublic /var/logs/file1.log

database.makeprivate
--------------------

**database.makeprivate** makes a file private.

**Return Value**:

.. code-block:: javascript

    {
        "status": "ok",
        "data": true
    }

**Example**::

    @db1.makeprivate /var/logs/file1.log

database.counter
----------------

**database.counter** creates a **'counter'** or global integer value for the database
which can be incremented **'incr'**, decremented **'decr'** or reset **'reset'**.
This command can be used to create primary keys for content.
'database.counter list' returns all counters and their values in the database.

**Return Value**:

.. code-block:: javascript
    
    // database.counter [name] incr [value]
    {
        "status": "ok",
        "data": [incremented integer value]
    }

    // database.counter [name] decr [value]
    {
        "status": "ok",
        "data": [decremented integer value]
    }

    // database.counter [name] reset [value]
    {
        "status": "ok",
        "data": [incremented integer value]
    }

    // database.counter list
    {
        "status": "ok",
        "data": [
            {"name":"...", "value": [current integer value]}
        ]
    }

**Example**::

    @db1.counter "logs" incr 1
    @db1.counter "logs" incr 5
    @db1.counter "logs" decr 2
    @db1.counter "logs" reset 0

    @db1.counter list
    @db1.counter list --regex="^l"