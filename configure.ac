AC_PREREQ(2.62)

## Canonical version number components ##

# Package version: see https://github.com/mypaint/libmypaint/wiki/Versioning
# See http://semver.org/ for what this means.
# This version is just the same as the current libmypaint version for
# now. It may get out of sync later on.
m4_define([mypaint_brushes_major], [1])
m4_define([mypaint_brushes_minor], [3])
m4_define([mypaint_brushes_micro], [0])

# The package version is "major.minor.micro[-prerelease]".
m4_define([mypaint_brushes_version],
          [mypaint_brushes_major.mypaint_brushes_minor.mypaint_brushes_micro])

# The data version indicates data compatibility.
# Basically this is part of 1.0 series of data which will work with
# libmypaint 1.x. It is not incremented with package versions unless
# incompatible changes in data format are made.
m4_define([mypaint_data_version], [1.0])

AC_INIT([MYPAINT_BRUSHES],
        [mypaint_brushes_version],
        [https://github.com/Jehan/mypaint-brushes/issues],
        [mypaint-brushes],
        [https://github.com/Jehan/mypaint-brushes])

AM_INIT_AUTOMAKE([no-define dist-xz no-dist-gzip
                  subdir-objects
                  foreign])

MYPAINT_BRUSHES_MAJOR_VERSION=mypaint_brushes_major
MYPAINT_BRUSHES_MINOR_VERSION=mypaint_brushes_minor
MYPAINT_BRUSHES_MICRO_VERSION=mypaint_brushes_micro
MYPAINT_BRUSHES_VERSION=mypaint_brushes_version
MYPAINT_DATA_VERSION=mypaint_data_version

AC_SUBST(MYPAINT_BRUSHES_MAJOR_VERSION)
AC_SUBST(MYPAINT_BRUSHES_MINOR_VERSION)
AC_SUBST(MYPAINT_BRUSHES_MICRO_VERSION)
AC_SUBST(MYPAINT_BRUSHES_VERSION)
AC_SUBST(MYPAINT_DATA_VERSION)

AC_PROG_INSTALL

# Initialize maintainer mode
AM_MAINTAINER_MODE([enable])

AC_CONFIG_FILES([
  brushes/Makefile
  Makefile
  mypaint-brushes-]mypaint_data_version()[.pc:pkgconfig.pc.in
])

AC_OUTPUT

echo ""
echo "  Configured mypaint-brushes $MYPAINT_BRUSHES_VERSION"
echo ""

