ARG BUILD_FROM
FROM $BUILD_FROM AS BUILD
ENV LANG C.UTF-8

RUN apk --update add --no-cache \
	nodejs npm python3 py3-pip alpine-sdk libcap bluez bluez-dev eudev-dev

FROM $BUILD_FROM AS RUNNING
RUN setcap cap_net_raw+eip $(eval readlink -f $(which node))

WORKDIR /

COPY start.sh /app/start.sh
COPY addon /app
RUN rm -rf /app/node_modules

RUN cd /app && npm i

# here we should just copy the /app contents to a run image with nodejs and other requirements only

ENTRYPOINT ["/app/start.sh"]

LABEL io.hass.version="VERSION" io.hass.type="addon" io.hass.arch="armhf|aarch64|i386|amd64"
