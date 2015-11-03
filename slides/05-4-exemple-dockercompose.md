###nuxeo docker-compose.yml
---

~~~
shibbolethsp:
  hostname: shib-pp
  domainname: ad.universite-lyon.fr
  image: nuxeoshibbolethdocker_shibbolethsp
  environment:
    VIRTUAL_HOST: nuxeo.universite-lyon.fr
    VIRTUAL_PROTO: https
  links:
    - nuxeo
  ports:
    - "443"
nuxeo:
  hostname: nuxeo-pp
  image: nuxeodocker_nuxeo:6.0-HF21
  domainname: ad.universite-lyon.fr
  environment:
    PACKAGES: "nuxeo-drive shibboleth-authentication nuxeo-diff nuxeo-virtualnavigation nuxeo-dam nuxeo-spreadsheet nuxeo-template-rendering nuxeo-web-mobile nuxeo-agenda nuxeo-platform-importer easyshare nuxeo-platform-user-registration"
    PACKAGES2: "pres-lyon-2.1.102 /platform/etc/data/conf/marketplace/marketplace-multidomain-userworkspace-1.0-SNAPSHOT.zip /platform/etc/data/conf/marketplace/marketplace-CustomLoginUDL-1.0.9-SNAPSHOT.zip /platform/etc/data/conf/marketplace/marketplace-LdapConf-1.0.0-SNAPSHOT.zip"
    TEMPLATES: "postgresql,drive,/platform/etc/data/conf/templates/shibboleth"
  volumes:
    - /data-pp:/platform/etc/data
    - /data-pp/conf/log4j.xml:/var/lib/nuxeo/server/lib/log4j.xml:ro
  ~~~
