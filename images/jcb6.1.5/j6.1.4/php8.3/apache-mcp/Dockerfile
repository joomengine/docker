#
# NOTE: THIS DOCKERFILE IS GENERATED VIA "src/bin/joomengine.sh"
#
# PLEASE DO NOT EDIT IT DIRECTLY.
#
# -----------------------------------------------------------------------------
# Official JCB v6.1.5 image: extend the official Joomla! v6.1.4 image
# -----------------------------------------------------------------------------
FROM joomla:6.1.4-php8.3-apache@sha256:a319477eb87ab5ec3267c3c3b855dd6af3bdd9adedae53d7c4559d706631de24

# Metadata
LABEL maintainer="Llewellyn van der Merwe <llewellyn.van-der-merwe@community.joomla.org> (@Llewellynvdm), Lemuel van der Merwe <lemuel.van-der-merwe@community.joomla.org> (@lemuelvdm)"
LABEL org.opencontainers.image.title="Joomla! Component Builder - JoomEngine"
LABEL org.opencontainers.image.description="Joomla! v6.1.4 + Component Builder v6.1.5 + JoomEngine MCP v1.0.5"
LABEL org.opencontainers.image.version="6.1.5"
LABEL org.opencontainers.image.source="https://github.com/octoleo/joomengine"
LABEL org.opencontainers.image.base.name="docker.io/library/joomla:6.1.4-php8.3-apache"
LABEL org.opencontainers.image.base.digest="sha256:a319477eb87ab5ec3267c3c3b855dd6af3bdd9adedae53d7c4559d706631de24"

# -----------------------------------------------------------------------------
# JCB metadata (required at build-time)
# -----------------------------------------------------------------------------
ENV JCB_VERSION 6.1.5
ENV JCB_SHA512 ce658189d350262580e91c76162d4d2f3c375dc20c0496147be93fb82dd3792698da95a5c07a15da7d682e00da6c2ef19c597acb1f6645a1cba6700fd8060d71
ENV JCB_PACKAGE https://github.com/joomengine/pkg-component-builder/archive/refs/tags/v6.1.5.zip
ENV JCB_INSTALL_DIR /usr/src/joomengine

# -----------------------------------------------------------------------------
# Download & verify JCB package (immutable, pinned, hash-verified)
# -----------------------------------------------------------------------------
RUN set -eux; \
	mkdir -p "$JCB_INSTALL_DIR"; \
	curl -fSL "$JCB_PACKAGE" -o "$JCB_INSTALL_DIR/jcb.zip"; \
	echo "$JCB_SHA512  $JCB_INSTALL_DIR/jcb.zip" | sha512sum -c -; \
	chown -R www-data:www-data "$JCB_INSTALL_DIR"

# -----------------------------------------------------------------------------
# Optional JoomEngine MCP package (component and plugins, pinned at image build)
# -----------------------------------------------------------------------------
LABEL org.joomengine.mcp.version="1.0.5"
LABEL org.joomengine.mcp.sha512="94a58198ae09e5c510f902e59579f6f9762fbbb17939ac29968e886aa69871c85ee1aa15c2e2b29b4ec0a48b4025eccabb710f89655892fe9aee470eefaab745"
LABEL org.joomengine.mcp.source="https://github.com/joomengine/mcp_package/archive/refs/tags/v1.0.5.zip"
ENV MCP_VERSION=1.0.5
ENV MCP_SHA512=94a58198ae09e5c510f902e59579f6f9762fbbb17939ac29968e886aa69871c85ee1aa15c2e2b29b4ec0a48b4025eccabb710f89655892fe9aee470eefaab745
ENV MCP_PACKAGE=https://github.com/joomengine/mcp_package/archive/refs/tags/v1.0.5.zip

RUN set -eux; \
	curl -fSL "$MCP_PACKAGE" -o "$JCB_INSTALL_DIR/mcp.zip"; \
	echo "$MCP_SHA512  $JCB_INSTALL_DIR/mcp.zip" | sha512sum -c -; \
	chown www-data:www-data "$JCB_INSTALL_DIR/mcp.zip"

# -----------------------------------------------------------------------------
# JCB entrypoint
# -----------------------------------------------------------------------------
COPY docker-entrypoint.sh /entrypoint.sh
RUN set -eux; \
	chmod +x /entrypoint.sh

ENTRYPOINT ["/entrypoint.sh"]
CMD ["apache2-foreground"]
