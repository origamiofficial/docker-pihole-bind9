FROM pihole/pihole:dev

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
COPY lighttpd-external.conf /etc/lighttpd/external.conf
COPY 99-edns.conf /etc/dnsmasq.d/99-edns.conf
COPY ./data/docker-entrypoint.sh /
RUN chmod +x /docker-entrypoint.sh


# set version label
LABEL maintainer="OrigamiOfficial"

# environment settings
ENV PIHOLE_DNS_ 127.0.0.1#5335


# target run
CMD ["/docker-entrypoint.sh"]
