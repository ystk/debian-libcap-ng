# Makefile.am -- 
# Copyright 2009 Red Hat Inc., Durham, North Carolina.
# All Rights Reserved.
#
# This library is free software; you can redistribute it and/or
# modify it under the terms of the GNU Lesser General Public
# License as published by the Free Software Foundation; either
# version 2.1 of the License, or (at your option) any later version.
# 
# This library is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU
# Lesser General Public License for more details.
# 
# You should have received a copy of the GNU Lesser General Public
# License along with this library; if not, write to the Free Software
# Foundation, Inc., 59 Temple Place, Suite 330, Boston, MA  02111-1307  USA
# 
# Authors:
#   Steve Grubb <sgrubb@redhat.com>
#
SUBDIRS = test
EXTRA_DIST = capng_swig.i
CONFIG_CLEAN_FILES = *.loT *.rej *.orig
AM_CFLAGS = -fPIC -DPIC
PYLIBVER ?= python$(PYTHON_VERSION)
INCLUDES = -I. -I$(top_builddir) -I/usr/include/$(PYLIBVER)
LIBS = $(top_builddir)/src/libcap-ng.la
pyexec_PYTHON = capng.py
pyexec_LTLIBRARIES = _capng.la
pyexec_SOLIBRARIES = _capng.so
_capng_la_LDFLAGS = -module -avoid-version
_capng_la_HEADERS: $(top_builddir)/config.h 
_capng_la_DEPENDENCIES =${top_srcdir}/src/cap-ng.h ${top_builddir}/src/libcap-ng.la
nodist__capng_la_SOURCES  = capng_wrap.c
capng.py capng_wrap.c: ${srcdir}/capng_swig.i caps.h capng.h
	swig -o capng_wrap.c -python ${INCLUDES} ${srcdir}/capng_swig.i 
caps.h:
	cat /usr/include/linux/capability.h | grep '^#define CAP'  | grep -v '[()]' > caps.h
capng.h:
	cat ${top_srcdir}/src/cap-ng.h | grep -v '_state' > capng.h

CLEANFILES = capng.py* capng_wrap.c caps.h capng.h *~

