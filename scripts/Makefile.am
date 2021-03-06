pkgdatadir = $(datadir)/@PACKAGE@

dist_pkgdata_SCRIPTS = \
	$(top_srcdir)/scripts/zimport.sh \
	$(top_srcdir)/scripts/zfs.sh \
	$(top_srcdir)/scripts/zfs-tests.sh \
	$(top_srcdir)/scripts/zloop.sh \
	$(top_srcdir)/scripts/zfs-helpers.sh

EXTRA_DIST = \
	commitcheck.sh \
	common.sh.in \
	cstyle.pl \
	dkms.mkconf \
	dkms.postbuild \
	enum-extract.pl \
	kmodtool \
	make_gitrev.sh \
	man-dates.sh \
	paxcheck.sh \
	zfs2zol-patch.sed \
	zol2zfs-patch.sed

define EXTRA_ENVIRONMENT

# Only required for in-tree use
export INTREE="yes"
export GDB="/usr/bin/libtool --mode=execute gdb"
export LDMOD=/sbin/insmod

export CMD_DIR=@abs_top_builddir@/cmd
export UDEV_RULE_DIR=@abs_top_builddir@/udev/rules.d
export ZEDLET_ETC_DIR=$$CMD_DIR/zed/zed.d
export ZEDLET_LIBEXEC_DIR=$$CMD_DIR/zed/zed.d
export ZPOOL_SCRIPT_DIR=$$CMD_DIR/zpool/zpool.d
export ZPOOL_SCRIPTS_PATH=$$CMD_DIR/zpool/zpool.d
export CONTRIB_DIR=@abs_top_builddir@/contrib
export LIB_DIR=@abs_top_builddir@/lib

export INSTALL_UDEV_DIR=@udevdir@
export INSTALL_UDEV_RULE_DIR=@udevruledir@
export INSTALL_MOUNT_HELPER_DIR=@mounthelperdir@
export INSTALL_SYSCONF_DIR=@sysconfdir@
export INSTALL_PYTHON_DIR=@pythonsitedir@

export KMOD_SPL=@abs_top_builddir@/module/spl/spl.ko
export KMOD_ZAVL=@abs_top_builddir@/module/avl/zavl.ko
export KMOD_ZNVPAIR=@abs_top_builddir@/module/nvpair/znvpair.ko
export KMOD_ZUNICODE=@abs_top_builddir@/module/unicode/zunicode.ko
export KMOD_ZCOMMON=@abs_top_builddir@/module/zcommon/zcommon.ko
export KMOD_ZLUA=@abs_top_builddir@/module/lua/zlua.ko
export KMOD_ICP=@abs_top_builddir@/module/icp/icp.ko
export KMOD_ZFS=@abs_top_builddir@/module/zfs/zfs.ko
endef

export EXTRA_ENVIRONMENT

all-local:
	-$(SED) -e '\|^export BIN_DIR=|s|$$|@abs_top_builddir@/bin|' \
		-e '\|^export SBIN_DIR=|s|$$|@abs_top_builddir@/bin|' \
		-e '\|^export ZTS_DIR=|s|$$|@abs_top_srcdir@/tests|' \
		-e '\|^export SCRIPT_DIR=|s|$$|@abs_top_srcdir@/scripts|' \
		$(abs_top_srcdir)/scripts/common.sh.in >common.sh
	-echo "$$EXTRA_ENVIRONMENT" >>common.sh

clean-local:
	-$(RM) common.sh

install-data-hook:
	-$(SED) -e '\|^export BIN_DIR=|s|$$|@bindir@|' \
		-e '\|^export SBIN_DIR=|s|$$|@sbindir@|' \
		-e '\|^export ZTS_DIR=|s|$$|@datadir@/@PACKAGE@|' \
		-e '\|^export SCRIPT_DIR=|s|$$|@datadir@/@PACKAGE@|' \
		$(abs_top_srcdir)/scripts/common.sh.in \
		>$(DESTDIR)$(datadir)/@PACKAGE@/common.sh
