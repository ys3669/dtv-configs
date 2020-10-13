ARG ARCH=
FROM ${ARCH}node:14.7.0-buster AS build
WORKDIR /app
ENV DOCKER=YES
ADD . .
RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y --no-install-recommends build-essential && \
    npm install && \
    npm run build && \
    npm install -g --unsafe-perm --production

FROM ${ARCH}node:14.7.0-buster-slim
ENV DEV="build-essential libtool autoconf git automake cmake"
WORKDIR /app
RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y --no-install-recommends \
    make \
    gcc \
    g++ \
    pkg-config \
    pcscd \
    libpcsclite-dev \
    libccid \
    wget \
    pcsc-tools && \
    apt-get -y install $DEV && \
    \
    # recpt1
    \
    git clone https://github.com/stz2012/recpt1 /tmp/recpt1 && \
    cd /tmp/recpt1/recpt1 && \
    ./autogen.sh && \
    ./configure && \
    make && \
    make install && \
    mkdir -p /opt/bin/ && \
    \
    # 不要なファイルを削除
    \
    apt-get -y remove $DEV && \
    apt-get autoremove -y && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* && \
    rm -rf /tmp
#Info.plist
RUN rm -rf /etc/libccid_Info.plist && \
    wget https://gist.githubusercontent.com/ys3669/bb62654ea3a6bd76afea1ef7cf725506/raw/b1b36c4dd1873aa9f97851702aedb0c76e46584d/Info.plist -O /etc/libccid_Info.plist && \
    chmod 755 /etc/libccid_Info.plist
COPY --from=build /usr/local/lib/node_modules/mirakurun /app
CMD ["./docker/container-init.sh"]
EXPOSE 40772 9229
