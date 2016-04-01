FROM debian:jessie

RUN apt-get -y update
RUN apt-get -y install libfontconfig

RUN   mkdir -p /opt/grafana

ADD . /tmp/src
WORKDIR /tmp/src
RUN wget https://storage.googleapis.com/golang/go1.6.linux-amd64.tar.gz && \
  tar xf go1.6.linux-amd64.tar.gz && \
  ./go/bin/go run build.go build && \
  rm -rf ./go

RUN apt-get install node npm && \
  npm install -g grunt-cli && \
  grunt release
  npm uninstall grunt-cli && \

RUN cp -a tmp /opt/grafana/

EXPOSE 3000

VOLUME ["/opt/grafana/data"]
VOLUME ["/opt/grafana/conf"]

WORKDIR /opt/grafana/
ENTRYPOINT ["./grafana", "web"]
