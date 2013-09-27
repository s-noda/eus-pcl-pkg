# -*- mode: Makefile; -*-

OS_NAME = $(shell uname -s)
ARCH_NAME = $(shell uname -m)

SLSFX=.so
ifeq ($(OS_NAME), Darwin)
SLSFX=.dylib
endif

MK_SL_FLAG = -shared
ifeq ($(OS_NAME), Darwin)
MK_SL_FLAG = -dynamiclib -flat_namespace -undefined suppress
endif

PCL_VERSION=1.7

CFLAGS  = $(shell PKG_CONFIG_PATH=/usr/lib/pkgconfig pkg-config --cflags pcl_search-$(PCL_VERSION))
CFLAGS += $(shell PKG_CONFIG_PATH=/usr/lib/pkgconfig pkg-config --cflags pcl_segmentation-$(PCL_VERSION))
CFLAGS += $(shell PKG_CONFIG_PATH=/usr/lib/pkgconfig pkg-config --cflags pcl_io-$(PCL_VERSION))
CFLAGS += $(shell PKG_CONFIG_PATH=/usr/lib/pkgconfig pkg-config --cflags pcl_keypoints-$(PCL_VERSION))
CFLAGS += $(shell PKG_CONFIG_PATH=/usr/lib/pkgconfig pkg-config --cflags pcl_geometry-$(PCL_VERSION))
CFLAGS += $(shell PKG_CONFIG_PATH=/usr/lib/pkgconfig pkg-config --cflags pcl_common-$(PCL_VERSION))
CFLAGS += $(shell PKG_CONFIG_PATH=/usr/lib/pkgconfig pkg-config --cflags pcl_filters-$(PCL_VERSION))
CFLAGS += $(shell PKG_CONFIG_PATH=/usr/lib/pkgconfig pkg-config --cflags pcl_kdtree-$(PCL_VERSION))
CFLAGS += $(shell PKG_CONFIG_PATH=/usr/lib/pkgconfig pkg-config --cflags pcl_octree-$(PCL_VERSION))
CFLAGS += $(shell PKG_CONFIG_PATH=/usr/lib/pkgconfig pkg-config --cflags pcl_apps-$(PCL_VERSION))
CFLAGS += $(shell PKG_CONFIG_PATH=/usr/lib/pkgconfig pkg-config --cflags pcl_sample_consensus-$(PCL_VERSION))
CFLAGS += $(shell PKG_CONFIG_PATH=/usr/lib/pkgconfig pkg-config --cflags pcl_features-$(PCL_VERSION))
CFLAGS += $(shell PKG_CONFIG_PATH=/usr/lib/pkgconfig pkg-config --cflags pcl_surface-$(PCL_VERSION))
CFLAGS += $(shell PKG_CONFIG_PATH=/usr/lib/pkgconfig pkg-config --cflags pcl_registration-$(PCL_VERSION))
CFLAGS += $(shell PKG_CONFIG_PATH=/usr/lib/pkgconfig pkg-config --cflags pcl_visualization-$(PCL_VERSION))
CFLAGS += $(shell PKG_CONFIG_PATH=/usr/lib/pkgconfig pkg-config --cflags pcl_tracking-$(PCL_VERSION))
CFLAGS += $(shell PKG_CONFIG_PATH=/usr/lib/pkgconfig pkg-config --cflags eigen3)
CFLAGS += -I$(shell pwd)/include

LDFLAGS  = $(shell PKG_CONFIG_PATH=/usr/lib/pkgconfig pkg-config --libs pcl_search-$(PCL_VERSION))
#LDFLAGS += $(shell PKG_CONFIG_PATH=/usr/lib/pkgconfig pkg-config --libs pcl_segmentation-$(PCL_VERSION))
LDFLAGS += -lpcl_segmentation
#LDFLAGS += $(shell PKG_CONFIG_PATH=/usr/lib/pkgconfig pkg-config --libs pcl_io-$(PCL_VERSION))
LDFLAGS += -lpcl_io
LDFLAGS += $(shell PKG_CONFIG_PATH=/usr/lib/pkgconfig pkg-config --libs pcl_keypoints-$(PCL_VERSION))
LDFLAGS += $(shell PKG_CONFIG_PATH=/usr/lib/pkgconfig pkg-config --libs pcl_geometry-$(PCL_VERSION))
LDFLAGS += $(shell PKG_CONFIG_PATH=/usr/lib/pkgconfig pkg-config --libs pcl_common-$(PCL_VERSION))
LDFLAGS += $(shell PKG_CONFIG_PATH=/usr/lib/pkgconfig pkg-config --libs pcl_filters-$(PCL_VERSION))
LDFLAGS += $(shell PKG_CONFIG_PATH=/usr/lib/pkgconfig pkg-config --libs pcl_kdtree-$(PCL_VERSION))
LDFLAGS += $(shell PKG_CONFIG_PATH=/usr/lib/pkgconfig pkg-config --libs pcl_octree-$(PCL_VERSION))
LDFLAGS += $(shell PKG_CONFIG_PATH=/usr/lib/pkgconfig pkg-config --libs pcl_apps-$(PCL_VERSION))
LDFLAGS += $(shell PKG_CONFIG_PATH=/usr/lib/pkgconfig pkg-config --libs pcl_sample_consensus-$(PCL_VERSION))
LDFLAGS += $(shell PKG_CONFIG_PATH=/usr/lib/pkgconfig pkg-config --libs pcl_features-$(PCL_VERSION))
LDFLAGS += $(shell PKG_CONFIG_PATH=/usr/lib/pkgconfig pkg-config --libs pcl_surface-$(PCL_VERSION))
LDFLAGS += $(shell PKG_CONFIG_PATH=/usr/lib/pkgconfig pkg-config --libs pcl_registration-$(PCL_VERSION))
#LDFLAGS += $(shell PKG_CONFIG_PATH=/usr/lib/pkgconfig pkg-config --libs pcl_visualization-$(PCL_VERSION))
LDFLAGS += -lpcl_visualization
LDFLAGS += $(shell PKG_CONFIG_PATH=/usr/lib/pkgconfig pkg-config --libs pcl_tracking-$(PCL_VERSION))
LLDFLAGS = $(filter-out -lflann_cpp-gd, $(LDFLAGS))

EUSPCL_OBJS = src/euspcl_main.o src/euspcl_common.o src/euspcl_features.o src/euspcl_filters.o src/euspcl_io.o src/euspcl_octree.o src/euspcl_range_image.o src/euspcl_registration.o src/euspcl_sample_consensus.o src/euspcl_segmentation.o src/euspcl_surface.o src/euspcl_tracking.o src/euspcl_recognition.o

all: lib/eus_pcl$(SLSFX)

lib/eus_pcl$(SLSFX): $(EUSPCL_OBJS)
	echo ${LD_FLAGS}
	if [ ! -e lib ]; then mkdir -p lib; fi
	g++ -O2 $(MK_SL_FLAG) -fPIC  -o $@ $^ $(LLDFLAGS)

.cpp.o:
	g++ -O2 -fPIC -c $< -o $@ ${CFLAGS} -DLinux -D_REENTRANT -Dx86_64 -I${EUSDIR}/include -I${EUSDIR}/../irteus

clean:
	rm -f lib/*.so src/*.o
