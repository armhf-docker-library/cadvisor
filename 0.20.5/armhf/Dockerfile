FROM armhfbuild/alpine:3.3

RUN apk --update --no-cache add curl device-mapper \
  && curl -fsSL https://github.com/armhf-docker-library/glibc/releases/download/2.22/glibc-bin.tar.gz \
    | tar -xz -C / \
  && ln -s /usr/glibc-compat/lib/ld-linux-armhf.so.3 /lib/ld-linux-armhf.so.3

COPY ./nsswitch.conf /etc/
COPY ./ld.so.conf /usr/glibc-compat/etc/
RUN /usr/glibc-compat/sbin/ldconfig /lib /usr/glibc/usr/lib

COPY ./cadvisor /usr/bin/

EXPOSE 8080
ENTRYPOINT ["/usr/bin/cadvisor", "-logtostderr"]
