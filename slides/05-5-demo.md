##Demo
---

~~~
cd ~/Downloads/
rm -fr nuxeo >/dev/null
git clone --recursive https://github.com/zzOzz/nuxeo.git
cd nuxeo/nuxeo-docker
docker-compose build
docker-compose up
open https://dev.local/nuxeo/
~~~
<!-- .element class="fragment" style="color:#268bd2;"-->
