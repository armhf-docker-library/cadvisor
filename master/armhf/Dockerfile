FROM armhfbuild/debian:jessie

# RUN apt-get update && apt-get install -y dmsetup zfs-utils
COPY ./cadvisor /usr/bin/

EXPOSE 8080
ENTRYPOINT ["/usr/bin/cadvisor", "-logtostderr"]
