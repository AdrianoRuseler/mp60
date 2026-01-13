# README.md

## Get scripts
```bash
mkdir scripts
cd scripts
wget https://raw.githubusercontent.com/AdrianoRuseler/mp60/refs/heads/main/scripts/UpdateScripts.sh -O UpdateScripts.sh
chmod a+x UpdateScripts.sh
./UpdateScripts.sh
```
## CreateApacheLocalSite
```bash
export LOCALSITENAME="mysite"
export SITETYPE="PROXY"
# export SITETYPE="HTPASSWD"
./CreateApacheLocalSite.sh
```
## CreateApacheSite
```bash
export LOCALSITENAME="mysite"
export SITETYPE="PROXY"
# export SITETYPE="HTPASSWD"
./CreateApacheSite.sh
```
