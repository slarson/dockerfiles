# Stable version of etherpad doesn't support npm 2
FROM debian:jessie
MAINTAINER Tony Motakis <tvelocity@gmail.com>

ENV ETHERPAD_VERSION 1.5.7

RUN apt-get update && \
    apt-get install -y curl unzip nodejs-legacy npm mysql-client && \
    rm -r /var/lib/apt/lists/*

WORKDIR /opt/

RUN curl -SL \
    https://github.com/ether/etherpad-lite/archive/${ETHERPAD_VERSION}.zip \
    > etherpad.zip && unzip etherpad && rm etherpad.zip && \
    mv etherpad-lite-${ETHERPAD_VERSION} etherpad-lite

WORKDIR etherpad-lite

RUN bin/installDeps.sh && rm settings.json
COPY entrypoint.sh /entrypoint.sh

VOLUME /opt/etherpad-lite/var
RUN ln -s var/settings.json settings.json

RUN npm install \
    ep_ether-o-meter \
    ep_timesliderdiff \
    ep_page_view \
    ep_disable_reset_authorship_colours \
    ep_print \
    ep_font_size \
    ep_font_color \
    ep_font_family \
    ep_sketchspace \
    ep_set_title_on_pad \
    ep_mypads

EXPOSE 9001
ENTRYPOINT ["/entrypoint.sh"]
CMD ["bin/run.sh", "--root"]
