

FROM    alpine:3.15

ADD     repositories /etc/apk/repositories
RUN     apk -U add alpine-sdk sudo nano bash

RUN     mkdir -p /var/cache/distfiles && \
        adduser -D packager && \
        addgroup packager abuild && \
        chgrp abuild /var/cache/distfiles && \
        chmod g+w /var/cache/distfiles && \
        echo "packager    ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers && \
        apk -U upgrade

ADD     setup.sh /home/packager/bin/setup.sh
ADD     build_gvm.sh /home/packager/bin/build.sh
ADD     build_single.sh /home/packager/bin/build_single.sh
ADD     update_checksum.sh /home/packager/bin/update_checksum.sh
# TODO: customize /etc/abuild.conf

WORKDIR /work
USER    packager

ENTRYPOINT [ "/home/packager/bin/setup.sh" ]
