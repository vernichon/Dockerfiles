# README #


Dockerfiles


for build image / pour construire l'image

git clone git@bitbucket.org:eric_vernichon/dockerfiles.git

docker build -t erp/odoo:v9  dockerfiles/odoo/9.0/

....

REPOSITORY TAG IMAGE ID CREATED VIRTUAL SIZE

erp/odoo v9 9b47bc2fa2ae 15 seconds ago 3.343 GB



for use / pour l’utiliser

docker run -p 8069:8069 -t -i erp/odoo:v9 



Plus de détails sur mon site  http://www.vernichon.fr/?p=1246