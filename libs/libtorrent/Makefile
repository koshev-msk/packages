#
# Copyright (C) 2007-2015 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=libtorrent
PKG_VERSION:=0.16.28
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/rakshasa/libtorrent
PKG_SOURCE_VERSION:=v$(PKG_VERSION)
#PKG_MIRROR_HASH:=f5baa923bf45b84a2d1a8bc279815fc5d4f460e581e2d0e3070b97f134301378
PKG_MIRROR_HASH:=38214a3fcbad5f09293ce96b5725aaef666156b0fabc2b47b5160d4ab86e271f

PKG_MAINTAINER:=Rosen Penev <rosenp@gmail.com>
PKG_LICENSE:=GPL-2.0-or-later
PKG_LICENSE_FILES:=COPYING

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1
PKG_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/package.mk

define Package/libtorrent
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=Rakshasa's BitTorrent library
  URL:=https://rakshasa.github.io/rtorrent/
  DEPENDS:=+libcurl +libopenssl +libstdcpp +zlib
endef

define Package/libtorrent/description
 LibTorrent is a BitTorrent library written in C++ for *nix, with a focus on
 high performance and good code. The library differentiates itself from other
 implementations by transferring directly from file pages to the network stack.
 On high-bandwidth connections it is able to seed at 3 times the speed of the
 official client.
endef

CONFIGURE_ARGS += \
	--enable-shared \
	--disable-static \
	--disable-aligned \
	--disable-debug \
	--disable-instrumentation \
	--with-epoll \
	--with-zlib=$(STAGING_DIR)/usr \
	--without-kqueue

TARGET_CXXFLAGS += -std=gnu++20


define Package/libtorrent/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libtorrent.so* $(1)/usr/lib/
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include
	$(CP) $(PKG_INSTALL_DIR)/usr/include/torrent $(1)/usr/include/
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libtorrent.* $(1)/usr/lib/
	$(INSTALL_DIR) $(1)/usr/lib/pkgconfig
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/pkgconfig/libtorrent.pc $(1)/usr/lib/pkgconfig/
endef



$(eval $(call BuildPackage,libtorrent))
