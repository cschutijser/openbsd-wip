# $OpenBSD$

COMMENT =		installation and loading of content packages in KDE
DISTNAME =		kpackage-${VERSION}

SHARED_LIBS =		KF5Package		0.0

WANTLIB =  KF5Archive KF5ConfigCore KF5CoreAddons KF5I18n Qt5Core
WANTLIB += c m pthread

MODULES =		devel/gettext

BUILD_DEPENDS =		devel/kf5/kdoctools
RUN_DEPENDS =		devel/kf5/kdoctools

LIB_DEPENDS =		devel/kf5/karchive \
			devel/kf5/kconfig \
			devel/kf5/kcoreaddons \
			devel/kf5/ki18n

PORTHOME =		${WRKDIR}
TEST_IS_INTERACTIVE =	X11

.include <bsd.port.mk>
