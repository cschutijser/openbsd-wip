#	$OpenBSD$

COMMENT=	tool to analyse #includes in C and C++ source files
CATEGORIES=	devel
DISTNAME=	include-what-you-use-0.5.src
PKGNAME=	include-what-you-use-0.5
HOMEPAGE=	http://include-what-you-use.org
MASTER_SITES=	${HOMEPAGE}/downloads/
WRKDIST=	${WRKDIR}/include-what-you-use

# BSD
PERMIT_PACKAGE_CDROM=	Yes

WANTLIB=	c curses form m pthread z
BUILD_DEPENDS=	devel/llvm

MODULES=		devel/cmake gcc4 lang/python
MODGCC4_LANGS =		c++
MODGCC4_ARCHS =		*
CONFIGURE_ARGS=		-DLLVM_PATH=${LOCALBASE}

post-install:
	@perl -pi -e 's,/usr/bin/env python,/usr/bin/env python${MODPY_VERSION},g' \
		${PREFIX}/bin/{fix_includes,iwyu_tool}.py

.include <bsd.port.mk>
