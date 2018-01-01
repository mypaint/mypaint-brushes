mypaint-brushes - MyPaint brushes
=================================

Brushes used by MyPaint and other software using libmypaint.

Building
---------

mypaint-brushes package can be installed as a typical autotools build:

> ./configure --prefix=/some/prefix && make && make install

See also `INSTALL` file.

There are also historical scons scripts, but they work only with scons
2.x (and in particular not newer scons 3, based on Python 3):

# Normal build
> scons prefix=/your/application/install/prefix

# Show build options
> scons -h
