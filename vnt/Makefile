# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2024 dev <dev@idea.lan>

include $(TOPDIR)/rules.mk

PKG_NAME:=vnt-client
PKG_VERSION:=1.2.14
PKG_RELEASE:=1

PKG_SOURCE_HEADER:=vnt
PKG_SOURCE_BODY:=unknown-linux-musl
PKG_SOURCE_FOOTER:=tar.gz

PKG_SOURCE_URL:=https://github.com/vnt-dev/vnt/releases/download/v$(PKG_VERSION)/

ifeq ($(ARCH),aarch64)
  PKG_SOURCE:=$(PKG_SOURCE_HEADER)-aarch64-$(PKG_SOURCE_BODY)-v$(PKG_VERSION).$(PKG_SOURCE_FOOTER)
  PKG_HASH:=24bf4d9193dc13361739fb98dcc743ee5ee9133a525e9d9241e51516171cf27f
else ifeq ($(ARCH),arm)
  ARM_CPU_FEATURES:=$(word 2,$(subst +,$(space),$(call qstrip,$(CONFIG_CPU_TYPE))))
  ifeq ($(ARM_CPU_FEATURES),)
    PKG_SOURCE:=$(PKG_SOURCE_HEADER)-arm-$(PKG_SPURCE_BODY)eabi-v$(PKG_VERSION).$(PKG_SOURCE_FOOTER)
    PKG_HASH:=8e070f8b87da31e6b6ce08677c3bb211de1e370985e82a1290968ad8d2b47bcd
  else
    PKG_SOURCE:=$(PKG_SOURCE_HEADER)-arm-$(PKG_SPURCE_BODY)eabihf-v$(PKG_VERSION).$(PKG_SOURCE_FOOTER)
    PKG_HASH:=39282e42560609fe96bcb317d812474033919cdf4e7f232dc446b6c137161183
  endif
else ifeq ($(ARCH),i386)
  PKG_SOURCE:=$(PKG_SOURCE_HEADER)-i686-$(PKG_SPURCE_BODY)-v$(PKG_VERSION).$(PKG_SOURCE_FOOTER)
  PKG_HASH:=82cca7a91f3a4ad82c3abc091981b5424ae711b82c34de0a9baf2c46d7550d62
else ifeq ($(ARCH),x86_64)
  PKG_SOURCE:=$(PKG_SOURCE_HEADER)-x86_64-$(PKG_SPURCE_BODY)-v$(PKG_VERSION).$(PKG_SOURCE_FOOTER)
  PKG_HASH:=b2c0873fc9c40f55e5e38bd56085e73bba255bd35b01716fc38b4244f526f8f9
else ifeq ($(ARCH),mips)
  PKG_SOURCE:=$(PKG_SOURCE_HEADER)-mips-$(PKG_SPURCE_BODY)-v$(PKG_VERSION).$(PKG_SOURCE_FOOTER)
  PKG_HASH:=313a4f6d413427d774f25cd75fbba69a0784d241de22455af0eee19b446afe10
else ifeq ($(ARCH),mipsel)
  PKG_SOURCE:=$(PKG_SOURCE_HEADER)-mipsel-$(PKG_SPURCE_BODY)-v$(PKG_VERSION).$(PKG_SOURCE_FOOTER)
  PKG_HASH:=86f5b962872ef7bd2616bcaeacef89e10abbf729279e26d2d3dbb12ef10a983b
else
  PKG_SOURCE:=dummy
  PKG_HASH:=dummy
endif

PKG_MAINTAINER:=dev <dev@idea.lan>
PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=LICENSE

include $(INCLUDE_DIR)/package.mk

TAR_CMD:=$(HOST_TAR) -C $(PKG_BUILD_DIR) $(TAR_OPTIONS)

define Package/vnt-client
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=VPN
  TITLE:=vnt networking
  URL:=https://github.com/vnt-dev/vnt
  DEPENDS:=@(aarch64||arm||mips||mipsel||i386||x86_64) @!(TARGET_x86_geode||TARGET_x86_legacy) +kmod-tun
endef

define Package/vnt-client/description
  An efficient VPN. Simple and efficient remote networking and intranet penetration tool.
endef

define Build/Compile
endef

define Package/vnt-client/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/vnt-cli $(1)/usr/bin/vnt-cli
endef

$(eval $(call BuildPackage,vnt-client))
