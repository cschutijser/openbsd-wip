# $OpenBSD: Makefile.template,v 1.61 2012/03/29 13:41:58 sthen Exp $

COMMENT =		Gnu All Mobile Management Utilities GUI

MODPY_EGG_VERSION = 	0.40
DISTNAME =		wammu-${MODPY_EGG_VERSION}

CATEGORIES =		comms x11

HOMEPAGE =		http://wammu.eu/

MAINTAINER =		Kirill Bychkov <kirby@openbsd.org>

# GPLv2
PERMIT_PACKAGE_CDROM =	Yes

MASTER_SITES =		http://dl.cihar.com/wammu/v0/

MODULES =		lang/python

RUN_DEPENDS =		comms/py-gammu \
			devel/desktop-file-utils \
			devel/gettext \
			x11/py-wxPython

NO_TEST = 		Yes
NO_BUILD = 		Yes

PKG_ARCH = 		*

.include <bsd.port.mk>
