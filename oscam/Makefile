#
# Copyright (C) 2015 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=oscam
PKG_REV:=11693
PKG_VERSION:=1.20-$(PKG_REV)
PKG_RELEASE:=1
PKG_SOURCE_VERSION:=a454c6702436479f369a202c5b55bbcc452a4770
PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=master
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_URL:=https://github.com/nx111/oscam.git
PKG_SOURCE:=$(PKG_SOURCE_SUBDIR).tar.bz2
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)
PKG_LICENSE:=GPL-3.0
PKG_LICENSE_FILES:=COPYING
PKG_BUILD_PARALLEL:=1
PKG_USE_MIPS16:=0

include $(INCLUDE_DIR)/package.mk

define Package/oscam
  SECTION:=DVB-EXTRAS
  CATEGORY:=DVB-EXTRAS
  DEPENDS:=+libopenssl +libusb-1.0 +kmod-usb-serial +kmod-usb-serial-ch341 +kmod-usb-serial-ftdi +kmod-usb-serial-pl2303 +libpcsclite +pcscd +ccid
  TITLE:=OSCam is an Open Source Conditional Access Module software
  URL:=http://www.streamboard.tv/oscam/
endef

define Package/oscam/description
  OSCam is an Open Source Conditional Access Module software,
  based on the very good MpCS version 0.9d created by 鈥媎ukat.
endef

define Package/oscam/conffiles
/etc/oscam/oscam.conf
/etc/oscam/oscam.server
/etc/oscam/oscam.user
/etc/oscam/SoftCam.Key
/etc/oscam/oscam.dvbapi
endef

CONFIGURE_CMD = ./config.sh
CONFIGURE_ARGS = \
	--enable all

MAKE_FLAGS += \
	CONF_DIR=/etc/oscam \
	OSCAM_BIN=Distribution/oscam \
        USE_SSL=1 \
	USE_LIBUSB=1 \
	USE_PCSC=1 \
	USE_LIBCRYPTO=1 

define Package/oscam/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/Distribution/oscam $(1)/usr/bin/oscam

	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/oscam.init $(1)/etc/init.d/oscam

	$(INSTALL_DIR) $(1)/etc/oscam
	$(INSTALL_CONF) ./files/oscam.conf $(1)/etc/oscam
	$(INSTALL_CONF) ./files/oscam.server $(1)/etc/oscam
	$(INSTALL_CONF) ./files/oscam.user $(1)/etc/oscam
	$(INSTALL_CONF) ./files/SoftCam.Key $(1)/etc/oscam
	$(INSTALL_CONF) ./files/oscam.dvbapi $(1)/etc/oscam


endef

define Package/$(PKG_NAME)/prerm
	#!/bin/sh
	# if run within buildroot exit
	[ -n "$${IPKG_INSTROOT}" ] && exit 0

	# stop running scripts
	/etc/init.d/oscam disable
	/etc/init.d/oscam stop

	exit 0
endef

$(eval $(call BuildPackage,oscam))
