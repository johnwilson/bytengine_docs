.. _quick-bshell:

Quick Tutorial - bshell
=======================

We are going to use `bshell <https://github.com/johnwilson/bshell/>`_.
this time round to execute the commands issued in the previous python tutorial.
bshell (Bytengine Shell) makes it much easier to test and build up scripts that
can later be used in an application.

We'll first have to install bshell from source (or download the binaries).

**Build from source (requires Go)**

This assumes you have setup $GOPATH and have added $GOPATH/bin to $PATH. We'll
also assume that you have Bytengine installed.

.. code-block:: bash
    
    go get github.com/johnwilson/bytengine/cmd/bshell
    bshell run -u=admin -p=password

**Create database**

.. code-block:: bash

    bql> server.newdb "test"; server.listdb;
    {
        "data": [
            true,
            [
                "test"
            ]
        ],
        "status": "ok"
    }

**Content creation: BQL script**

We are going to execute the following script using bshell's editor command

.. code-block:: guess

    /* ============================================
       This is a BQL comment:

       Multiple commands can be issued in a single
       script but must be separated by a ';'
       Results from the all commands will be
       returned in an array.
    =============================================== */
    
    /*---- create directories ----*/

    @test.newdir /myapp ;
    @test.newdir /myapp/users ;

    /*---- create file with valid JSON data ----*/

    @test.newfile /myapp/users/u1 {"name":"justin","age":24} ;
    @test.newfile /myapp/users/u2 {"name":"lola","age":57} ;
    @test.newfile /myapp/users/u3 {"name":"jenny","age":33} ;
    @test.newfile /myapp/users/u4 {"name":"sam","age":16} ;

    /*---- search for users ----*/

    @test.select "name" "age" in /myapp/users
    where "age" < 20 or regex("name","i") == "^j";

Open bshell editor ('vim' by default) and type/save the above script

.. code-block:: bash

    bql> \e

You should see the following response

.. code-block:: javascript

    {
        "data": [
            true,
            true,
            true,
            true,
            true,
            true,
            [
                {
                    "content": {
                        "age": 24,
                        "name": "justin"
                    },
                    "path": "/myapp/users/u1"
                },
                {
                    "content": {
                        "age": 33,
                        "name": "jenny"
                    },
                    "path": "/myapp/users/u3"
                },
                {
                    "content": {
                        "age": 16,
                        "name": "sam"
                    },
                    "path": "/myapp/users/u4"
                }
            ]
        ],
        "status": "ok"
    }

As we can see, the result for each of the commands issued is returned by the server.

The bshell example is less verbose than the python one which makes it an essential
tool when working with Bytengine.