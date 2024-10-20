# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2024 dev <dev@idea.lan>

include $(TOPDIR)/rules.mk

PKG_NAME:=vnt-server
PKG_VERSION:=1.2.12
PKG_RELEASE:=1

PKG_SOURCE_HEADER:=vnts
PKG_SOURCE_BODY:=unknown-linux-musl
PKG_SOURCE_FOOTER:=tar.gz

PKG_SOURCE_URL:=https://github.com/vnt-dev/vnts/releases/download/v$(PKG_VERSION)/

ifeq ($(ARCH),aarch64)
  PKG_SOURCE:=$(PKG_SOURCE_HEADER)-aarch64-$(PKG_SOURCE_BODY)-v$(PKG_VERSION).$(PKG_SOURCE_FOOTER)
  PKG_HASH:=bb6023c114c808435258e2f9f5f2c1f5e4f73df994f42e0cd301cf39df4c45c9
else ifeq ($(ARCH),arm)
  ARM_CPU_FEATURES:=$(word 2,$(subst +,$(space),$(call qstrip,$(CONFIG_CPU_TYPE))))
  ifeq ($(ARM_CPU_FEATURES),)
    PKG_SOURCE:=$(PKG_SOURCE_HEADER)-arm-$(PKG_SPURCE_BODY)eabi-v$(PKG_VERSION).$(PKG_SOURCE_FOOTER)
    PKG_HASH:=f52880d14ba47908b302aca533ff5f46c6018fa39f393fb273d1ee8122f907f8
  else
    PKG_SOURCE:=$(PKG_SOURCE_HEADER)-arm-$(PKG_SPURCE_BODY)eabihf-v$(PKG_VERSION).$(PKG_SOURCE_FOOTER)
    PKG_HASH:=2b60eb5ad73fdcd52774b3f12b759cb359549266762fb34ce206ed46137f7403
  endif
else ifeq ($(ARCH),x86_64)
  PKG_SOURCE:=$(PKG_SOURCE_HEADER)-x86_64-$(PKG_SPURCE_BODY)-v$(PKG_VERSION).$(PKG_SOURCE_FOOTER)
  PKG_HASH:=5a44eed7340d8517a1850110da0a750da1e5f14ff497ec8e11e54cb646143b45
else ifeq ($(ARCH),mips)
  PKG_SOURCE:=$(PKG_SOURCE_HEADER)-mips-$(PKG_SPURCE_BODY)-v$(PKG_VERSION).$(PKG_SOURCE_FOOTER)
  PKG_HASH:=90634571c2ae71d16c97673c22f8f5288ee3ab23e12801821c22bdf8aed2c0e3
else ifeq ($(ARCH),mipsel)
  PKG_SOURCE:=$(PKG_SOURCE_HEADER)-mipsel-$(PKG_SPURCE_BODY)-v$(PKG_VERSION).$(PKG_SOURCE_FOOTER)
  PKG_HASH:=ad1e065f5bb26339d9dc54ac9e1289495a68a5019813e2b71b2f42ce5fec03ad
else
  PKG_SOURCE:=dummy
  PKG_HASH:=dummy
endif

PKG_MAINTAINER:=dev <dev@idea.lan>
PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=LICENSE

include $(INCLUDE_DIR)/package.mk

TAR_CMD:=$(HOST_TAR) -C $(PKG_BUILD_DIR) $(TAR_OPTIONS)

define Package/vnt-server
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=VPN
  TITLE:=vnt server
  URL:=https://github.com/vnt-dev/vnts
  DEPENDS:=@(aarch64||arm||mips||mipsel||x86_64) @!(TARGET_x86_geode||TARGET_x86_legacy) +kmod-tun
endef

define Package/vnt-server/description
  An efficient VPN. Simple and efficient remote networking and intranet penetration tool.
endef

define Build/Compile
endef

define Package/vnt-server/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/vnts $(1)/usr/bin/vnts
endef

$(eval $(call BuildPackage,vnt-server))
