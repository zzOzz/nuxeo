###Dockerfile
---
```docker
FROM       quay.io/nuxeoio/nuxeo-base
MAINTAINER Vincent Lombard <vincent.lombard@universite-lyon.fr>
# Copy scripts
ADD nuxeo-install.sh /root/nuxeo-install.sh
ADD nuxeo-update.sh /root/nuxeo-update.sh
ADD start.sh /root/start.sh
# Download & Install Nuxeo
ENV NUXEO_VERSION nuxeo-7.4
RUN /bin/bash /root/nuxeo-install.sh
# Update Nuxeo
ADD instance.clid /var/lib/nuxeo/data/instance.clid
RUN /bin/bash /root/nuxeo-update.sh
# export NUXEO_CONF=/platform/etc/data/conf/nuxeo.conf
ENV NUXEO_CONF /platform/etc/data/conf/nuxeo.conf
# RUN mv -f /var/lib/nuxeo/server/lib/log4j.xml /var/lib/nuxeo/server/lib/log4j.xml.orig
ADD data /platform/etc/data/
RUN chown -R nuxeo:nuxeo /platform/etc/data/conf/nuxeo.conf
EXPOSE 8080
CMD ["/bin/bash","/root/start.sh"]
VOLUME ["/platform/etc/data/"]
ONBUILD RUN apt-get update && apt-get upgrade -y
```
