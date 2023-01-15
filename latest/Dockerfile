FROM pihole/pihole:latest

ENV \
	USER=bind \
	GROUP=bind

# install
RUN set -eux \
	&& apt update \
	&& apt install --no-install-recommends --no-install-suggests -y \
		bind9 \
	&& apt purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false \
	&& rm -r /var/lib/apt/lists/* \
	&& mkdir /var/log/named \
	&& chown bind:bind /var/log/named \
	&& chmod 0755 /var/log/named


# copy extra files
COPY ./data/docker-entrypoint.sh /


# set version label
LABEL maintainer="OrigamiOfficial"

# environment settings
ENV PIHOLE_DNS_ 127.0.0.1#5335


# target run
CMD ["/docker-entrypoint.sh"]
