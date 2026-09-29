#
# NOTE: THIS DOCKERFILE IS GENERATED VIA "src/bin/joomengine.sh"
#
# PLEASE DO NOT EDIT IT DIRECTLY.
#
# -----------------------------------------------------------------------------
# Official JCB v6.1.3 image: extend the official Joomla! v6.1.3 image
# -----------------------------------------------------------------------------
FROM joomla:6.1.3-php8.4-apache@sha256:6ccc90fc7d0375507a86604de2b6a6dca56fea775b9941445b36fe1712a35c85

# Metadata
LABEL maintainer="Llewellyn van der Merwe <llewellyn.van-der-merwe@community.joomla.org> (@Llewellynvdm), Lemuel van der Merwe <lemuel.van-der-merwe@community.joomla.org> (@lemuelvdm)"
LABEL org.opencontainers.image.title="Joomla! Component Builder - JoomEngine"
LABEL org.opencontainers.image.description="Joomla! v6.1.3 + Component Builder v6.1.3 + JoomEngine MCP v1.0.2"
LABEL org.opencontainers.image.version="6.1.3"
LABEL org.opencontainers.image.source="https://github.com/octoleo/joomengine"
LABEL org.opencontainers.image.base.name="docker.io/library/joomla:6.1.3-php8.4-apache"
LABEL org.opencontainers.image.base.digest="sha256:6ccc90fc7d0375507a86604de2b6a6dca56fea775b9941445b36fe1712a35c85"

# -----------------------------------------------------------------------------
# JCB metadata (required at build-time)
# -----------------------------------------------------------------------------
ENV JCB_VERSION 6.1.3
ENV JCB_SHA512 987a41234f52a9e632825445039b6feb8ca5d2c2118f570a0777d78603efe7ad6bd31547a2d2fe31421d5105e04799b31dc86c55f77a3d53e1a60d7a174c4f45
ENV JCB_PACKAGE https://github.com/joomengine/pkg-component-builder/archive/refs/tags/v6.1.3.zip
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
LABEL org.joomengine.mcp.version="1.0.2"
LABEL org.joomengine.mcp.sha512="c7b14f9f870a91e074524c438c7e29fc6a5452017e169c80b501a499c10a4e1fc7425a2bc8ec7ef759ce14580af8ee05846ca27b4cb3752d4a3df218b46f7d3f"
LABEL org.joomengine.mcp.source="https://github.com/joomengine/mcp_package/archive/refs/tags/v1.0.2.zip"
ENV MCP_VERSION=1.0.2
ENV MCP_SHA512=c7b14f9f870a91e074524c438c7e29fc6a5452017e169c80b501a499c10a4e1fc7425a2bc8ec7ef759ce14580af8ee05846ca27b4cb3752d4a3df218b46f7d3f
ENV MCP_PACKAGE=https://github.com/joomengine/mcp_package/archive/refs/tags/v1.0.2.zip

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
