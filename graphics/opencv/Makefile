# $OpenBSD: Makefile,v 1.34 2015/01/30 21:38:37 zhuk Exp $

ONLY_FOR_ARCHS =	amd64 i386
ONLY_FOR_ARCHS-java =	${ONLY_FOR_ARCHS}

CATEGORIES =		graphics devel
COMMENT-docs =		OpenCV documentation and examples
COMMENT-main =		library of programming functions for real time cv
COMMENT-java =		Java bindings for OpenCV

V =			3.0.0
DISTNAME =		opencv-${V}
PKGNAME-main =		${PKGNAME}
PKGNAME-docs =		opencv-docs-$V
PKGNAME-java =		opencv-java-${V}

HOMEPAGE =		http://www.opencv.org/
MAINTAINER =		Rafael Sadowski <rafael@sizeofvoid.org>

SHARED_LIBS =		opencv_calib3d			2.0 #1.1
SHARED_LIBS +=		opencv_core			2.0 #1.1
SHARED_LIBS +=		opencv_features2d		2.0 #1.1
SHARED_LIBS +=		opencv_flann			2.0 #1.1
SHARED_LIBS +=		opencv_highgui			2.0 #1.1
SHARED_LIBS +=		opencv_imgcodecs		0.0 #1.0
SHARED_LIBS +=		opencv_imgproc			2.0 #1.1
SHARED_LIBS +=		opencv_ml			2.0 #1.1
SHARED_LIBS +=		opencv_objdetect		2.0 #1.1
SHARED_LIBS +=		opencv_photo			1.0 #0.1
SHARED_LIBS +=		opencv_shape			0.0 #1.0
SHARED_LIBS +=		opencv_stitching		0.0 #1.0
SHARED_LIBS +=		opencv_superres			1.0 #0.1
SHARED_LIBS +=		opencv_video			2.0 #1.1
SHARED_LIBS +=		opencv_videoio			0.0 #1.0
SHARED_LIBS +=		opencv_videostab		1.0 #0.1

EXTRACT_SUFX =		.zip
MASTER_SITES =		${MASTER_SITE_SOURCEFORGE:=opencvlibrary/}

WANTLIB-main =  Half Iex IlmImf IlmThread Imath X11 Xcomposite Xcursor
WANTLIB-main += Xdamage Xext Xfixes Xi Xinerama Xrandr Xrender atk-1.0
WANTLIB-main += avcodec avformat avutil bz2 c cairo fontconfig intl
WANTLIB-main += freetype gdk_pixbuf-2.0 gio-2.0 glib-2.0
WANTLIB-main += gobject-2.0 gstapp-1.0 gstbase-1.0 gstpbutils-1.0
WANTLIB-main += avresample cairo-gobject gdk-3 gtk-3
WANTLIB-main += gstreamer-1.0 gstriff-1.0 gstvideo-1.0 gthread-2.0
WANTLIB-main += jasper jpeg m pango-1.0 pangocairo-1.0
WANTLIB-main += pangoft2-1.0 png pthread stdc++ swscale tiff xml2 z
WANTLIB-main += ${MODGETTEXT_WANTLIB} ${MODPY_WANTLIB}

WANTLIB-docs =

WANTLIB-java =  m pthread stdc++
WANTLIB-java += opencv_calib3d>=2.0 opencv_core>=2.0 opencv_features2d>=2.0 opencv_flann>=2.0
WANTLIB-java += opencv_highgui>=2.0 opencv_imgproc>=2.0 opencv_ml>=2.0 opencv_objdetect>=2.0
WANTLIB-java += opencv_photo>=1.0 opencv_video>=2.0 opencv_imgcodecs opencv_videoio

MULTI_PACKAGES =	-main -docs -java
PSEUDO_FLAVORS =	no_docs no_java
FLAVOR ?=

# BSDL
PERMIT_PACKAGE_CDROM =	Yes

.include <bsd.port.arch.mk>

MODULES =		lang/clang \
			devel/cmake \
			devel/gettext \
			lang/python

MODCLANG_ARCHS =	amd64 i386
MODCLANG_LANGS =	c c++

MODPY_VERSION =		${MODPY_DEFAULT_VERSION_2}

BUILD_DEPENDS =		devel/doxygen>=1.8.10 \
			math/py-numpy \
			math/eigen3

RUN_DEPENDS-main =	math/py-numpy
RUN_DEPENDS-docs =	${BUILD_PKGPATH},-main
RUN_DEPENDS-java =	${MODJAVA_RUN_DEPENDS}

LIB_DEPENDS-main =	${LIB_DEPENDS} \
			${MODPY_LIB_DEPENDS} \
			multimedia/gstreamer1/plugins-base \
			x11/gtk+3 \
			graphics/ffmpeg \
			graphics/ilmbase \
			graphics/jpeg \
			graphics/openexr \
			graphics/png \
			graphics/tiff

LIB_DEPENDS-java =	${BUILD_PKGPATH},-main=${V}

# XXX PIE cannot be produced due to problems with inline assembly.
# Since OpenCV is mostly used as a LIBrary, switch to PIC.
.if ${ARCH:Mi386}
CONFIGURE_ENV =		CFLAGS="${CFLAGS} -fPIC" \
			CXXFLAGS="${CXXFLAGS} -fPIC"
.endif

# ATM opencv requires V4L1 compat, ask them to change it,
# then see WITH_V4L below.
CONFIGURE_ARGS =	-DWITH_1394:Bool=Off \
			-DWITH_VTK:Bool=Off \
			-DWITH_CUDA:Bool=Off \
			-DWITH_CUFFT:Bool=Off \
			-DWITH_EIGEN:Bool=Off \
			-DWITH_V4L:Bool=Off \
			-DWITH_LIBV4L:Bool=Off \
			-DWITH_IPP:Bool=Off \
			-DWITH_OPENCL:Bool=Off \
			-DWITH_OPENCLAMDFFT:Bool=Off \
			-DWITH_OPENCLAMDBLAS:Bool=Off \
			-DBUILD_TESTS:Bool=On \
			-DPYTHON_EXECUTABLE:FILEPATH=${MODPY_BIN}

.if ${BUILD_PACKAGES:M-docs}
BUILD_DEPENDS +=	textproc/py-sphinx
ALL_TARGET =		all doxygen
CONFIGURE_ARGS +=	-DBUILD_DOCS:Bool=On \
			-DBUILD_EXAMPLES:Bool=On \
			-DINSTALL_C_EXAMPLES:Bool=On \
			-DINSTALL_PYTHON_EXAMPLES:Bool=On
.else
CONFIGURE_ARGS +=	-DBUILD_DOCS:Bool=Off \
			-DBUILD_EXAMPLES:Bool=Off \
			-DINSTALL_PYTHON_EXAMPLES:Bool=Off
.endif

.if ${BUILD_PACKAGES:M-java}
MODULES +=		java
MODJAVA_VER =		1.7+
BUILD_DEPENDS +=	devel/apache-ant
.else
# Safe: Java will be detected, if present, but won't be used
CONFIGURE_ARGS +=	-DBUILD_opencv_java:Bool=Off
.endif

CONFIG_ADJ_CMD =	perl -pi
.for _l _v in ${SHARED_LIBS}
CONFIG_ADJ_CMD +=	-e 's,lib${_l}.so([^.]),lib${_l}.so.${_v}$$1,g;'
.endfor

post-patch:
	# remove BOM (byte order mark)
	find ${WRKSRC} -type f \( -name "*.cpp" -or -name \
		"*.h" -or -name "*.hpp" \) -exec perl -CD -pi -e 'tr/\x{feff}//d' \
		"{}" \;

post-install:
	${CONFIG_ADJ_CMD} ${PREFIX}/share/OpenCV/OpenCVConfig.cmake
	${MODPY_BIN} ${MODPY_LIBDIR}/compileall.py ${WRKINST}${MODPY_SITEPKG}

do-test:
	cd ${WRKBUILD}; \
	${MODPY_BIN} ${WRKSRC}/modules/ts/misc/run.py

.include <bsd.port.mk>
