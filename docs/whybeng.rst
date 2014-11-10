Why Bytengine
=============

Bytengine is designed to be a lightweight content repository for storing JSON
documents as well as digital assets. Your data is stored in files that can be 
organised using directories, similar to a regular OS file system.

A BFS (Bytengine File System) file is made up of two layers, the JSON data layer
and the bytes data layer. This allows you for example to store digital assets 
along with their metadata that can be queried using Bytengine Query Language (BQL).

Bytengine's role in your application stack is to store form data in JSON format or
as raw bytes (if it happens to be a scanned document, word document or pdf document)
and to allow you to organise and query that data easily. This means that it is the
ideal repository for questionnaire data, cv and application form data, and general
business form data. The ability to structure your data into directories also means
you can build a sophisticated workflow layer which goes beyond just adding a status
field to track a forms progress within a process.

Bytengine is written in `Go <https://golang.org/>`_ and is open source so you can
extended it to include features particular to your application's needs.