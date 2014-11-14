.. _data-functions:

Data Filter Functions
=====================

Bytengine allows you to filter/modify commands results by redirecting their output
to **Filter Functions** (or user defined functions). This feature comes in handy
especially when you want to process the data server-side before returning it to 
your application.
The syntax to redirect output is ``>> function_name`` and can be used after any
bfs command.

Currently only a sample function ``pretty`` which pretty prints bfs commands is
included as an example but further useful ones will be added eventually. You can
view the filter function plugin code implementation in 
`/bytengine/fltcore/fltcore.go <https://github.com/johnwilson/bytengine/blob/master/fltcore/fltcore.go>`_.

**Example**::

    @db1.select "name" in /users >> pretty
    
    @db1.select "name" in /users >> my_custom_function