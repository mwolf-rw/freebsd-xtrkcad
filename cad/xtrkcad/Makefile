# $FreeBSD$

PORTNAME=	xtrkcad
DISTVERSION=	5.1.2
DISTVERSIONPREFIX=	source-
DISTVERSIONSUFFIX=	a
CATEGORIES=	cad
MASTER_SITES=	SF/xtrkcad-fork/XTrackCad/Version%20${DISTVERSION}

MAINTAINER=	freebsd@rheinwolf.de
COMMENT=	XTrackCAD is a CAD program for designing model railroad layouts

LICENSE=	GPLv2

OPTIONS_DEFINE=	DOCS EXAMPLES NLS
OPTIONS_SUB=	NLS

DOCS_BUILD_DEPENDS=	pandoc:textproc/hs-pandoc

NLS_VARS=	USES+=gettext-runtime:lib \
		USES+=gettext-tools:build
NLS_CMAKE_ON=	XTRKCAD_USE_GETTEXT

LIB_DEPENDS=	libcmocka.so:sysutils/cmocka \
		libfontconfig.so:x11-fonts/fontconfig \
		libfreetype.so:print/freetype2 \
		libsoup-2.4.so:devel/libsoup \
		libwebkitgtk-1.0.so:www/webkit-gtk2
BUILD_DEPENDS=	pkg-config:devel/pkgconf

USES=		cmake gnome
USE_GNOME=	gdkpixbuf2 gtk20 cairo
CMAKE_ON=	XTRKCAD_USE_GTK
CMAKE_OFF=	XTRKCAD_TESTING

post-install:
	${MKDIR} ${STAGEDIR}${DESKTOPDIR} \
		 ${STAGEDIR}${DOCSDIR} \
		 ${STAGEDIR}${EXAMPLESDIR} \
		 ${STAGEDIR}${PREFIX}/share/pixmaps
	${RM} ${STAGEDIR}${DATADIR}/COPYING
	${MV} ${STAGEDIR}/usr/share/applications/xtrkcad.desktop ${STAGEDIR}${DESKTOPDIR}
	${MV} ${STAGEDIR}/usr/share/pixmaps/xtrkcad.png ${STAGEDIR}${PREFIX}/share/pixmaps
	${MV} ${STAGEDIR}${DATADIR}/CHANGELOG.txt ${STAGEDIR}${DOCSDIR}
	${MV} ${STAGEDIR}${DATADIR}/Readme.txt ${STAGEDIR}${DOCSDIR}
	${MV} ${STAGEDIR}${DATADIR}/examples/* ${STAGEDIR}${EXAMPLESDIR}

.include <bsd.port.mk>
