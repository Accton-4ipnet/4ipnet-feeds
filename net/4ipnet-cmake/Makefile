#
# Copyright (C) 2007-2015 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=4ipnet-cmake
PKG_VERSION:=1.0.0
PKG_RELEASE:=1

# PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
# PKG_SOURCE_URL:=http://10.2.14.1/~liam.huang/
# PKG_MD5SUM:=34178967967a3b193cdbb32ca97dd93b
PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL=git@github.com:Accton-4ipnet/4ipnet-cmake.git
PKG_SOURCE_BRANCH:=github/master
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_VERSION:=994878b6ed6aaf424d397ebae8dd5e6261c9526a
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_MAINTAINER:=liam.huang <liam.huang@4ipnet.com>
PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=COPYING

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)/$(PKG_NAME)-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/$(PKG_NAME)/Default
  SECTION:=net
  CATEGORY:=Network
  DEPENDS:=+libpcre
  SUBMENU:=4ipnet Customs
  TITLE:=Demo Hello world~
  URL:=http://4ipnet.com
endef

define Package/$(PKG_NAME)/Default/description
  make a good softwaire to earn money
  http://ju.outofmemory.cn/entry/216853
  https://raw.githubusercontent.com/curl/curl/master/docs/examples/10-at-a-time.c
endef

define Package/$(PKG_NAME)
$(call Package/$(PKG_NAME)/Default)
  DEPENDS+= +libcurl +libuci
  TITLE+= (A)
endef

define Package/$(PKG_NAME)/description
	$(call Package/$(PKG_NAME)/Default/description)
	Add other description
endef

define Package/$(PKG_NAME)/conffiles
endef
define Build/Prepare
	$(call Build/Prepare/Default)
	mkdir -p $(PKG_BUILD_DIR)
endef

define Package/$(PKG_NAME)/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/$(PKG_NAME) $(1)/usr/bin/$(PKG_NAME)
endef

define Package/$(PKG_NAME)/postinst
#!/bin/sh
if [ -e $${IPKG_INSTROOT}/usr/bin/$(PKG_NAME) ]; then
  rm -rf $${IPKG_INSTROOT}/usr/bin/$(PKG_NAME);
fi
ln -sf ./$(PKG_NAME) $${IPKG_INSTROOT}/usr/bin/$(PKG_NAME)
endef

define Package/$(PKG_NAME)/postrm
#!/bin/sh
rm $${IPKG_INSTROOT}/usr/bin/$(PKG_NAME)
exit 0
endef

$(eval $(call BuildPackage,$(PKG_NAME)))
