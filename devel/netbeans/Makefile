# $OpenBSD: Makefile,v 1.28 2015/05/25 07:54:27 jasper Exp $

SHARED_ONLY=		Yes

COMMENT=		NetBeans Java IDE

V=			8.1
DISTNAME=		netbeans-${V}-201510222201
PKGNAME=		netbeans-${V}
CATEGORIES=		devel

HOMEPAGE=		https://www.netbeans.org/

MAINTAINER=		Daniel Dickman <daniel@openbsd.org>, \
			Rafael Sadowski <rafael@sizeofvoid.org>

# CDDL and GPLv2 dual-licensed
#
# See:
# https://netbeans.org/about/legal/index.html
PERMIT_PACKAGE_CDROM=	Yes

MASTER_SITES=		http://download.netbeans.org/netbeans/${V}/final/zip/
EXTRACT_SUFX=		.zip

MODULES=		java
MODJAVA_VER=		1.8+

RUN_DEPENDS=		java/javaPathHelper \
			devel/desktop-file-utils

NO_BUILD=		Yes
NO_TEST=		Yes

WRKDIST=		${WRKDIR}/netbeans

NB=			${PREFIX}/netbeans

do-install:
	${INSTALL_DATA_DIR} ${NB}
	@tar -czf - -C ${WRKDIR}/netbeans . | tar xzf - -C ${NB}
	@rm -rf ${NB}/profiler ${NB}/{ide,cnd,dlight}/bin \
		${NB}/platform/modules/lib/{i386,amd64,x86}
	@find ${NB} -name "*.dll" -o -name "*.exe" -o -name "*.cmd" \
		-o -name "*.bat" -o -name ".lastModified" \
		-o -name "*.orig" | xargs rm
	@${SUBST_CMD} -o ${BINOWN} -g ${BINGRP} -m ${BINMODE} -c \
		${FILESDIR}/netbeans \
		${PREFIX}/bin/netbeans
	@${INSTALL_DATA_DIR} ${PREFIX}/share/applications

.include <bsd.port.mk>
