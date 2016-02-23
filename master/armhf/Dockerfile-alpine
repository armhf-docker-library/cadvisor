FROM armhfbuild/alpine:3.3

RUN apk --update-cache add curl device-mapper
#   && curl -fsSL https://github.com/armhf-docker-library/glibc/releases/download/2.22/glibc-bin.tar.gz \
#     | tar -xz -C / \
#   && ln -s /usr/glibc-compat/lib/ld-linux-armhf.so.3 /lib/ld-linux-armhf.so.3

RUN cd /tmp \
  && curl -fsSL https://github.com/armhf-docker-library/alpine-pkg-glibc/releases/download/2.22/glibc-2.22-r8.apk \
    -o glibc.apk \
  && curl -fsSL https://github.com/armhf-docker-library/alpine-pkg-glibc/releases/download/2.22/glibc-bin-2.22-r8.apk \
    -o glibc-bin.apk \
  && apk add --allow-untrusted glibc.apk glibc-bin.apk

COPY ./nsswitch.conf /etc/
COPY ./ld.so.conf /usr/glibc-compat/etc/
RUN /usr/glibc-compat/sbin/ldconfig /lib /usr/glibc/usr/lib

COPY ./cadvisor /usr/bin/

EXPOSE 8080
ENTRYPOINT ["/usr/bin/cadvisor", "-logtostderr"]
