#
# This file and its contents are supplied under the terms of the
# Common Development and Distribution License ("CDDL"), version 1.0.
# You may only use this file in accordance with the terms of version
# 1.0 of the CDDL.
#
# A full copy of the text of the CDDL should have accompanied this
# source.  A copy of the CDDL is also available via the Internet at
# http://www.illumos.org/license/CDDL.
#

#
# Copyright 2015 Alexander Pyhalov
#

include ../../../make-rules/shared-macros.mk

COMPONENT_NAME= pango
COMPONENT_VERSION_MAJOR=1
COMPONENT_VERSION_MINOR=40
COMPONENT_VERSION_MICRO=3
COMPONENT_VERSION_DL= $(COMPONENT_VERSION_MAJOR).$(COMPONENT_VERSION_MINOR)
COMPONENT_VERSION= $(COMPONENT_VERSION_DL).$(COMPONENT_VERSION_MICRO)
COMPONENT_SUMMARY= GNOME core text and font handling libraries
COMPONENT_SRC= $(COMPONENT_NAME)-$(COMPONENT_VERSION)
COMPONENT_ARCHIVE= $(COMPONENT_SRC).tar.xz
COMPONENT_ARCHIVE_HASH= \
  sha256:abba8b5ce728520c3a0f1535eab19eac3c14aeef7faa5aded90017ceac2711d3
COMPONENT_ARCHIVE_URL= \
  http://ftp.gnome.org/pub/GNOME/sources/$(COMPONENT_NAME)/$(COMPONENT_VERSION_DL)/$(COMPONENT_ARCHIVE)
COMPONENT_PROJECT_URL = http://www.pango.org/
COMPONENT_FMRI= library/desktop/pango
COMPONENT_CLASSIFICATION= Desktop (GNOME)/Libraries
COMPONENT_LICENSE = LGPLv2
COMPONENT_LICENSE_FILE = COPYING

include $(WS_MAKE_RULES)/prep.mk
include $(WS_MAKE_RULES)/configure.mk
include $(WS_MAKE_RULES)/ips.mk

PATH=/usr/gnu/bin:/usr/bin

CONFIGURE_OPTIONS.32 = -sysconfdir=/etc
CONFIGURE_OPTIONS.64 = -sysconfdir=/etc/$(MACH64)
CONFIGURE_OPTIONS += $(CONFIGURE_OPTIONS.$(BITS))

COMPONENT_BUILD_ENV += CC="$(CC)"
COMPONENT_BUILD_ENV += CFLAGS="$(CFLAGS)"

COMPONENT_POST_INSTALL_ACTION.32 = ( $(RM) -fr $(PROTO_DIR)/etc/pango && $(MKDIR) $(PROTO_DIR)/etc/pango &&\
	$(ENV) LD_LIBRARY_PATH=$(PROTO_DIR)/usr/lib \
	$(PROTO_DIR)/usr/bin/pango-querymodules \
	  $(PROTO_DIR)/usr/lib/pango/*/modules/*.so   | sed -e "s:$(PROTO_DIR)::" \
	  > $(PROTO_DIR)/etc/pango/pango.modules )

COMPONENT_POST_INSTALL_ACTION.64 = ( $(RM) -fr $(PROTO_DIR)/etc/$(MACH64)/pango && $(MKDIR) $(PROTO_DIR)/etc/$(MACH64)/pango &&\
	$(ENV) LD_LIBRARY_PATH=$(PROTO_DIR)/usr/lib/$(MACH64) \
	$(PROTO_DIR)/usr/bin/$(MACH64)/pango-querymodules \
	  $(PROTO_DIR)/usr/lib/$(MACH64)/pango/*/modules/*.so | sed -e "s:$(PROTO_DIR)::" \
	  > $(PROTO_DIR)/etc/$(MACH64)/pango/pango.modules )

COMPONENT_POST_INSTALL_ACTION=$(COMPONENT_POST_INSTALL_ACTION.$(BITS))

build: $(BUILD_32_and_64)

install: $(INSTALL_32_and_64)

test: $(NO_TESTS)

REQUIRED_PACKAGES += library/c++/harfbuzz
REQUIRED_PACKAGES += library/desktop/cairo
REQUIRED_PACKAGES += library/glib2
REQUIRED_PACKAGES += system/library
REQUIRED_PACKAGES += system/library/fontconfig
REQUIRED_PACKAGES += system/library/freetype-2
REQUIRED_PACKAGES += system/library/math
REQUIRED_PACKAGES += x11/library/libx11
REQUIRED_PACKAGES += x11/library/libxft
REQUIRED_PACKAGES += x11/library/libxrender
