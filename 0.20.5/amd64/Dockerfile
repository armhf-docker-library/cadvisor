FROM alpine:3.3

RUN apk --update --no-cache add curl device-mapper \
  && curl -fsSOL https://circle-artifacts.com/gh/andyshinn/alpine-pkg-glibc/8/artifacts/0/home/ubuntu/alpine-pkg-glibc/packages/x86_64/glibc-2.21-r2.apk \
  && curl -fsSOL https://circle-artifacts.com/gh/andyshinn/alpine-pkg-glibc/8/artifacts/0/home/ubuntu/alpine-pkg-glibc/packages/x86_64/glibc-bin-2.21-r2.apk \
  && apk add --allow-untrusted glibc-2.21-r2.apk glibc-bin-2.21-r2.apk

RUN apk add zfs-utils --update-cache --repository http://dl-3.alpinelinux.org/alpine/edge/testing/ --allow-untrusted  \
  && /usr/glibc/usr/bin/ldconfig /lib /usr/glibc/usr/lib \
  && echo 'hosts: files mdns4_minimal [NOTFOUND=return] dns mdns4' >> /etc/nsswitch.conf

COPY ./cadvisor /usr/bin/cadvisor

EXPOSE 8080
ENTRYPOINT ["/usr/bin/cadvisor", "-logtostderr"]
