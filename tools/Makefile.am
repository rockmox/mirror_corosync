# Copyright (c) 2009 Red Hat, Inc.
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

sbin_PROGRAMS		= corosync-cfgtool \
			  corosync-keygen \
			  corosync-cpgtool corosync-quorumtool \
			  corosync-notifyd corosync-cmapctl

bin_SCRIPTS		= corosync-blackbox

if INSTALL_XMLCONF
bin_SCRIPTS		+= corosync-xmlproc
endif

noinst_HEADERS          = util.h

AM_CFLAGS		= $(knet_CFLAGS)

EXTRA_DIST		= corosync-xmlproc.sh \
			  corosync-notifyd.sysconfig.example \
                          corosync-blackbox.sh

corosync_cfgtool_SOURCES = corosync-cfgtool.c util.c

corosync_quorumtool_SOURCES = corosync-quorumtool.c util.c

corosync-xmlproc: corosync-xmlproc.sh
	$(SED) -e 's#@''DATADIR@#${datadir}#g' \
	       -e 's#@''BASHPATH@#${BASHPATH}#g' \
	       $< > $@

corosync-blackbox: corosync-blackbox.sh
	$(SED) -e 's#@''LOCALSTATEDIR@#${localstatedir}#g' $< > $@

corosync_cmapctl_LDADD	= $(LIBQB_LIBS) $(top_builddir)/common_lib/libcorosync_common.la $(top_builddir)/lib/libcmap.la

corosync_cfgtool_LDADD	= $(LIBQB_LIBS) $(top_builddir)/common_lib/libcorosync_common.la \
			  $(top_builddir)/lib/libcfg.la $(top_builddir)/lib/libcmap.la

corosync_cpgtool_LDADD	= $(LIBQB_LIBS) $(top_builddir)/lib/libcfg.la \
			  $(top_builddir)/lib/libcpg.la \
			  $(top_builddir)/common_lib/libcorosync_common.la

corosync_quorumtool_LDADD = $(LIBQB_LIBS) \
			    $(top_builddir)/lib/libcmap.la \
			    $(top_builddir)/lib/libcfg.la \
			    $(top_builddir)/lib/libquorum.la \
			    $(top_builddir)/lib/libvotequorum.la \
			    $(top_builddir)/common_lib/libcorosync_common.la

corosync_notifyd_CFLAGS   = $(DBUS_CFLAGS) $(libsystemd_CFLAGS)
corosync_notifyd_LDADD    = $(LIBQB_LIBS) $(DBUS_LIBS) $(SNMP_LIBS) \
			    $(libsystemd_LIBS) \
			    $(top_builddir)/lib/libcmap.la \
			    $(top_builddir)/lib/libcfg.la \
			    $(top_builddir)/lib/libquorum.la \
			    $(top_builddir)/common_lib/libcorosync_common.la

lint:
	-splint $(LINT_FLAGS) $(DBUS_CFLAGS) $(CPPFLAGS) $(CFLAGS) *.c

clean-local:
	rm -f corosync-xmlproc corosync-blackbox
