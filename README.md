# Bytengine Documentation

[![BQL](https://github.com/johnwilson/bytengine/raw/master/bql.png)](#bql.snippet)

## About

**[Bytengine](http://www.bytengine.io/ "Bytengine")** is a scalable content 
repository built with Go. Its API is accessible from any Http client library so 
you can start coding in your favorite language!

**[Bytengine](http://www.bytengine.io/ "Bytengine")** stores your JSON data and 
digital assets in a pseudo hierarchical file system which you query using it's 
inbuilt SQL like language.

## Build the documentation

Requires **[Mongodb](http://docs.mongodb.org/manual/installation/ "Mongodb")**
to build the docs locally. Once installed run the following

```
    cd $BYTENGINE_DOCS_LOCATION/docs
    export LOCAL_BUILD=True # to use the 'read the docs theme'
    make clean
    make html
```