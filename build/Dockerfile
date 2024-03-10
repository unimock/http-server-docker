#https://github.com/patrickdappollonio/http-server/releases/download/v2.1.4/http-server_linux_arm64.tar.gz
#https://github.com/patrickdappollonio/http-server/releases/download/v2.1.4/http-server_linux_x86_64.tar.gz
#https://www.google.com/search?channel=fs&client=ubuntu-sn&q=docker+bake+platform
FROM alpine
RUN echo "nobody:x:65534:65534:Nobody:/:" > /etc/nobody
ARG VERSION="2.1.4"

ARG TARGETPLATFORM
RUN echo "$TARGETPLATFORM"

#RUN if [ "$TARGETPLATFORM" = "linux/amd64" ]; then ARCH="x86_64"; elif [ "$TARGETPLATFORM" = "linux/arm64" ]; then ARCH="arm64"; else ARCH="amd64"; fi && \
#  wget  -O /tmp/x.tar.gz https://github.com/patrickdappollonio/http-server/releases/download/v${VERSION}/http-server_linux_${ARCH}.tar.gz && \
#  tar -C / -xzf /tmp/x.tar.gz && \
#  chmod a+x /http-server
RUN mkdir -p /tmp

RUN if [ "$TARGETPLATFORM" = "linux/amd64" ]; then A="x86_64" ; else A="arm64" ; fi && \
 wget -O /tmp/x.tar.gz https://github.com/patrickdappollonio/http-server/releases/download/v${VERSION}/http-server_linux_${A}.tar.gz && \
 tar -C / -xzf /tmp/x.tar.gz && \
 chmod a+x /http-server
 

FROM scratch
WORKDIR /html
USER nobody

COPY --from=0 /etc/nobody /etc/passwd
COPY --from=0 /http-server /http-server
EXPOSE 80
ENTRYPOINT ["/http-server"]

