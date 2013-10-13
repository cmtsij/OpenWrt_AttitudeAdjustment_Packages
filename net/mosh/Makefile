#
# Copyright (C) 2006-2012 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=mosh
PKG_RELEASE:=1
PKG_REV:=45bba44
PKG_VERSION:=$(PKG_REV)

PKG_SOURCE:=$(PKG_NAME)-git-$(PKG_VERSION).tar.bz2
PKG_SOURCE_URL:=https://github.com/keithw/mosh
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_VERSION:=$(PKG_REV)
PKG_SOURCE_PROTO:=git

include $(INCLUDE_DIR)/package.mk

define Package/mosh-server
	SECTION:=net
	CATEGORY:=Network
	SUBMENU:=Mosh
	TITLE:=Mobile Shell(replacement for SSH)
	MAINTAINER:=Tung-Yi Chen <cmtsij@gmail.com>
	DEPENDS:=+libopenssl +libncurses +protobuf
	URL:=http://mosh.mit.edu/
endef

define Package/mosh-server/Description
	Mobile shell that supports roaming and intelligent local echo.
	Mosh is a remote terminal application that supports:
		- intermittent network connectivity,
		- roaming to different IP address without dropping the connection, and
		- intelligent local echo and line editing to reduce the effects of "network lag" on high-latency connections.
endef

CONFIGURE_ARGS += \
	--disable-client \
	--disable-hardening


define Build/Configure
	(cd $(PKG_BUILD_DIR) ; test -x ./autogen.sh && ./autogen.sh || true)
	$(call Build/Configure/Default)
endef

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR) DESTDIR="$(PKG_INSTALL_DIR)" all install-exec
endef


define Package/mosh-server/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/mosh-server $(1)/usr/bin/
endef

$(eval $(call BuildPackage,mosh-server))

