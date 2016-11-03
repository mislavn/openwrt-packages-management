#
# Copyright (C) 2016 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=netopeer2-authd

PKG_LICENSE:=BSD-3-Clause
PKG_MAINTAINER:=Mislav Novakovic <mislav.novakovic@sartura.hr>

PKG_NAME:=netopeer2-authd
PKG_VERSION:=0.3.6

PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=fcdc95cf6cac29163076554659432460c32699fb
PKG_SOURCE:=$(PKG_NAME)-$(PKG_SOURCE_VERSION).tar.bz2
PKG_SOURCE_URL:=https://github.com/CESNET/Netopeer2.git
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_SOURCE_VERSION)

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_SOURCE_SUBDIR)

PKG_BUILD_PARALLEL:=1
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/netopeer2-authd
  SECTION:=util
  CATEGORY:=Utilities
  DEPENDS:=+sysrepod +sysrepoctl +sysrepocfg +sysrepo-plugind +openssl
  TITLE:=Netopeer2 authd
endef

CMAKE_OPTIONS += \
	-DCMAKE_INSTALL_PREFIX=/usr \
	-DCMAKE_BUILD_TYPE:STRING=release

CMAKE_SOURCE_DIR=./authd

define Package/netopeer2-authd/install
	$(INSTALL_DIR) $(1)/lib/sysrepo/plugins
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/libauthd.so $(1)/lib/sysrepo/plugins

	$(INSTALL_DIR) $(1)/etc/sysrepo/yang
	$(INSTALL_CONF) $(PKG_BUILD_DIR)/modules/ietf-system.yang $(1)/etc/sysrepo/yang

	$(INSTALL_DIR) $(1)/etc/sysrepo/yang
	$(INSTALL_CONF) $(PKG_BUILD_DIR)/modules/ietf-system-keychain.yang $(1)/etc/sysrepo/yang

	$(INSTALL_DIR) $(1)/etc/sysrepo/yang
	$(INSTALL_CONF) $(PKG_BUILD_DIR)/modules/iana-crypt-hash.yang $(1)/etc/sysrepo/yang

	$(INSTALL_DIR) $(1)/etc/sysrepo/yang
	$(INSTALL_CONF) $(PKG_BUILD_DIR)/modules/ietf-x509-cert-to-name.yang $(1)/etc/sysrepo/yang

	$(INSTALL_DIR) $(1)/etc/sysrepo/yang
	$(INSTALL_CONF) $(PKG_BUILD_DIR)/modules/ietf-ssh-server.yang $(1)/etc/sysrepo/yang

	$(INSTALL_DIR) $(1)/etc/sysrepo/yang
	$(INSTALL_CONF) $(PKG_BUILD_DIR)/modules/ietf-tls-server.yang $(1)/etc/sysrepo/yang

	$(INSTALL_DIR) $(1)/tmp
	$(INSTALL_CONF) $(PKG_BUILD_DIR)/authd/stock_key_config.xml $(1)/tmp

	$(INSTALL_DIR) $(1)/etc/uci-defaults
	$(INSTALL_BIN) ./files/netopeer2-authd.default $(1)/etc/uci-defaults/netopeer2-authd
endef

$(eval $(call BuildPackage,netopeer2-authd))
