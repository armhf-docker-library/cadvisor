FROM armhfbuild/alpine:3.3

RUN apk --update --no-cache add curl device-mapper \
  && curl -fsSL https://github.com/armhf-docker-library/glibc/releases/download/2.22/glibc-bin.tar.gz \
    | tar -xz -C / \
  && ln -s /usr/glibc-compat/lib/ld-linux-armhf.so.3 /lib/ld-linux-armhf.so.3

# # There is no alpine zfs-utils package for armhf yet
# RUN apk add zfs-utils --update-cache --repository http://dl-3.alpinelinux.org/alpine/edge/testing/ --allow-untrusted  \

RUN /usr/glibc-compat/sbin/ldconfig /lib /usr/glibc/usr/lib \
  && echo 'hosts: files mdns4_minimal [NOTFOUND=return] dns mdns4' >> /etc/nsswitch.conf

COPY ./cadvisor /usr/bin/cadvisor

EXPOSE 8080
ENTRYPOINT ["/usr/bin/cadvisor", "-logtostderr"]
