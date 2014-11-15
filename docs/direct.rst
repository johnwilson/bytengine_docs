.. _direct-access:

Direct Content Access
=====================

Bytengine allows you to server your content directly (as static content) via Http GET.
You have to first make the bytengine file **public** by issuing a :ref:`cmd-fs-makepublic`
command which will make the content available at the following url::

    http://[your bytengine server address]/bfs/direct/[layer]/[database]/[path]

Where:

    * **[layer]** is the bytengine file layer you want to retrieve (JSON or Bytes)
    * **[database]** is the database name
    * **[path]** is the bytengine file path

The response header will either be ``application/json`` if the layer is ``json``
and ``application/octet-stream`` if the layer is ``bytes``

**Example**::

    http://localhost:8500/bfs/direct/json/db1/users/active/file1

    http://localhost:8500/bfs/direct/bytes/db1/users/active/file1_profile_picture