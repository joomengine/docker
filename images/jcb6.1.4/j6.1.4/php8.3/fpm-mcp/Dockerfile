#
# NOTE: THIS DOCKERFILE IS GENERATED VIA "src/bin/joomengine.sh"
#
# PLEASE DO NOT EDIT IT DIRECTLY.
#
# -----------------------------------------------------------------------------
# Official JCB v6.1.4 image: extend the official Joomla! v6.1.4 image
# -----------------------------------------------------------------------------
FROM joomla:6.1.4-php8.3-fpm@sha256:5d982624795500ca6edfec0834b636140665036be58ecfdbb203895bec511afa

# Metadata
LABEL maintainer="Llewellyn van der Merwe <llewellyn.van-der-merwe@community.joomla.org> (@Llewellynvdm), Lemuel van der Merwe <lemuel.van-der-merwe@community.joomla.org> (@lemuelvdm)"
LABEL org.opencontainers.image.title="Joomla! Component Builder - JoomEngine"
LABEL org.opencontainers.image.description="Joomla! v6.1.4 + Component Builder v6.1.4 + JoomEngine MCP v1.0.6"
LABEL org.opencontainers.image.version="6.1.4"
LABEL org.opencontainers.image.source="https://github.com/octoleo/joomengine"
LABEL org.opencontainers.image.base.name="docker.io/library/joomla:6.1.4-php8.3-fpm"
LABEL org.opencontainers.image.base.digest="sha256:5d982624795500ca6edfec0834b636140665036be58ecfdbb203895bec511afa"

# -----------------------------------------------------------------------------
# JCB metadata (required at build-time)
# -----------------------------------------------------------------------------
ENV JCB_VERSION 6.1.4
ENV JCB_SHA512 cde289bdd21689dcb90ac68d44573ce52c0ff861ff02780327b1ff7f3a58918ddcf010f1e4a2b79af17cd91bf33ee4b81d99a8be9d98ce81e560614bd26d6a66
ENV JCB_PACKAGE https://github.com/joomengine/pkg-component-builder/archive/refs/tags/v6.1.4.zip
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
LABEL org.joomengine.mcp.version="1.0.6"
LABEL org.joomengine.mcp.sha512="46ef7cb59b8371aaeb25232c9f88ba7002f215be6a7404b802be1ac1ac15ecd52771874b9c016fd7453f7e46a2a36ca93a9d8ff4326105dee83341ec07638497"
LABEL org.joomengine.mcp.source="https://github.com/joomengine/mcp_package/archive/refs/tags/v1.0.6.zip"
ENV MCP_VERSION=1.0.6
ENV MCP_SHA512=46ef7cb59b8371aaeb25232c9f88ba7002f215be6a7404b802be1ac1ac15ecd52771874b9c016fd7453f7e46a2a36ca93a9d8ff4326105dee83341ec07638497
ENV MCP_PACKAGE=https://github.com/joomengine/mcp_package/archive/refs/tags/v1.0.6.zip

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
CMD ["php-fpm"]
