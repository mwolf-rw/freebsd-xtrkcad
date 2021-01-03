# $FreeBSD$

PORTNAME=	xtrkcad
PORTVERSION=	5.2.1a
CATEGORIES=	cad
MASTER_SITES=	https://sourceforge.net/code-snapshots/hg/x/xt/xtrkcad-fork/xtrkcad/
DISTNAME=	${PORTNAME}-fork-${PORTNAME}-${SF_COMMIT}

MAINTAINER=	freebsd@rheinwolf.de
COMMENT=	CAD program for designing model railroad layouts

LICENSE=	GPLv2
LICENSE_FILE=	${WRKSRC}/app/COPYING

LIB_DEPENDS=	libfontconfig.so:x11-fonts/fontconfig \
		libfreetype.so:print/freetype2 \
		libzip.so:archivers/libzip
BUILD_DEPENDS=	pkg-config:devel/pkgconf

USES=		cmake gnome zip
USE_GNOME=	gdkpixbuf2 gtk20 cairo

SF_COMMIT=	31686443927091c46337f73245750acb05d4e3bb

CMAKE_ARGS=	-Wno-dev
CMAKE_ON=	XTRKCAD_USE_GTK XTRKCAD_USE_BROWSER
CMAKE_OFF=	XTRKCAD_TESTING

OPTIONS_DEFINE=	DOCS EXAMPLES NLS
OPTIONS_SUB=	NLS

DOCS_BUILD_DEPENDS=	pandoc:textproc/hs-pandoc

NLS_USES=	gettext-runtime:lib gettext-tools:build
NLS_CMAKE_BOOL=	XTRKCAD_USE_GETTEXT

post-install:
	${MKDIR} ${STAGEDIR}${DESKTOPDIR} \
		 ${STAGEDIR}${DOCSDIR} \
		 ${STAGEDIR}${EXAMPLESDIR} \
		 ${STAGEDIR}${PREFIX}/share/pixmaps
	${MV} ${STAGEDIR}${DATADIR}/applications/xtrkcad.desktop ${STAGEDIR}${DESKTOPDIR}
	${MV} ${STAGEDIR}${DATADIR}/pixmaps/xtrkcad.png ${STAGEDIR}${PREFIX}/share/pixmaps
	${RM} ${STAGEDIR}${DATADIR}/COPYING

post-install-DOCS-on:
	${MV} ${STAGEDIR}${DATADIR}/CHANGELOG.txt ${STAGEDIR}${DOCSDIR}
	${MV} ${STAGEDIR}${DATADIR}/Readme.txt ${STAGEDIR}${DOCSDIR}

post-install-DOCS-off:
	${RM} ${STAGEDIR}${DATADIR}/*.txt

post-install-EXAMPLES-on:
	${MV} ${STAGEDIR}${DATADIR}/examples/* ${STAGEDIR}${EXAMPLESDIR}
	${RMDIR} ${STAGEDIR}${DATADIR}/examples

post-install-EXAMPLES-off:
	${RM} -rf ${STAGEDIR}${DATADIR}/examples

.include <bsd.port.mk>
