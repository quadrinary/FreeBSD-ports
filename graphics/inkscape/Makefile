# Created by: Alexander Nedotsukov <bland@FreeBSD.org>
# $FreeBSD$

PORTNAME=	inkscape
PORTVERSION=	0.92.2
PORTREVISION=	8
CATEGORIES=	graphics gnome
MASTER_SITES=	https://launchpadlibrarian.net/332184472/ \
		https://inkscape.org/en/gallery/item/11254/ \
		LOCAL/kwm

MAINTAINER=	gnome@FreeBSD.org
COMMENT=	Full featured open source SVG editor

LICENSE=	GPLv2+ GPLv3+ LGPL21 MPL11
LICENSE_COMB=	multi
LICENSE_FILE_GPLv2=	${WRKSRC}/GPL2.txt
LICENSE_FILE_GPLv3=	${WRKSRC}/GPL3.txt
LICENSE_FILE_LGPL21=	${WRKSRC}/LGPL2.1.txt

BUILD_DEPENDS=	${LOCALBASE}/include/boost/concept_check.hpp:devel/boost-libs
LIB_DEPENDS=	libpopt.so:devel/popt \
		libgc.so:devel/boehm-gc \
		libgsl.so:math/gsl \
		libgtkspell.so:textproc/gtkspell \
		liblcms2.so:graphics/lcms2 \
		libfontconfig.so:x11-fonts/fontconfig \
		libfreetype.so:print/freetype2 \
		libpotrace.so:graphics/libpotrace \
		libpng.so:graphics/png \
		libMagick++-6.so:graphics/ImageMagick
#aspell?

USE_GNOME=	gtkmm24 libxml2 libxslt
USES=		compiler:c++11-lib cmake cpe desktop-file-utils gnome \
		iconv:wchar_t jpeg pathfix pkgconfig python:2.7,build \
		shebangfix tar:bzip2
USE_XORG=	x11
INSTALLS_ICONS=	yes
CMAKE_ARGS+=	-DWITH_GNOME_VFS:BOOL=NO

SHEBANG_FILES=	cxxtest/cxxtestgen.pl share/extensions/*.p[lm] \
		share/extensions/*.py share/extensions/genpofiles.sh \
		fix-roff-punct

OPTIONS_DEFINE=	POPPLER VISIO CDR DBUS WPG
OPTIONS_DEFAULT=POPPLER VISIO CDR WPG
OPTIONS_SUB=	yes

CDR_DESC=		Support for CorelDRAW diagrams
CDR_CMAKE_BOOL=		WITH_LIBCDR
CDR_LIB_DEPENDS=	librevenge-stream-0.0.so:textproc/librevenge \
			libcdr-0.1.so:graphics/libcdr01

DBUS_CMAKE_BOOL=	WITH_DBUS
DBUS_LIB_DEPENDS=	libdbus-glib-1.so:devel/dbus-glib \
			libdbus-1.so:devel/dbus

#OPENMP_USES=		compiler:openmp
#OPENMP_USES_OFF=	compiler:c++11-lib
#OPENMP_CMAKE_BOOL=	WITH_OPENMP
CMAKE_ARGS+=		-DWITH_OPENMP:BOOL=NO

POPPLER_DESC=		PDF preview rendering
POPPLER_CMAKE_BOOL=	ENABLE_POPPLER ENABLE_POPPLER_CAIRO
POPPLER_LIB_DEPENDS=	libpoppler.so:graphics/poppler \
			libpoppler-glib.so:graphics/poppler-glib

VISIO_DESC=		Support for Microsoft Visio diagrams
VISIO_CMAKE_BOOL=	WITH_LIBVISIO
VISIO_LIB_DEPENDS=	librevenge-stream-0.0.so:textproc/librevenge \
			libvisio-0.1.so:textproc/libvisio01

WPG_DESC=		Support for WordPerfect graphics
WPG_CMAKE_BOOL=		WITH_LIBWPG
WPG_LIB_DEPENDS=	libwpg-0.3.so:graphics/libwpg03

# temporary until the build works for the !NLS case
USES+=			gettext
#NLS_CMAKE_BOOL=		WITH_NLS
#NLS_USES=		gettext

post-patch:
	@${REINPLACE_CMD} -e 's|COMMAND python|COMMAND ${PYTHON_VERSION}|g' \
		${WRKSRC}/share/*/CMakeLists.txt

.include <bsd.port.mk>
