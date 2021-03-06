FROM ubuntu:latest as builder

ARG DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt-get install --assume-yes apt-utils
RUN apt-get install curl -y
RUN curl -L -o /tmp/go.sh https://install.direct/go.sh
RUN chmod +x /tmp/go.sh
RUN /tmp/go.sh

FROM alpine:latest

LABEL maintainer "Darian Raymond <admin@v2ray.com>"

COPY --from=builder /usr/bin/v2ray/v2ray /usr/bin/v2ray/
COPY --from=builder /usr/bin/v2ray/v2ctl /usr/bin/v2ray/
COPY --from=builder /usr/bin/v2ray/geoip.dat /usr/bin/v2ray/
COPY --from=builder /usr/bin/v2ray/geosite.dat /usr/bin/v2ray/
EXPOSE 8000
COPY config.json /etc/v2ray/config.json

RUN set -ex && \
apk --no-cache add ca-certificates && \
mkdir /var/log/v2ray/ &&\
chmod +x /usr/bin/v2ray/v2ctl && \
chmod +x /usr/bin/v2ray/v2ray
ENV TZ=Asia/Shanghai
ENV PATH /usr/bin/v2ray:$PATH

CMD ["/usr/bin/v2ray/v2ray", "-config=/etc/v2ray/config.json"]
