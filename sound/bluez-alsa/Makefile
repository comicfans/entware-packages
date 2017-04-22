#
# Copyright (C) 2007-2015 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=bluez-alsa
PKG_VERSION:=1.2.0
PKG_RELEASE:=1

PKG_SOURCE:=v$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://github.com/Arkq/bluez-alsa/release
PKG_MD5SUM:=7a6710f4c6d693417fc09db61b1b2cdb
PKG_MAINTAINER:=comicfans <comicfans@gmail.com>

PKG_BUILD_DEPDS:=+libortp

PKG_FIXUP:=libtool

PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=LICENSE.txt
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk

define Package/bluez-alsa/Default
  URL:=https://github.com/Arkq/bluez-alsa
  DEPENDS:=@BUILD_PATENTED
endef

define Package/bluez-alsa
  $(call Package/bluez-alsa/Default)
  SECTION:=sound
  CATEGORY:=Sound
  TITLE:=bluez alsa
  DEPENDS:=+bluez-libs +sbc +alsa-lib +glib2 $(ICONV_DEPENDS) $(INTL_DEPENDS)
endef

CONFIGURE_ARGS += \
	--with-libiconv-prefix="$(ICONV_PREFIX)" \
	--with-libintl-prefix="$(INTL_PREFIX)" \


define Build/Configure
	$(call Build/Configure/Default, \
		--enable-shared \
		--disable-hcitop \
		--disable-static \
	)
endef


define Package/bluez-alsa/install
	$(INSTALL_DIR) $(1)/opt/lib/alsa-lib
	$(CP) \
		$(PKG_INSTALL_DIR)/opt/lib/alsa-lib/libasound_module*.so* \
		$(1)/opt/lib/alsa-lib/

	$(INSTALL_DIR) \
		$(1)/opt/bin

	$(INSTALL_BIN) \
		$(PKG_INSTALL_DIR)/opt/bin/bluealsa* \
		$(1)/opt/bin/

endef


$(eval $(call BuildPackage,bluez-alsa))
