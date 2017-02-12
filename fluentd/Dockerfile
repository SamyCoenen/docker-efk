FROM fluent/fluentd:latest

MAINTAINER Samy Coenen <contact@samycoenen.be>

WORKDIR /home/fluent
ENV PATH /home/fluent/.gem/ruby/2.3.0/bin:$PATH

USER root
RUN apk --no-cache add sudo build-base ruby-dev && \
sudo -u fluent gem install fluent-plugin-elasticsearch fluent-plugin-record-reformer fluent-plugin-rewrite-tag-filter \
fluent-plugin-tail-ex fluent-plugin-elasticsearch fluent-plugin-parser fluent-plugin-docker fluent-plugin-json-transform && \
rm -rf /home/fluent/.gem/ruby/2.3.0/cache/*.gem && sudo -u fluent gem sources -c && \
apk del sudo build-base ruby-dev

EXPOSE 24284
USER fluent
COPY plugins /fluentd/plugins
CMD fluentd -c /home/fluent/data/fluentd.conf -p /fluentd/plugins $FLUENTD_OPT
