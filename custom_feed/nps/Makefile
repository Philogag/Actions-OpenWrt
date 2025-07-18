# SPDX-License-Identifier: GPL-3.0-only
#
# Copyright (C) 2021 ImmortalWrt.org

include $(TOPDIR)/rules.mk

PKG_NAME:=nps
PKG_VERSION:=0.26.18
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/yisier/nps/tar.gz/v$(PKG_VERSION)?
PKG_HASH:=29da044262071a1fa53ce7169c6427ee4f12fc0ada60ef7fb52fabfd165afe91

PKG_LICENSE:=Apache-2.0
PKG_LICENSE_FILE:=LICENSE
PKG_MAINTAINTER:=Tianling Shen <cnsztl@immortalwrt.org>

PKG_CONFIG_DEPENDS:=
PKG_BUILD_DEPENDS:=golang/host
PKG_BUILD_PARALLEL:=1
PKG_USE_MIPS16:=0

GO_PKG:=ehang.io/nps
GO_PKG_BUILD_PKG:=ehang.io/nps/cmd/...
GO_PKG_LDFLAGS:=-s -w

include $(INCLUDE_DIR)/package.mk
include $(TOPDIR)/feeds/packages/lang/golang/golang-package.mk

define Package/nps/template
  SECTION:=net
  CATEGORY:=Network
  TITLE:=A intranet penetration proxy server ($(1))
  DEPENDS:=$(GO_ARCH_DEPENDS) +ca-bundle
  URL:=https://ehang-io.github.io/nps
endef

Package/npc = $(call Package/nps/template,client)
Package/nps = $(call Package/nps/template,server)

define Package/nps/description/template
  NPS is a lightweight, high-performance, powerful intranet penetration proxy server,
  with a powerful web management terminal.
endef

Package/npc/description = $(Package/nps/description/template)
Package/nps/description = $(Package/nps/description/template)

define Build/Compile
	$(call GoPackage/Build/Compile)
endef

define Package/nps/install/template
	$(call GoPackage/Package/Install/Bin,$(PKG_INSTALL_DIR))
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/$(2) $(1)/usr/bin/$(2)
endef

Package/npc/install = $(call Package/nps/install/template,$(1),npc)
Package/nps/install = $(call Package/nps/install/template,$(1),nps)

$(eval $(call GoBinPackage,npc))
$(eval $(call GoBinPackage,nps))
$(eval $(call BuildPackage,npc))
$(eval $(call BuildPackage,nps))
