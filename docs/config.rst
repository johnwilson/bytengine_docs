.. _configuration:

Configuring Bytengine
=====================

Bytengine configuration file is in JSON format and can be found at 
`/bytengine/bytengine/config.json <https://github.com/johnwilson/bytengine/blob/master/cmd/bytengine/config.json>`_.

The authentication (authentication) and bytengine file system (filesystem) plugins use 
`Mongodb <http://www.mongodb.org/>`_. as their database and the 
`mgo driver <http://godoc.org/gopkg.in/mgo.v2#DialInfo>`_.

.. code-block:: javascript

    {
        "plugin": "mongodb",                // authentication plugin name
        "addresses":["localhost:27017"],    // mongodb server(s)
        "authdb":"",                        // mongodb authentication database
        "username":"",                      // mongodb authentication username
        "password":"",                      // mongodb authentication password
        "timeout":60                        // mongodb client timeout
    }

The state store plugin (statestore), for tokens and cache, relies on `Redis <http://redis.io/>`_.

.. code-block:: javascript

    {
        "plugin": "redis",              // state store plugin name
        "address": "localhost:6379",    // redis server address
        "password": "",                 // redis server password
        "timeout": 60,                  // redis client timeout
        "database": 1                   // database index
    }

The byte store (bytestore) plugin uses `Diskv <https://github.com/peterbourgon/diskv>`_. for storage.

.. code-block:: javascript

    {
        "rootdir":"/tmp/bytengine_bst", // directory to store content
        "cachesize":1                   // cache size in mb
    }

Other configurations

.. code-block:: javascript

    {
        ...
        "workers": 2,           // number of goroutines
        "port": 8500,           // bytengine server port
        "address": "localhost", // bytengine server address
        "timeout": {
            "authtoken": 60,    // authentication cache timeout in minutes
            "uploadticket": 60  // upload ticket cache timeout in minutes
        }
    }