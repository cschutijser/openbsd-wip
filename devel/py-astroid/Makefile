# $OpenBSD: Makefile,v 1.11 2013/07/01 10:39:18 sthen Exp $

COMMENT =		common base representation of Python source code

MODPY_EGG_VERSION =	1.4.4
DISTNAME =		astroid-${MODPY_EGG_VERSION}
PKGNAME =		py-${DISTNAME}
CATEGORIES =		devel

HOMEPAGE =		http://www.astroid.org/

MAINTAINER =		Alexandr Shadchin <shadchin@openbsd.org>

# LGPLv2.1+
PERMIT_PACKAGE_CDROM =	Yes

MODULES =		lang/python

MODPY_PI =		Yes
MODPY_SETUPTOOLS =	Yes

RUN_DEPENDS =		devel/py-logilab-common${MODPY_FLAVOR} \
			devel/py-lazy-object-proxy${MODPY_FLAVOR} \
			devel/py-six${MODPY_FLAVOR} \
			devel/py-wrapt${MODPY_FLAVOR}
TEST_DEPENDS =		${RUN_DEPENDS}

FLAVORS =	python3
FLAVOR ?=

do-test:
	@cd ${WRKSRC} && \
	    ${MODPY_BIN} -m unittest discover -p "unittest*.py"

.include <bsd.port.mk>
