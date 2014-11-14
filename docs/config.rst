.. _configuration:

Configuring Bytengine
=====================

Bytengine configuration file is in JSON format and can be found at 
`/bytengine/bytengine/config.json <https://github.com/johnwilson/bytengine/blob/master/bytengine/config.json>`_.

The authentication (auth) and bytengine file system (bfs) plugins use 
`Mongodb <http://www.mongodb.org/>`_. as their database and the 
`mgo driver <http://godoc.org/gopkg.in/mgo.v2#DialInfo>`_.

.. code-block:: javascript

    {
        "addresses":["localhost:27017"], // mongodb server(s)
        "authdb":"", // mongodb authentication database
        "username":"", // mongodb authentication username
        "password":"", // mongodb authentication password
        "timeout":60 // mongodb client timeout
    }

The cache plugin (cache) relies on `Redis <http://redis.io/>`_. and uses 
`Beego Cache implementation <https://github.com/astaxie/beego/tree/master/cache>`_.

.. code-block:: javascript

    {
        "conn": "localhost:6379"
    }

The byte store (bst) plugin uses `Diskv <https://github.com/peterbourgon/diskv>`_. for storage.

.. code-block:: javascript

    {
        "rootdir":"/tmp/bytengine_bst", // directory to store content
        "cachesize":1 // cache size in mb
    }

Other configurations

.. code-block:: javascript

    {
        ...
        "workers": 2, // number of goroutines
        "port": 8500, // bytengine server port
        "address": "localhost", // bytengine server address
        "timeout": {
            "authtoken": 60, // authentication cache timeout in minutes
            "uploadticket": 60 // upload ticket cache timeout in minutes
        }
    }