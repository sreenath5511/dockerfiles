# run tor in a container
#
# docker run -d \
#	--restart always \
#	-v /etc/localtime:/etc/localtime:ro \
#	-p 9040:9040 \
#	-p 5353:5353 \
# 	--name tor-router \
# 	jess/tor-router
#
FROM debian:sid
MAINTAINER Jessica Frazelle <jess@docker.com>

RUN apt-get update && apt-get install -y \
	tor \
	--no-install-recommends \
	&& rm -rf /var/lib/apt/lists/*

EXPOSE 9040
EXPOSE 5353

# copy in our torrc file
COPY torrc.default /etc/tor/torrc.default

# make sure files are owned by tor user
RUN chown -R debian-tor:debian-tor /etc/tor/torrc.default

USER debian-tor

ENTRYPOINT [ "tor" ]
CMD [ "-f", "/etc/tor/torrc.default" ]