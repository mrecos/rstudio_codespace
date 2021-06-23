# Set up a local Rstudio connected to Codespaces

### Start a Codespace in your repo

### connect VS code to Todespace

- cntrl+Shift+p 
- "Codespaces: Add development container config files"
- show all
- Jupyter notebook

### in `devcontainer.json` add

```
"forwardPorts": [8787],
```

### in `dockerfile` add
#### from: https://www.rstudio.com/products/rstudio/download-server/debian-ubuntu/

```
&& apt-get update \
&& sudo apt-get install -y gdebi-core \
&& wget https://download2.rstudio.org/server/bionic/amd64/rstudio-server-1.4.1717-amd64.deb \
&& sudo gdebi -n rstudio-server-1.4.1717-amd64.deb
```
### and at the end
```
EXPOSE 8787
```

### Add location of R to `rserver.conf`
#### us vi to edit file
```
sudo vi /etc/rstudio/rserver.conf
```
#### add path from $which R
```
rsession-which-r=/opt/conda/bin/R
```
#### write and quite vi with `:wq`

### Fix some issue with the sqlite DB
#### from: https://community.rstudio.com/t/permissions-related-to-upgrade-to-rstudio-server-open-source-1-4/94256/3
```
 sudo rm /var/lib/rstudio-server/rstudio.sqlite 
 sudo chmod -R g=u /var/lib/rstudio-server
```

### Conirm Rstudio Server
```
sudo rstudio-server stop
sudo rstudio-server verify-installation
sudo rstudio-server start
```

#### add rstudio user 
```
sudo useradd rstudio
echo rstudio:NEWPASSWORD | sudo chpasswd 
```
