# Created by: vanilla@
# $FreeBSD$

PORTNAME=	protobuf
PORTVERSION=	3.12.4
PORTEPOCH=	1
CATEGORIES=	devel python
MASTER_SITES=	CHEESESHOP
PKGNAMEPREFIX=	${PYTHON_PKGNAMEPREFIX}

MAINTAINER=	sunpoet@FreeBSD.org
COMMENT=	Google protobuf Python Client Library

LICENSE=	BSD3CLAUSE

BUILD_DEPENDS=	protoc:devel/protobuf \
		${PYTHON_PKGNAMEPREFIX}wheel>=0:devel/py-wheel@${PY_FLAVOR}
RUN_DEPENDS=	${PYTHON_PKGNAMEPREFIX}six>=1.9:devel/py-six@${PY_FLAVOR}

USES=		python
USE_PYTHON=	autoplist concurrent distutils

DO_MAKE_TEST=	${PYTHON_CMD} ${PYDISTUTILS_SETUP}
NO_ARCH=	yes
TEST_TARGET=	test

.include <bsd.port.mk>
