#
# Copyright (c) 2009-2020 Red Hat, Inc.
#
# Authors: Andrew Beekhof
#	   Steven Dake (sdake@redhat.com)
#
# This software licensed under BSD license, the text of which follows:
#
# Redistribution and use in source and binary forms, with or without
# modification, are permitted provided that the following conditions are met:
#
# - Redistributions of source code must retain the above copyright notice,
#   this list of conditions and the following disclaimer.
# - Redistributions in binary form must reproduce the above copyright notice,
#   this list of conditions and the following disclaimer in the documentation
#   and/or other materials provided with the distribution.
# - Neither the name of the MontaVista Software, Inc. nor the names of its
#   contributors may be used to endorse or promote products derived from this
#   software without specific prior written permission.
#
# THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS"
# AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE
# IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE
# ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT OWNER OR CONTRIBUTORS BE
# LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR
# CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF
# SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS
# INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN
# CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE)
# ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF
# THE POSSIBILITY OF SUCH DAMAGE.

MAINTAINERCLEANFILES	= Makefile.in

EXTRA_DIST		= ploadstart.sh

noinst_PROGRAMS		= testcpg testcpg2 cpgbench \
			  testquorum testvotequorum1 testvotequorum2	\
			  stress_cpgfdget stress_cpgcontext cpgbound testsam \
			  testcpgzc cpgbenchzc testzcgc stress_cpgzc \
			  testquorummodel testcfg

noinst_SCRIPTS		= ploadstart

testcpg_LDADD		= $(LIBQB_LIBS) $(top_builddir)/lib/libcpg.la
testcpg2_LDADD		= $(LIBQB_LIBS) $(top_builddir)/lib/libcpg.la
testcpgzc_LDADD		= $(LIBQB_LIBS) $(top_builddir)/lib/libcpg.la
testzcgc_LDADD		= $(LIBQB_LIBS) $(top_builddir)/lib/libcpg.la
stress_cpgzc_LDADD	= $(LIBQB_LIBS) $(top_builddir)/lib/libcpg.la
stress_cpgfdget_LDADD	= $(LIBQB_LIBS) $(top_builddir)/lib/libcpg.la
stress_cpgcontext_LDADD	= $(LIBQB_LIBS) $(top_builddir)/lib/libcpg.la
testquorum_LDADD	= $(LIBQB_LIBS) $(top_builddir)/lib/libquorum.la
testquorummodel_LDADD	= $(LIBQB_LIBS) $(top_builddir)/lib/libquorum.la
testvotequorum1_LDADD	= $(LIBQB_LIBS) $(top_builddir)/lib/libvotequorum.la
testvotequorum2_LDADD	= $(LIBQB_LIBS) $(top_builddir)/lib/libvotequorum.la
cpgbound_LDADD		= $(LIBQB_LIBS) $(top_builddir)/lib/libcpg.la
cpgbench_LDADD		= $(LIBQB_LIBS) $(top_builddir)/lib/libcpg.la
cpgbenchzc_LDADD	= $(LIBQB_LIBS) $(top_builddir)/lib/libcpg.la \
			  $(top_builddir)/common_lib/libcorosync_common.la
testsam_LDADD		= $(LIBQB_LIBS) $(top_builddir)/lib/libsam.la \
			  $(top_builddir)/lib/libcmap.la
testcfg_LDADD		= $(LIBQB_LIBS) $(top_builddir)/lib/libcfg.la

if HAVE_CRC32
noinst_PROGRAMS	        += cpghum cpgverify
cpghum_LDADD            = $(LIBQB_LIBS) $(top_builddir)/lib/libcpg.la -lz
cpgverify_LDADD		= $(LIBQB_LIBS) $(top_builddir)/lib/libcpg.la -lz
endif

ploadstart: ploadstart.sh
	$(SED) -e 's#@''BASHPATH@#${BASHPATH}#g' $< > $@
	chmod 755 $@

LINT_FILES1:=$(filter-out sa_error.c, $(wildcard *.c))
LINT_FILES:=$(filter-out testparse.c, $(LINT_FILES1))

lint:
	-for f in $(LINT_FILES) ; do echo Splint $$f ; splint $(LINT_FLAGS) $(CPPFLAGS) $(CFLAGS) $$f ; done

clean-local:
	rm -f ploadstart
