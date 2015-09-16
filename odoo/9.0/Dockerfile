FROM debian:stable
MAINTAINER EricVernichon "eric@vernichon.fr"

RUN (apt-get update && apt-get upgrade -y -q && apt-get dist-upgrade -y -q && apt-get -y -q autoclean && apt-get -y -q autoremove)
RUN apt-get -y install postgresql-9.4 postgresql-client-9.4
RUN apt-get -y install git
RUN mkdir /opt/odoo
RUN git clone -b 9.0 https://github.com/odoo/odoo.git /opt/odoo/9.0
RUN apt-get -y install python-dev libsasl2-dev sudo libjpeg-dev libevent-dev gcc libxml2-dev libxslt-dev node-less libldap2-dev
RUN apt-get -y install wget net-tools apt-utils openssh-server
RUN apt-get -y install postgresql-server-dev-9.4
RUN wget https://bootstrap.pypa.io/get-pip.py
RUN python get-pip.py
RUN pip install -r /opt/odoo/9.0/requirements.txt
RUN pip install pillow
RUN useradd --home /opt/odoo --shell /bin/bash odoo
RUN chown odoo.odoo -R /opt/odoo
RUN pg_dropcluster --stop 9.4 main
RUN pg_createcluster   -e UTF-8 9.4 main
RUN /etc/init.d/postgresql start &&  su  - postgres -c "createuser -s odoo"
COPY start_openerp /usr/local/bin/
RUN wget http://download.gna.org/wkhtmltopdf/0.12/0.12.2/wkhtmltox-0.12.2_linux-jessie-amd64.deb
RUN apt-get -y install fontconfig  libfontconfig1 libfreetype6 libpng12-0 libxrender1 xfonts-base xfonts-75dpi
RUN dpkg -i wkhtmltox-0.12.2_linux-jessie-amd64.deb
RUN cp /usr/local/bin/wkhtmltopdf /usr/bin/
RUN cp /usr/local/bin/wkhtmltoimage /usr/bin/
RUN chmod +x /usr/local/bin/start_openerp
CMD ["/bin/bash","/usr/local/bin/start_openerp"]
EXPOSE   8069
