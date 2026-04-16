#
# NOTE: THIS DOCKERFILE IS GENERATED VIA "src/bin/joomengine.sh"
#
# PLEASE DO NOT EDIT IT DIRECTLY.
#
# -----------------------------------------------------------------------------
# Official JCB v5.1.6-alpha1 image: extend the official Joomla! v5.4.5 image
# -----------------------------------------------------------------------------
FROM joomla:5.4.5-php8.2-apache

# Metadata
LABEL maintainer="Llewellyn van der Merwe <llewellyn.van-der-merwe@community.joomla.org> (@Llewellynvdm), Lemuel van der Merwe <lemuel.van-der-merwe@community.joomla.org> (@lemuelvdm)"
LABEL org.opencontainers.image.title="Joomla! Component Builder - JoomEngine"
LABEL org.opencontainers.image.description="Joomla! v5.4.5 + Component Builder v5.1.6-alpha1"
LABEL org.opencontainers.image.version="5.1.6-alpha1"
LABEL org.opencontainers.image.source="https://github.com/octoleo/joomengine"

# -----------------------------------------------------------------------------
# JCB metadata (required at build-time)
# -----------------------------------------------------------------------------
ENV JCB_VERSION 5.1.6-alpha1
ENV JCB_SHA512 ba31afbd9b3f07f90ea9bfa5c62a022fbd51a5dc8d3522c83c3bb40a77d18d056734dfb4b91d98238d140a37acd48b013542ca5f0646da895438ffe61ef73154
ENV JCB_PACKAGE https://github.com/joomengine/pkg-component-builder/archive/refs/tags/v5.1.6-alpha1.zip
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
# JCB entrypoint
# -----------------------------------------------------------------------------
COPY docker-entrypoint.sh /entrypoint.sh
RUN set -eux; \
	chmod +x /entrypoint.sh

ENTRYPOINT ["/entrypoint.sh"]
CMD ["apache2-foreground"]

