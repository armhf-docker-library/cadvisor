FROM armhfbuild/golang:1.5.3

RUN go get -d github.com/google/cadvisor \
  && go get github.com/tools/godep \
  && cd $GOPATH/src/github.com/google/cadvisor \
  && godep go build . \
  && cp ./cadvisor /usr/local/bin/

CMD ["cadvisor"]
