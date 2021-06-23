# rstudio_codespace

# connect VS code go codespace
# cntrl+Shift+p - "Codespaces: Add development container config files" -> show all -> Jupyter notebook

#devcontainer.json add
```
"forwardPorts": [8787],
```

# dockerfile add
# https://www.rstudio.com/products/rstudio/download-server/debian-ubuntu/

```
&& apt-get update \
&& sudo apt-get install -y gdebi-core \
&& wget https://download2.rstudio.org/server/bionic/amd64/rstudio-server-1.4.1717-amd64.deb \
&& sudo gdebi -n rstudio-server-1.4.1717-amd64.deb
#and
EXPOSE 8787
```

sudo vi /etc/rstudio/rserver.conf
# add from $ which R
```
rsession-which-r=/opt/conda/bin/R
```
# :wq (to write and quit)

# https://community.rstudio.com/t/permissions-related-to-upgrade-to-rstudio-server-open-source-1-4/94256/3
```
 sudo rm /var/lib/rstudio-server/rstudio.sqlite 
 sudo chmod -R g=u /var/lib/rstudio-server
```

# test
```
sudo rstudio-server stop
sudo rstudio-server verify-installation
sudo rstudio-server start
```

# add rstudio user
```
sudo useradd rstudio
echo rstudio:rstudio | sudo chpasswd 
```
