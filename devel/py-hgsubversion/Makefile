# $OpenBSD$

COMMENT =		Subversion client Mercurial extension

MODPY_EGG_VERSION =	1.8.5
DISTNAME =		py-hgsubversion-${MODPY_EGG_VERSION}
CATEGORIES =		devel net

HOMEPAGE =		http://bitbucket.org/durin42/hgsubversion/overview/

MAINTAINER =		Dmitrij D. Czarkoff <czarkoff@openbsd.org>

# GPLv2
PERMIT_PACKAGE_CDROM =	Yes

MASTER_SITES =		https://bitbucket.org/durin42/hgsubversion/get/
DISTFILES =		${DISTNAME}{${MODPY_EGG_VERSION}}${EXTRACT_SUFX}

MODULES =		lang/python
MODPY_SETUPTOOLS =	Yes
RUN_DEPENDS =		devel/mercurial \
			devel/py-subvertpy
TEST_DEPENDS =		${RUN_DEPENDS} \
			devel/py-nose

# Instead of updating WRKDIST manually on every update, just move the directory
post-extract:
	@mv ${WRKDIR}/durin42-hgsubversion-???????????? ${WRKDIST}

do-test:
	cd ${WRKSRC} && ${MODPY_BIN} tests/run.py

.include <bsd.port.mk>
