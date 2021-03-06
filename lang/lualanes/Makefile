#
# Copyright (C) 2007-2014 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=lualanes
PKG_VERSION:=3.13.0
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/LuaLanes/lanes/tar.gz/v$(PKG_VERSION)?
PKG_HASH:=53a17d7ee11f17ca0543ae5aa640208dcb62d37862a0d0ea450455fae12c8ff1
PKG_BUILD_DIR:=$(BUILD_DIR)/lanes-$(PKG_VERSION)

PKG_INSTALL:=1
PKG_BUILD_PARALLEL:=1

PKG_BUILD_DEPENDS:=lua/host

include $(INCLUDE_DIR)/package.mk

define Package/lualanes
	SUBMENU:=Lua
	SECTION:=lang
	CATEGORY:=Languages
	TITLE:=LuaLanes
	URL:=http://luaforge.net/projects/lanes/
	DEPENDS:=+lua +luac +liblua +libpthread
	MAINTAINER:=Vladimir Malyutin <first-leon@yandex.ru>
endef

define Package/lualanes/description
	Lanes is a lightweight, native, lazy evaluating multithreading library for Lua 5.1 and 5.2.
endef

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR) all \
        CC="$(TARGET_CC)" \
        LUA="$(STAGING_DIR_HOSTPKG)/bin/lua" \
        LUAC="$(STAGING_DIR_HOSTPKG)/bin/luac" \
	LUA_FLAGS= \
	LUA_LIBS=-llua \
        OPT_FLAGS="$(TARGET_CFLAGS) -Dpthread_yield=sched_yield"
endef

define Package/lualanes/install
	$(INSTALL_DIR) $(1)/usr/lib/lua
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/lanes.lua $(1)/usr/lib/lua/
	$(INSTALL_DIR) $(1)/usr/lib/lua/lanes
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/src/lanes/core.so $(1)/usr/lib/lua/lanes/core.so
endef

$(eval $(call BuildPackage,lualanes))
