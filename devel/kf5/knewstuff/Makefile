# $OpenBSD$

COMMENT =		KDE framework for sharing additional application data
DISTNAME =		knewstuff-${VERSION}

SHARED_LIBS =		KF5NewStuff		0.0

WANTLIB =  KF5Archive KF5Attica KF5Auth KF5Codecs KF5Completion
WANTLIB += KF5ConfigCore KF5ConfigGui KF5ConfigWidgets KF5CoreAddons
WANTLIB += KF5I18n KF5IconThemes KF5ItemViews KF5JobWidgets KF5KIOCore
WANTLIB += KF5KIOWidgets KF5Service KF5SonnetUi KF5TextWidgets
WANTLIB += KF5WidgetsAddons KF5XmlGui Qt5Core Qt5DBus Qt5Gui Qt5Network
WANTLIB += Qt5Widgets Qt5Xml m

MODULES =		devel/gettext

LIB_DEPENDS =		devel/kf5/karchive \
			devel/kf5/attica \
			devel/kf5/kcompletion \
			devel/kf5/kconfig \
			devel/kf5/kcoreaddons \
			devel/kf5/ki18n \
			devel/kf5/kiconthemes \
			devel/kf5/kitemviews \
			devel/kf5/kio \
			devel/kf5/kservice \
			devel/kf5/ktextwidgets \
			devel/kf5/kwidgetsaddons \
			devel/kf5/kxmlgui

PORTHOME =		${WRKDIR}
TEST_IS_INTERACTIVE =	X11

.include <bsd.port.mk>
