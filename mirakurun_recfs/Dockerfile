FROM amd64/debian:buster AS build2
WORKDIR /build
RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y --no-install-recommends build-essential curl ca-certificates && \
    curl -fsSL https://github.com/epgdatacapbon/recfsusb2n/tarball/master | \
                tar -xz --strip-components=1
WORKDIR /build/src
RUN make

FROM chinachu/mirakurun:latest
COPY --from=build2 /build/src/recfsusb2n /usr/bin
COPY --from=build2 /build/src/recfsusb2n.conf /usr/bin
CMD ["./docker/container-init.sh"]
EXPOSE 40772 9229
