# $OpenBSD: Makefile,v 1.16 2015/03/27 08:11:27 ajacoutot Exp $

BROKEN-powerpc =	error: invalid 'asm': invalid %k value
BROKEN-alpha =		error: invalid 'asm': invalid %xn code
BROKEN-sparc64 =	error: invalid 'asm': invalid operand output code

COMMENT =		modern Amiga emulator
V =			2.6.2
MODPY_EGG_VERSION =	${V}
DISTNAME =		fs-uae-$V
CATEGORIES =		emulators

HOMEPAGE =		http://fengestad.no/fs-uae/
MAINTAINER =		Edd Barrett <edd@openbsd.org>

# GPLv2, LGPLv2.1, BSD
PERMIT_PACKAGE_CDROM =	Yes

WANTLIB += GL GLEW GLU SDL2 X11 c freetype glib-2.0 gthread-2.0 m mpeg2
WANTLIB += mpeg2convert openal png pthread stdc++ z

MASTER_SITES =		${HOMEPAGE}stable/$V/

MODULES =		devel/gettext
LIB_DEPENDS =		devel/sdl2 \
			graphics/png \
			audio/openal \
			devel/glib2 \
			graphics/libmpeg2 \
			graphics/glew
RUN_DEPENDS =		devel/desktop-file-utils \
			x11/gtk+3,-guic

BUILD_DEPENDS =	${MODGNU_AUTOCONF_DEPENDS} \
		${MODGNU_AUTOMAKE_DEPENDS}
AUTOCONF_VERSION =      2.69
AUTOMAKE_VERSION =      1.15

CONFIGURE_STYLE =	gnu
USE_GMAKE =		Yes

NO_TEST =		Yes

post-patch:
	cd ${WRKSRC} && env AUTOCONF_VERSION=${AUTOCONF_VERSION} \
		AUTOMAKE_VERSION=${AUTOMAKE_VERSION} \
		${LOCALBASE}/bin/autoreconf -fi

.include <bsd.port.mk>
