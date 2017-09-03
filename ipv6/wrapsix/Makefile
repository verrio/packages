#
# Copyright (C) 2006-2017 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=wrapsix
PKG_VERSION:=0.2.0
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=git://github.com/verrio/wrapsix.git
PKG_SOURCE_DATE:=2017-09-03
PKG_SOURCE_VERSION:=5fec4872e2bc036b84bf517d75eecd6dc48013fa
PKG_INSTALL:=1
PKG_FIXUP:=autoreconf

include $(INCLUDE_DIR)/package.mk

define Package/wrapsix/Default
  SECTION:=ipv6
  CATEGORY:=IPv6
  TITLE:=NAT64 user-space daemon
  URL:=https://www.wrapsix.org/
endef

define Package/wrapsix
  $(call Package/wrapsix/Default)
  TITLE+= Daemon
endef

define Package/wrapsix/description
wrapsix is a NAT64 daemon.  This daemon listens for incoming requests to a
NAT64 mapped subnet (by default 64:ff9b::/96, defined in RFC 6052) and 
translates them to their IPv4 destination, and vice-versa.  This IPv6 
transition mechanism is generally used in combination with a DNS64 resolver 
like Google's public DNS servers.  Effectively, this mechanisms allows 
disabling IPv4 on the end nodes, though has compatibility problems with 
some legacy, ill-conceived application protocols like Skype.
endef

define Package/wrapsix/conffiles
/etc/config/wrapsix
endef

define Package/wrapsix/install
	$(INSTALL_DIR) $(1)/etc/config
	$(INSTALL_CONF) ./files/wrapsix.config $(1)/etc/config/wrapsix
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/wrapsix.init $(1)/etc/init.d/wrapsix
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/sbin/wrapsix $(1)/usr/sbin/
endef

define Package/radvdump/install
	$(INSTALL_DIR) $(1)/usr/sbin
endef

$(eval $(call BuildPackage,wrapsix))
