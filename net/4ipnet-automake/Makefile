#
# Copyright (C) 2007-2015 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=4ipnet-automake
PKG_VERSION:=1.0.0
PKG_RELEASE:=1

if [[ -z "$(GITPATH)" ]]; then
GITPATH=github.com:Accton-4ipnet
fi


# PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
# PKG_SOURCE_URL:=http://10.2.14.1/~liam.huang/
# PKG_MD5SUM:=4960ca9fa6aa3f3ab432d99878d7b347
PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL=git@$(GITPATH)/4ipnet-automake.git
PKG_SOURCE_BRANCH:=github/master
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_VERSION:=efda7cc8d1f55ac9ae13e6fd930b5e14f4b1db86
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_MAINTAINER:=liam.huang <liam.huang@4ipnet.com>
PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=COPYING

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)/$(PKG_NAME)-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/autotools.mk

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
  https://raw.githubusercontent.com/curl/curl/master/docs/examples/10-at-a-time.c
endef

define Package/$(PKG_NAME)
$(call Package/$(PKG_NAME)/Default)
  DEPENDS+= +libcurl
  TITLE+= (A)
endef

define Package/$(PKG_NAME)/description
	$(call Package/$(PKG_NAME)/Default/description)
	Add other description
endef

define Build/Configure
	cd $(PKG_BUILD_DIR); automake --add-missing; cd -
	$(call Build/Configure/Default,--with-linux-headers=$(LINUX_DIR))
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
