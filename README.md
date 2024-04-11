# LodView NuBBE[KG]


## Running

```
docker build -t lodview_nubbe .
docker run -p 8083:8080 lodview_nubbe
```


## Redirect Config

```
<VirtualHost *>
    Use TemplateServerBlock marx@informatik.uni-leipzig.de nubbekg.aksw.org nubbekg.aksw.org

    Use TemplateForceHttps
    Use TemplateProxyBase

    #:%acmeno%letsencrypt.org% want nubbekg.aksw.org
    #:%acmeno%letsencrypt.org% want nubbe-kg.aksw.org

    Use TemplateHttpProxy2 141.57.8.18:8892 /sparql "sparql"

    SSLProxyEngine on
    ProxyPreserveHost off
    ProxyPass /downloads http://141.57.8.18:9090/downloads/
    ProxyPassReverse /downloads http://141.57.8.18:9090/downloads/
    ProxyPass /data http://141.57.8.18:8083/lodview/data
    ProxyPass /linkedResourceTitles http://141.57.8.18:8083/lodview/linkedResourceTitles
    ProxyPass /staticResources http://141.57.8.18:8083/lodview/staticResources
    ProxyPass /linkedResourceInverses http://141.57.8.18:8083/lodview/linkedResourceInverses
    ProxyPassReverse /data http://141.57.8.18:8083/lodview/data
    ProxyPassReverse /linkedResourceTitles http://141.57.8.18:8083/lodview/linkedResourceTitles
    ProxyPassReverse /staticResources http://141.57.8.18:8083/lodview/staticResources
    ProxyPassReverse /linkedResourceInverses http://141.57.8.18:8083/lodview/linkedResourceInverses
    ProxyPass / https://chemnet-io.github.io/nubbeKG/ retry=1
    ProxyPassReverse / https://chemnet-io.github.io/nubbeKG/

</VirtualHost>
```
