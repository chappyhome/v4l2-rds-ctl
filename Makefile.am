AUTOMAKE_OPTIONS = foreign
ACLOCAL_AMFLAGS = -I m4

SUBDIRS = \
	lib/libv4lconvert \
	lib/libv4l2 \
	lib/libv4l1 \
	lib/libdvbv5 \
	lib/libv4l2rds

if WITH_V4LUTILS
SUBDIRS += \
	utils/dvb \
	utils/libv4l2util \
	utils/libmedia_dev \
	utils/decode_tm6000 \
	utils/keytable \
	utils/v4l2-compliance \
	utils/v4l2-ctl \
	utils/v4l2-dbg \
	utils/v4l2-sysfs-path \
	utils/rds-ctl

if LINUX_OS
SUBDIRS += \
	utils/xc3028-firmware \
	contrib/test

if HAVE_LINUX_I2C_DEV
SUBDIRS += \
	utils/rds
endif
endif

if WITH_QV4L2
SUBDIRS += utils/qv4l2
endif
endif

EXTRA_DIST = contrib include README.lib README.lib-multi-threading

# custom targets

sync-with-kernel:
	@if [ ! -f $(KERNEL_DIR)/include/linux/videodev2.h -o \
	      ! -f $(KERNEL_DIR)/include/linux/v4l2-common.h -o \
	      ! -f $(KERNEL_DIR)/include/linux/ivtv.h -o \
	      ! -f $(KERNEL_DIR)/include/media/v4l2-chip-ident.h ]; then \
	  echo "Error you must set KERNEL_DIR to point to an extracted kernel source dir"; \
	  exit 1; \
	fi
	cp -a $(KERNEL_DIR)/include/linux/videodev2.h $(top_srcdir)/include/linux
	cp -a $(KERNEL_DIR)/include/linux/v4l2-common.h $(top_srcdir)/include/linux
	cp -a $(KERNEL_DIR)/include/linux/ivtv.h $(top_srcdir)/include/linux
	cp -a $(KERNEL_DIR)/include/media/v4l2-chip-ident.h $(top_srcdir)/include/media

	$(MAKE) -C utils/keytable $@
	$(MAKE) -C utils/v4l2-dbg $@
	$(MAKE) -C utils/xc3028-firmware $@
	$(MAKE) -C lib/libdvbv5 $@
	$(MAKE) -C contrib/freebsd $@

