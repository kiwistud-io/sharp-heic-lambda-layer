# Library Versions
WEBP_VERSION=1.2.4
LIBDE265_VERSION=1.0.8
LIBHEIF_VERSION=1.12.0
VIPS_VERSION=8.12.2
SHARP_VERSION=0.30.7

PREFIX_PATH=/opt

export PKG_CONFIG_PATH=$(PREFIX_PATH)/lib/pkgconfig

# Install and enable the EPEL RPM package on Amazon Linux 2
yum install https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm

# Install the RPM Fusion configuration package
yum install https://download1.rpmfusion.org/free/el/rpmfusion-free-release-7.noarch.rpm

# Install the Remi repository configuration package
yum install http://rpms.remirepo.net/enterprise/remi-release-7.rpm

# Install the yum-utils package (for the yum-config-manager command)
yum install yum-utils

# Enable Remi's RPM repository
yum-config-manager --enable remi

# Install libvips with HEIC support (+ development files and command-line tools)
yum install vips vips-heif vips-devel vips-tools

build-SharpHEICLayer: libvips
	mkdir -p "$(ARTIFACTS_DIR)/nodejs"
	mkdir -p "$(ARTIFACTS_DIR)/lib"

	# sharp uses several of the libs we installed or compiled. extract the full list and copy all of those into /opt/lib
	# extract list with ldd from sharp.node, manipulate a bit with sed to only get the absolute paths, then copy
	LD_LIBRARY_PATH=$(PREFIX_PATH)/lib npm --prefix "$(ARTIFACTS_DIR)/nodejs/" install sharp@$(SHARP_VERSION)
	LD_LIBRARY_PATH=$(PREFIX_PATH)/lib ldd $(ARTIFACTS_DIR)/nodejs/node_modules/sharp/build/Release/sharp-linux-x64.node | sed -nE "s/^[^\/\n]*(\/[^ ]+)(.*)/\1/p" | xargs cp -t $(ARTIFACTS_DIR)/lib

# libwebp:
# 	curl -L https://github.com/webmproject/libwebp/archive/v$(WEBP_VERSION).tar.gz | tar zx
# 	cd libwebp-$(WEBP_VERSION) && ./autogen.sh && ./configure --enable-libwebpmux --prefix=$(PREFIX_PATH) && make V=0 && make install
#
# x265:
# 	yum install -y mercurial
# 	yum install -y cmake
# 	hg clone http://hg.videolan.org/x265
# 	cd ./x265/build/linux && \
# 		cmake -G "Unix Makefiles" -DCMAKE_INSTALL_PREFIX=$(PREFIX_PATH) ../../source && \
# 		make && \
# 		make install
#
#
# libde265: x265
# 	# libde265
# 	curl -L https://github.com/strukturag/libde265/releases/download/v$(LIBDE265_VERSION)/libde265-$(LIBDE265_VERSION).tar.gz | tar zx
# 	cd libde265-$(LIBDE265_VERSION) && ./autogen.sh && ./configure --disable-dec265 --disable-sherlock265 --prefix=$(PREFIX_PATH) && make V=0 && make install
#
# libheif: libde265 x265
# 	# libheif
# 	curl -L https://github.com/strukturag/libheif/releases/download/v$(LIBHEIF_VERSION)/libheif-$(LIBHEIF_VERSION).tar.gz | tar zx
# 	cd libheif-$(LIBHEIF_VERSION) && ./autogen.sh && ./configure --prefix=$(PREFIX_PATH) && make V=0 && make install

libvips:
    # Install and enable the EPEL RPM package on Amazon Linux 2
    yum install -y https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm

    # Install the RPM Fusion configuration package
    yum install -y https://download1.rpmfusion.org/free/el/rpmfusion-free-release-7.noarch.rpm

    # Install the Remi repository configuration package
    yum install -y http://rpms.remirepo.net/enterprise/remi-release-7.rpm

    # Install the yum-utils package (for the yum-config-manager command)
    yum install -y yum-utils

    # Enable Remi's RPM repository
    yum-config-manager --enable remi

    # Install libvips with HEIC support (+ development files and command-line tools)
    yum install -y vips vips-heif vips-devel vips-tools



# installLib:
# 	yum install -y yum-plugin-ovl && \
# 	yum install -y \
# 		glib2-devel \
# 		expat-devel \
# 		libjpeg-devel \
# 		libjpeg-turbo-devel \
# 		libpng-devel \
# 		giflib-devel \
# 		libexif-devel \
# 		librsvg2-devel \
# 		libtiff-devel
