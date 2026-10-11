# Upstream's Dockerfile (XBEN-052-24/src/Dockerfile) with these changes:
# - the sources are copied from app/src/ (the vendored benchmark folder sits in app/)
# - the build argument FLAG defaults to this lab's fixed flag, the value upstream's Makefile passes
#   (FLAG{sha256 of "XBEN-052-24"}), since the spec passes no build arguments
FROM php:5-apache

COPY app/src/ .
WORKDIR /var/www/html

ARG FLAG=FLAG{46c3ef043123012aa7ed0ab5a0c6a7e40a53a624ce3ae406f52e7301a8033a9b}

RUN sed -i s/@FLAG@/$FLAG/g index.php

EXPOSE 80

# CyberCTF per-player flag: the flag above is only the development fallback. ctf-entrypoint.sh
# puts the player's flag (CTF_FLAG_MAIN) in its place at every start, then runs the original
# entrypoint and command, repeated here unchanged.
COPY ctf-entrypoint.sh /usr/local/bin/ctf-entrypoint.sh
ENTRYPOINT ["/usr/local/bin/ctf-entrypoint.sh", "docker-php-entrypoint"]
CMD ["apache2-foreground"]
