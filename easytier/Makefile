# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2024 dev <dev@idea.lan>

include $(TOPDIR)/rules.mk

PKG_NAME:=easytier
PKG_VERSION:=2.0.3
PKG_RELEASE:=1

PKG_SOURCE_HEADER:=easytier
PKG_SOURCE_SYSTEM:=linux
PKG_SOURCE_FOOTER:=zip

PKG_SOURCE_URL:=https://github.com/EasyTier/EasyTier/releases/download/v$(PKG_VERSION)/

ifeq ($(ARCH),aarch64)
  PKG_SOURCE:=$(PKG_SOURCE_HEADER)-$(PKG_SOURCE_SYSTEM)-aarch64-v$(PKG_VERSION).$(PKG_SOURCE_FOOTER)
  PKG_HASH:=52d545bcdd3a5a8a069838fae7cdec43d4c2f5166795e75bf5b9bfb07c57d181
  PKG_SOURCE_DIR_NAME:=$(PKG_SOURCE_HEADER)-$(PKG_SOURCE_SYSTEM)-aarch64
else ifeq ($(ARCH),arm)
  ARM_CPU_FEATURES:=$(word 2,$(subst +,$(space),$(call qstrip,$(CONFIG_CPU_TYPE))))
  ifeq ($(ARM_CPU_FEATURES),)
    PKG_SOURCE:=$(PKG_SOURCE_HEADER)-$(PKG_SOURCE_SYSTEM)-arm-v$(PKG_VERSION).$(PKG_SOURCE_FOOTER)
    PKG_HASH:=d570e8301bc411a018297e584ac160653df87db4955cdcc1b72f592ee25348be
    PKG_SOURCE_DIR_NAME:=$(PKG_SOURCE_HEADER)-$(PKG_SOURCE_SYSTEM)-arm
  else
    PKG_SOURCE:=$(PKG_SOURCE_HEADER)-$(PKG_SOURCE_SYSTEM)-armhf-v$(PKG_VERSION).$(PKG_SOURCE_FOOTER)
    PKG_HASH:=9db5d102fa440d05435ea46c79066cf247ef33af84126d61b45cfa4effa2fcb4
    PKG_SOURCE_DIR_NAME:=$(PKG_SOURCE_HEADER)-$(PKG_SOURCE_SYSTEM)-armhf
  endif
else ifeq ($(ARCH),x86_64)
  PKG_SOURCE:=$(PKG_SOURCE_HEADER)-$(PKG_SOURCE_SYSTEM)-x86_64-v$(PKG_VERSION).$(PKG_SOURCE_FOOTER)
  PKG_HASH:=ca9b3b850c066f210ee7a0b93b18a21ce1ed4bf4e4cd9530aee42350286b9cb7
  PKG_SOURCE_DIR_NAME:=$(PKG_SOURCE_HEADER)-$(PKG_SOURCE_SYSTEM)-x86_64
else ifeq ($(ARCH),mips)
  PKG_SOURCE:=$(PKG_SOURCE_HEADER)-$(PKG_SOURCE_SYSTEM)-mips-v$(PKG_VERSION).$(PKG_SOURCE_FOOTER)
  PKG_HASH:=fb9e2f0170507ad5cbd08a7bdf9d502598c8c420ba7aeb395478d0a53992d6a4
  PKG_SOURCE_DIR_NAME:=$(PKG_SOURCE_HEADER)-$(PKG_SOURCE_SYSTEM)-mips
else ifeq ($(ARCH),mipsel)
  PKG_SOURCE:=$(PKG_SOURCE_HEADER)-$(PKG_SOURCE_SYSTEM)-mipsel-v$(PKG_VERSION).$(PKG_SOURCE_FOOTER)
  PKG_HASH:=7ead866df025d9c84159db3fdb5680f6da104b6ea40ac61601712ae3ef57e2ba
  PKG_SOURCE_DIR_NAME:=$(PKG_SOURCE_HEADER)-$(PKG_SOURCE_SYSTEM)-mipsel
else
  PKG_SOURCE:=dummy
  PKG_HASH:=dummy
  PKG_SOURCE_DIR_NAME:=dummy
endif

PKG_MAINTAINER:=dev <dev@idea.lan>
PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=LICENSE

include $(INCLUDE_DIR)/package.mk

UNZIP_CMD:=unzip -q -d $(PKG_BUILD_DIR) $(DL_DIR)/$(PKG_SOURCE)

define Package/easytier
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=VPN
  TITLE:=EasyTier networking
  URL:=https://github.com/EasyTier/EasyTier/
  DEPENDS:=@(aarch64||arm||mips||mipsel||x86_64) @!(TARGET_x86_geode||TARGET_x86_legacy) +kmod-tun
endef

define Package/easytier/description
  A simple, decentralized mesh VPN with WireGuard support.
endef

define Build/Compile
endef

define Package/easytier/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/$(PKG_SOURCE_DIR_NAME)/easytier-core $(1)/usr/bin/easytier-core
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/$(PKG_SOURCE_DIR_NAME)/easytier-cli $(1)/usr/bin/easytier-cli
endef

$(eval $(call BuildPackage,easytier))
