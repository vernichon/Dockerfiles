FROM debian:stable
MAINTAINER EricVernichon "eric@vernichon.fr"
RUN apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys B97B0AFCAA1A47F044F244A07FCC7D46ACCC4CF8
RUN echo "deb http://apt.postgresql.org/pub/repos/apt/ jessie-pgdg main" > /etc/apt/sources.list.d/pgdg.list
RUN (apt-get update && apt-get upgrade -y -q && apt-get dist-upgrade -y -q && apt-get -y -q autoclean && apt-get -y -q autoremove)
RUN apt-get -y install postgresql-9.4 postgresql-client-9.4
RUN apt-get -y install git
RUN apt-get -y install openssh-server
RUN apt-get -y install python-psycopg2
RUN apt-get -y install python-babel
RUN apt-get -y install python-lxml
RUN apt-get -y install python-tz
RUN apt-get -y install python-imaging
RUN apt-get -y install python-yaml
RUN apt-get -y install python-reportlab
RUN apt-get -y install python-mako
RUN apt-get -y install python-pychart
RUN apt-get -y install python-werkzeug
RUN apt-get -y install python-dateutil
RUN apt-get -y install python-openid
RUN apt-get -y install python-docutils
RUN apt-get -y install postgresql
RUN apt-get -y install python-setuptools
RUN apt-get -y install python-pychart
RUN apt-get -y install python-pybabel
RUN apt-get -y install python-simplejson
RUN apt-get -y install python-httplib2
RUN apt-get -y install python-unittest2
RUN apt-get -y install python-mock
RUN apt-get -y install python-jinja2
RUN apt-get -y install python-gdata
RUN  easy_install python-dime
RUN apt-get -y install wget net-tools apt-utils
RUN apt-get -y install postgresql-server-dev-9.4
RUN mkdir /opt/odoo
RUN git clone -b 7.0 https://github.com/odoo/odoo.git /opt/odoo/7.0
RUN useradd --home /opt/odoo --shell /bin/bash odoo
RUN chown odoo.odoo -R /opt/odoo
RUN pg_dropcluster --stop 9.4 main
RUN pg_createcluster   -e UTF-8 9.4 main
RUN wget https://bootstrap.pypa.io/get-pip.py
COPY alter_password.sql /tmp/
RUN /etc/init.d/postgresql start && su  - postgres -c "createuser -s odoo" && su - postgres -c  "psql -f /tmp/alter_password.sql"
RUN echo "host all  all    0.0.0.0/0  md5" >> /etc/postgresql/9.4/main/pg_hba.conf
RUN echo "listen_addresses='*'" >> /etc/postgresql/9.4/main/postgresql.conf
COPY start_openerp /usr/local/bin/
RUN chmod +x /usr/local/bin/start_openerp
CMD ["/bin/bash","/usr/local/bin/start_openerp"]
EXPOSE   8069
EXPOSE 5432
EXPOSE 22
