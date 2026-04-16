#
# NOTE: THIS DOCKERFILE IS GENERATED VIA "src/bin/joomengine.sh"
#
# PLEASE DO NOT EDIT IT DIRECTLY.
#
# -----------------------------------------------------------------------------
# Official JCB v4.1.5-alpha1 image: extend the official Joomla! v4.4.14 image
# -----------------------------------------------------------------------------
FROM joomla:4.4.14-php8.1-fpm

# Metadata
LABEL maintainer="Llewellyn van der Merwe <llewellyn.van-der-merwe@community.joomla.org> (@Llewellynvdm), Lemuel van der Merwe <lemuel.van-der-merwe@community.joomla.org> (@lemuelvdm)"
LABEL org.opencontainers.image.title="Joomla! Component Builder - JoomEngine"
LABEL org.opencontainers.image.description="Joomla! v4.4.14 + Component Builder v4.1.5-alpha1"
LABEL org.opencontainers.image.version="4.1.5-alpha1"
LABEL org.opencontainers.image.source="https://github.com/octoleo/joomengine"

# -----------------------------------------------------------------------------
# JCB metadata (required at build-time)
# -----------------------------------------------------------------------------
ENV JCB_VERSION 4.1.5-alpha1
ENV JCB_SHA512 fa33f6702c1b633b43e8b044ef069f459cf90da0f90689c43d1380da11271854f2310c38ffa4c87e8747769835764871c6b824c569f04d14435f61e75481dfd5
ENV JCB_PACKAGE https://github.com/joomengine/pkg-component-builder/archive/refs/tags/v4.1.5-alpha1.zip
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
CMD ["php-fpm"]

