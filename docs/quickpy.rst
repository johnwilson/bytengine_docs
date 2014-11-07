.. _quick-py:

Quick Tutorial - Python
=======================

This guide will give you a quick overview of a few Bytengine api calls.

This guide assumes that you be running Bytengine locally on its default ports.
The python code uses the excellent `requests module <http://docs.python-requests.org/en/latest/>`_.

**Create admin user and start Bytengine server**

.. code-block:: bash
    
    cd $YOUR_BYTENGINE_SERVER_EXECUTABLE_DIR
    ./bytengine createadmin -u=admin -p=password
    ./bytengine run

**Connect to Bytengine**

.. code-block:: python

    >>> import requests
    >>> url = "http://localhost:8500/"
    >>> r = requests.get(url)
    >>> print r.text
    {"bytengine":"Welcome","version":"0.2.0"}

**Login and create database**

.. code-block:: python

    >>> url = "http://localhost:8500/bfs/token"
    >>> data = {"username":"admin","password":"password"}
    >>> r = requests.post(url, data=data)
    >>> j = r.json()
    >>> print j["status"]
    ok
    >>> token = j["data"]
    >>> cmd = 'server.newdb "test"; server.listdb;'  # issue two commands
    >>> url = "http://localhost:8500/bfs/query"
    >>> data = {"token":token,"query":cmd}
    >>> r = requests.post(url, data=data)
    >>> j = r.json()
    >>> print j["status"]
    ok
    >>> print j["data"][-1]  # get last result
    [u'test']

**Content creation: BQL script**: ch1_script.bql

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

**Load and execute script**

.. code-block:: python

    >>> with open("ch1_script.bql","r") as f:
    ...     cmd = f.read()
    ... 
    >>> url = "http://localhost:8500/bfs/query"
    >>> data = {"token":token,"query":cmd}
    >>> r = requests.post(url, data=data)
    >>> j = r.json()
    >>> j["status"]
    u'ok'
    >>> len(j["data"][-1])
    3 