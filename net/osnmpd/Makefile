include $(TOPDIR)/rules.mk

PKG_NAME:=osnmpd
PKG_VERSION:=2017-08-20
PKG_RELEASE=$(PKG_SOURCE_VERSION)

PKG_SOURCE_URL:=git://github.com/verrio/osnmpd.git
PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=09cd9731e11f6f1a128fbe2efdaec516474bd295
PKG_LICENSE:=MIT
PKG_FIXUP:=autoreconf
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/osnmpd/Default
  SECTION:=network
  CATEGORY:=services
  TITLE:=SNMP agent
  URL:=https://github.com/verrio/osnmpd/
endef

define Package/osnmpd
  $(call Package/osnmpd/Default)
  TITLE+= Daemon
  DEPENDS:=+libconfig +libopenssl +libsensors +zlib
endef

define Package/osnmpd/description
  osnmpd is an SNMPv3 agent.  It exposes network statistics 
  and unsollicited notifications to remote NMS systems.
endef

define Package/osnmpd/conffiles
  /etc/snmp/snmpd.conf
endef

define Package/osnmpd/install
	$(INSTALL_DIR) \
		$(1)/etc/init.d \
		$(1)/etc/snmp \
		$(1)/usr/sbin \
		$(1)/usr/lib/snmp/plugins

	$(INSTALL_BIN) \
		./files/osnmpd.init $(1)/etc/init.d/snmpd

	$(INSTALL_BIN) \
		$(PKG_INSTALL_DIR)/usr/bin/snmpd $(1)/usr/sbin/snmpd

	$(INSTALL_BIN) \
		$(PKG_INSTALL_DIR)/usr/lib/snmp/plugins/* \
		$(1)/usr/lib/snmp/plugins

	$(INSTALL_CONF) \
		./files/osnmpd.config $(1)/etc/snmp/snmpd.conf
endef

$(eval $(call BuildPackage,osnmpd))
