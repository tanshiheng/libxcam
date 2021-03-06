SUBDIRS = interface

plugin_LTLIBRARIES = \
    $(NULL)

if ENABLE_IA_AIQ
plugin_LTLIBRARIES += \
    libgstxcamsrc.la  \
    $(NULL)
endif

if HAVE_LIBCL
plugin_LTLIBRARIES += \
    libgstxcamfilter.la  \
    $(NULL)
endif

XCORE_DIR = $(top_builddir)/xcore
XCORE_LA = $(top_builddir)/xcore/libxcam_core.la

ISP_DIR = $(top_builddir)/modules/isp
ISP_LA = $(top_builddir)/modules/isp/libxcam_isp.la

if HAVE_LIBCL
OCL_DIR = $(top_builddir)/modules/ocl
OCL_LA = $(top_builddir)/modules/ocl/libxcam_ocl.la
else
OCL_DIR =
OCL_LA =
endif

PTHREAD_LDFLAGS = -pthread

XCAMGST_CXXFLAGS = $(XCAM_CXXFLAGS)
XCAMGST_LIBS = \
    $(NULL)

if HAVE_LIBDRM
XCAMGST_CXXFLAGS += $(LIBDRM_CFLAGS)
XCAMGST_LIBS += $(LIBDRM_LIBS)
endif

if USE_LOCAL_ATOMISP
XCAMGST_CXXFLAGS += \
    -I$(top_srcdir)/ext/atomisp \
    $(NULL)
endif

# Note: plugindir is set in configure
plugindir="$(libdir)/gstreamer-1.0"

if ENABLE_IA_AIQ
# sources used to compile this plug-in
libgstxcamsrc_la_SOURCES = \
    gstxcambuffermeta.cpp  \
    gstxcambufferpool.cpp  \
    main_dev_manager.cpp   \
    gstxcamsrc.cpp         \
    $(NULL)

# compiler and linker flags used to compile this plugin, set in configure.ac
libgstxcamsrc_la_CXXFLAGS = \
    $(GST_CFLAGS) $(XCAMGST_CXXFLAGS)              \
    -I$(XCORE_DIR) -I$(ISP_DIR) -I$(OCL_DIR)       \
    -I$(top_builddir)/wrapper/gstreamer            \
    -I$(top_builddir)/wrapper/gstreamer/interface  \
    $(NULL)

libgstxcamsrc_la_LIBADD = $(XCAMGST_LIBS)  \
    $(top_builddir)/wrapper/gstreamer/interface/libgstxcaminterface.la  \
    $(XCORE_LA) $(ISP_LA) $(OCL_LA)        \
    $(GST_ALLOCATOR_LIBS)                  \
    $(GST_VIDEO_LIBS)                      \
    $(GST_LIBS)                            \
    $(NULL)

libgstxcamsrc_la_LDFLAGS = \
    -module -avoid-version           \
    $(PTHREAD_LDFLAGS)               \
    $(XCORE_LA) $(ISP_LA) $(OCL_LA)  \
    $(NULL)

libgstxcamsrc_la_LIBTOOLFLAGS = --tag=disable-static
endif

if HAVE_LIBCL
libgstxcamfilter_la_SOURCES = \
    gstxcambuffermeta.cpp  \
    main_pipe_manager.cpp  \
    gstxcamfilter.cpp      \
    $(NULL)

libgstxcamfilter_la_CXXFLAGS = \
    $(GST_CFLAGS) $(XCAMGST_CXXFLAGS)    \
    -I$(XCORE_DIR) -I$(OCL_DIR)          \
    -I$(top_builddir)/wrapper/gstreamer  \
    $(NULL)

libgstxcamfilter_la_LIBADD = \
    $(XCAMGST_LIBS)        \
    $(XCORE_LA) $(OCL_LA)  \
    $(GST_ALLOCATOR_LIBS)  \
    $(GST_VIDEO_LIBS)      \
    $(GST_LIBS)            \
    $(NULL)

libgstxcamfilter_la_LDFLAGS = \
    -module -avoid-version    \
    $(XCORE_LA) $(OCL_LA)     \
    $(NULL)

libgstxcamfilter_la_LIBTOOLFLAGS = --tag=disable-static
endif

# headers we need but don't want installed
noinst_HEADERS = \
    $(NULL)

if ENABLE_IA_AIQ
noinst_HEADERS += \
    gstxcambufferpool.h  \
    gstxcambuffermeta.h  \
    main_dev_manager.h   \
    gstxcamsrc.h         \
    $(NULL)
endif

if HAVE_LIBCL
noinst_HEADERS += \
    gstxcambuffermeta.h  \
    main_pipe_manager.h  \
    gstxcamfilter.h      \
    $(NULL)
endif
