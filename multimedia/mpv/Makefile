# $OpenBSD: Makefile,v 1.22 2016/01/12 09:09:57 czarkoff Exp $

# archs with atomic ops
ONLY_FOR_ARCHS =	alpha amd64 i386 mips64 mips64el powerpc sparc64

COMMENT =		movie player based on MPlayer/mplayer2

GH_ACCOUNT =		mpv-player
GH_PROJECT =		mpv
GH_TAGNAME =		v0.16.0

GH_TAGNAME =
GH_COMMIT =		7caecc53b0b8ac1805fa498fb9dbe9379f3053d4
DISTNAME =		mpv-0.15.1

CATEGORIES =		multimedia x11

HOMEPAGE =		http://mpv.io/

MAINTAINER =		Dmitrij D. Czarkoff <czarkoff@openbsd.org>

WAF =			${WRKSRC}/waf-1.8.19
MASTER_SITES0 =		http://waf.io/
DISTFILES =		${DISTNAME}{${GH_COMMIT}}${EXTRACT_SUFX} ${WAF:T}:0
EXTRACT_ONLY =		${DISTNAME}${EXTRACT_SUFX}

# GPLv2+
PERMIT_PACKAGE_CDROM =	patents
PERMIT_PACKAGE_FTP =	Yes

WANTLIB += EGL GL SDL2 X11 X11-xcb Xau Xdamage Xdmcp Xext Xfixes
WANTLIB += Xinerama Xrandr Xrender Xss Xv Xxf86vm ass avcodec
WANTLIB += avdevice avfilter avformat avresample avutil bluray
WANTLIB += c cdio cdio_cdda cdio_paranoia drm dvdnav dvdread expat
WANTLIB += fontconfig freetype fribidi lcms2 m opus postproc pthread
WANTLIB += pthread-stubs smbclient sndio speex swresample swscale
WANTLIB += v4l2 v4lconvert vpx x264 x265 xcb xcb-dri2 xcb-glx
WANTLIB += z ${MODLUA_WANTLIB}

MODULES =		converters/libiconv \
			lang/lua \
			lang/python

BUILD_DEPENDS =		audio/ladspa \
			graphics/libmng \
			textproc/py-docutils

LIB_DEPENDS =		audio/libcdio \
			devel/libdvdread \
			devel/sdl2 \
			graphics/ffmpeg>=20151112 \
			graphics/lcms2 \
			multimedia/libass \
			multimedia/libbluray>=0.8.0 \
			multimedia/libdvdnav \
			multimedia/libv4l \
			net/samba
#			graphics/jpeg \

MODPY_RUNDEP ?=		No
RUN_DEPENDS =		devel/desktop-file-utils \
			x11/gtk+3,-guic

CONFIGURE_ARGS =	--confloaddir=${SYSCONFDIR}/mpv \
			--confdir=${LOCALBASE}/share/examples/mpv \
			--mandir=${LOCALBASE}/man \
			--docdir=${LOCALBASE}/share/examples/mpv \
			--zshdir=${LOCALBASE}/share/zsh/vendor-completions \
			--enable-sndio \
			--enable-sdl2 \
			--enable-zsh-comp \
			--disable-alsa \
			--disable-caca \
			--disable-dxva2-hwaccel \
			--disable-enca \
			--disable-gpl3 \
			--disable-jack \
			--disable-libarchive \
			--disable-libguess \
			--disable-rubberband \
			--disable-oss-audio \
			--disable-openal \
			--disable-optimize \
			--disable-pulse \
			--disable-rsound \
			--disable-uchardet \
			--disable-vaapi \
			--disable-vaapi-glx \
			--disable-vaapi-hwaccel \
			--disable-vaapi-x-egl \
			--disable-vaapi-x11 \
			--disable-vaapi-wayland \
			--disable-vapoursynth \
			--disable-vapoursynth-lazy \
			--disable-vdpau \
			--disable-vdpau-hwaccel \
			--disable-videotoolbox-hwaccel \
			--disable-videotoolbox-gl \
			--disable-wayland

MAKE_FLAGS =		-o "${WRKBUILD}" -t "${WRKSRC}" --destdir="${DESTDIR}"

USE_GROFF =		Yes
NO_TEST =		Yes

.if ${MACHINE_ARCH} == "i386"
CFLAGS +=		-march=i586
.endif

do-configure:
	cp ${DISTDIR}/${WAF:T} ${WAF}
	cd ${WRKSRC} && ${SETENV} ${MAKE_ENV} ${MODPY_BIN} ${WAF} \
				${MAKE_FLAGS} configure ${CONFIGURE_ARGS}

do-build:
	cd ${WRKSRC} && ${SETENV} ${MAKE_ENV} ${MODPY_BIN} ${WAF} \
				${MAKE_FLAGS} build -v

do-install:
	cd ${WRKSRC} && ${SETENV} ${MAKE_ENV} ${MODPY_BIN} ${WAF} \
				${MAKE_FLAGS} install
	${INSTALL_DATA} ${WRKDIST}/TOOLS/mpv_identify.sh \
	                ${WRKDIST}/TOOLS/umpv \
	                	${PREFIX}/share/examples/mpv
	${MODPY_BIN_ADJ} ${PREFIX}/share/examples/mpv/umpv
	sed -Ei 's,(/dev/dvd|/dev/cdrom),/dev/rcd0c,g' ${PREFIX}/man/man1/mpv.1

.include <bsd.port.mk>
