# $OpenBSD$

COMMENT =		KDE framework for binding JavaScript object to QObjects
DISTNAME =		kjsembed-${VERSION}

SHARED_LIBS =		KF5JsEmbed		0.0

WANTLIB =  KF5I18n KF5JS Qt5Core Qt5Gui Qt5Svg Qt5Widgets Qt5Xml
WANTLIB += c m pthread

MODULES =		devel/gettext

BUILD_DEPENDS =		devel/kf5/kdoctools
RUN_DEPENDS =		devel/kf5/kdoctools

LIB_DEPENDS =		devel/kf5/ki18n \
			devel/kf5/kjs

IS_PORTING_AID =	Yes

.include <bsd.port.mk>
