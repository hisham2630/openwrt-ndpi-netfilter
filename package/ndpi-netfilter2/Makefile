 #
# Copyright (C) 2010 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/kernel.mk

PKG_NAME:=ndpi-netfilter2
PKG_VERSION:=0670f78
PKG_RELEASE:=1
PKG_REV:=0670f78

PKG_SOURCE_PROTO:=git
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_MIRROR_HASH:=d9a5c2c9455fdcd7181582e6079c7469b88628a0acf3cac8dcf1c2e7586f47da
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_URL:=https://github.com/vel21ripn/nDPI.git
PKG_SOURCE_VERSION:=$(PKG_REV)

PKG_BUILD_DIR:=$(KERNEL_BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1

include $(INCLUDE_DIR)/uclibc++.mk
include $(INCLUDE_DIR)/package.mk


CONFIGURE_ARGS += --with-pic
MAKE_PATH := ndpi-netfilter

define Package/iptables-mod-ndpi
	SUBMENU:=Firewall
	SECTION:=net
	CATEGORY:=Network
	TITLE:=ndpi successor of OpenDPI
	URL:=http://www.ntop.org/products/ndpi/
	DEPENDS:=+iptables +iptables-mod-conntrack-extra +kmod-ipt-ndpi
	MAINTAINER:=Thomas Heil <heil@terminal-consulting.de>
endef

define Package/iptables-mod-ndpi/description
  nDPI is a ntop-maintained superset of the popular OpenDPI library
endef

MAKE_FLAGS += KERNEL_DIR="$(LINUX_DIR)" MODULES_DIR="$(TARGET_MODULES_DIR)" 

define Package/iptables-mod-ndpi/install
	$(INSTALL_DIR) $(1)/usr/lib/iptables
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/ndpi-netfilter/ipt/libxt_ndpi.so $(1)/usr/lib/iptables
endef

define KernelPackage/ipt-ndpi
	SUBMENU:=Netfilter Extensions
	TITLE:= nDPI net netfilter module
	DEPENDS:=+kmod-nf-conntrack +kmod-nf-conntrack-netlink +kmod-ipt-compat-xtables
	KCONFIG:=CONFIG_NF_CONNTRACK_LABELS=y
	FILES:= \
	$(PKG_BUILD_DIR)/ndpi-netfilter/src/xt_ndpi.ko
	AUTOLOAD:=$(call AutoProbe,xt_ndpi)
endef

$(eval $(call BuildPackage,iptables-mod-ndpi))
$(eval $(call KernelPackage,ipt-ndpi))
