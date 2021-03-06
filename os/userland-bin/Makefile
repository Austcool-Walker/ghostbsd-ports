# $FreeBSD$

PORTNAME=	userland-bin
PORTVERSION=	${BASEPKG_PORTVERSION}
CATEGORIES=	os
PKGNAMEPREFIX=	${OS_PKGNAMEPREFIX}
DISTFILES=
EXTRACT_ONLY=

MAINTAINER=	kmoore@FreeBSD.org
COMMENT=	FreeBSD userland bin directories and binaries

BUILD_DEPENDS=  ${OS_WORLDDIST}:os/buildworld@${OS_FLAVOR}

USES=	os:flavors

PREFIX=/
NEED_ROOT=	yes

.include <bsd.port.pre.mk>

do-build:
	@${MKDIR} ${STAGEDIR}
	${ECHO_MSG} "==> Extracting ${OS_WORLDDIST}..."
	${TAR} xpf ${OS_WORLDDIST} -C ${STAGEDIR}

do-install:
	${ECHO_MSG} "==> Generating plist..."
	(cd ${STAGEDIR}; ${FIND} ./bin ./usr/bin \( -type f -o -type l \) \
		| ${SED} -e 's,^\./,,g' \
		| ${AWK} '{print length, $$0}' | ${SORT} -rn \
		| ${AWK} '{print $$2 }' \
		| ${GREP} -v -e 'usr/bin/clang' -e 'usr/bin/cc' -e 'usr/bin/c++' \
			-e 'usr/bin/ld' -e 'usr/bin/llvm' -e 'usr/bin/lldb' \
		>> ${TMPPLIST})
	(cd ${STAGEDIR}; ${FIND} ./bin ./usr/bin \( -type d \) \
		| ${SED} -e 's,^\./,,g' \
		| ${AWK} '{print length, $$0}' | ${SORT} -rn \
		| ${AWK} '{print $$2 }' \
		| ${GREP} -v -x '/' \
		| ${XARGS} -I '{}' echo "@dir {}" \
		| ${GREP} -v -x '@dir ' \
		| ${CAT} >> ${TMPPLIST})

clean:
	if [ -d ${WRKDIR} ]; then \
		if [ -w ${WRKDIR} ]; then \
			${ECHO_MSG} "===> Cleaning for ${PKGNAME}"; \
			${CHFLAGS} -R noschg ${WRKDIR} ; \
			${RM} -r ${WRKDIR}; \
		else \
			${ECHO_MSG} "===>   ${WRKDIR} not writable, skipping"; \
		fi; \
	fi

.include "../Makefile.common"
.include <bsd.port.post.mk>
