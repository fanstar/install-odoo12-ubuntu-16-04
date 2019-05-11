## - How to install Odoo 12 on Ubuntu 16.04 --
# Odoo System Dependencies
### STEP 1
```Unix
sudo apt-get update
sudo apt-get -y upgrade
```
### STEP 2
Install Python Dependencies for Odoo 12
```Unix
sudo apt install git python3-pip build-essential wget python3-dev python3-venv python3-wheel libxslt-dev libzip-dev libldap2-dev libsasl2-dev python3-setuptools node-less
```
INSTALL DEPENDENCIES USING PIP3
```Unix
$ pip3 install Babel decorator docutils ebaysdk feedparser gevent greenlet html2text Jinja2 lxml Mako MarkupSafe mock num2words ofxparse passlib Pillow psutil psycogreen pydot pyparsing PyPDF2 pyserial python-dateutil python-openid pytz pyusb PyYAML qrcode reportlab requests six suds-jurko vatnumber vobject Werkzeug XlsxWriter xlwt xlrd
```
INSTALL psycopg2 on Python3
```Unix
sudo apt-get install python3-dev
pip3 install psycopg2
```
if get Error ==> Command "python setup.py egg_info" failed with error code 1 in /tmp/pip-build-ggml4lwf/psycopg2/
Use this command
```Unix
sudo apt-get install python3-dev
sudo apt-get install python3-psycopg2
```

INSTALL ssl on ubuntu
```Unix
sudo apt-get install libssl-dev
```
# Odoo Web Dependencies
### STEP 3
```Unix
sudo apt-get install -y npm
```
### STEP 4 Link node to user node
```Unix
sudo apt-get install -y npm
sudo ln -s /usr/bin/nodejs /usr/bin/node
```
### STEP 5 setup web lib
```Unix
sudo npm install -g less less-plugin-clean-css
sudo apt-get install node-less
sudo python3 -m pip install libsass
sudo apt install python-pip
sudo pip install --upgrade pip
```

# Odoo Database [postgreSQL] Dependencies
### STEP 6 Install PostgreSQL 9.6+
```Unix
sudo apt-get install python3-software-properties
```
### STEP 7 Add source list
```Unix
sudo nano /etc/apt/sources.list.d/pgdg.list
```
Put this line [ ctrl+o == save , ctrl+x == exit ]
```Unix
deb http://apt.postgresql.org/pub/repos/apt/ xenial-pgdg main
```
STEP 8 get Key access
```Unix
wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -
sudo apt-get update
```
### STEP 8 install postgreSQL
```Unix
sudo apt-get install postgresql-9.6
```
### STEP 9 Change TimeZone to 'UTC' DB for postgreSQL
>> scroll down to bottom <<
```Unix
#timezone = 'localtime'
timezone = 'UTC'
```

### STEP 10 Create User for postgreSQL DB
```Unix
sudo su postgres
```
Use cd to root path
```Unix
cd
```
Create user odoo
```Unix
createuser -s odoo
createuser -s ubuntu_user_name
createuser -s root
exit
```
### STEP 11 Create path and group for odoo user 
```Unix
sudo adduser --system --home=/opt/odoo --group odoo
```
# Install Gdata
### STEP 12 Create Data path "/opt/odoo"
```Unix
cd /opt/odoo
sudo wget https://pypi.python.org/packages/a8/70/bd554151443fe9e89d9a934a7891aaffc63b9cb5c7d608972919a002c03c/gdata-2.0.18.tar.gz
sudo tar zxvf gdata-2.0.18.tar.gz
```
### STEP 13 Take action by root user and install python package
```Unix
sudo chown -R odoo: gdata-2.0.18
sudo -s
cd gdata-2.0.18/
python setup.py install
```
### STEP 14 exit from root user
```Unix
exit
```

# Odoo Project from GitHub [setup data folder]
### STEP 15 Go to "/opt/odoo" and enter "odoo user"
```Unix
cd /opt/odoo
sudo su - odoo -s /bin/bash
git clone https://www.github.com/odoo/odoo --depth 1 --branch 12.0 --single-branch
```
Exit from "odoo user"
```Unix
exit
```
### STEP 15 Create Log file path
```Unix
sudo mkdir /var/log/odoo
sudo chown -R odoo:root /var/log/odoo
```
### STEP 16 Create and Edit Odoo configuration file
```Unix
sudo nano /etc/odoo.conf
```
Put this setting in config file [Default odoo-server.conf] 
AddonsPath is important!
```Unix
[options]

; This is the password that allows database operations:

; admin_passwd = admin

db_host = False

db_port = False

db_user = odoo

db_password = False

logfile = /var/log/odoo/odoo-server.log

addons_path = /opt/odoo/addons,/opt/odoo/odoo/addons
```
### STEP 17 Create Log file path
```Unix
sudo chown odoo: /etc/odoo.conf
```

# WKHTMLTOPDF ( Supported Version 0.12.1 ) for Odoo
### STEP 18 Lib export html to pdf , 
```Unix
sudo wget https://builds.wkhtmltopdf.org/0.12.1.3/wkhtmltox_0.12.1.3-1~bionic_amd64.deb
sudo apt install ./wkhtmltox_0.12.1.3-1~bionic_amd64.deb
sudo cp /usr/local/bin/wkhtmltoimage /usr/bin/wkhtmltoimage
sudo cp /usr/local/bin/wkhtmltopdf /usr/bin/wkhtmltopdf
```
Exit from "odoo user"
```Unix
exit
```

# START Odoo Server
### STEP 19 ==> "./odoo-bin" command
```Unix
cd /opt/odoo/odoo
./odoo-bin
```

If success you will get message like this
```Unix
2019-05-11 14:37:04,529 13607 INFO ? odoo: Odoo version 12.0
2019-05-11 14:37:04,529 13607 INFO ? odoo: addons paths: ['/home/ubuntu/.local/share/Odoo/addons/12.0', '/opt/odoo/odoo/odoo/addons', '/opt/odoo/odoo/addons']
2019-05-11 14:37:04,530 13607 INFO ? odoo: database: default@default:default
2019-05-11 14:37:04,918 13607 INFO ? odoo.addons.base.models.ir_actions_report: Will use the Wkhtmltopdf binary at /usr/local/bin/wkhtmltopdf
2019-05-11 14:37:04,952 13607 INFO ? odoo.addons.base.models.ir_actions_report: Wkhtmltopdf seems to be broken.
2019-05-11 14:37:05,298 13607 INFO ? odoo.service.server: HTTP service (werkzeug) running on erpbiz:8069
```




sudo apt-get install -y npm
sudo ln -s /usr/bin/nodejs /usr/bin/node
sudo npm install -g less less-plugin-clean-css
sudo apt-get install node-less
STEP 5
sudo apt-get install python-software-properties
sudo vim /etc/apt/sources.list.d/pgdg.list
add a line for the repository
deb http://apt.postgresql.org/pub/repos/apt/ xenial-pgdg main
wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -
sudo apt-get update
sudo apt-get install postgresql-9.6
STEP 6
Create Database user for Odoo
sudo su postgres
cd
createuser -s odoo
createuser -s ubuntu_user_name
exit
STEP 7
Create Odoo user and group
sudo adduser --system --home=/opt/odoo --group odoo
STEP 8
Install Gdata
cd /opt/odoo
sudo wget https://pypi.python.org/packages/a8/70/bd554151443fe9e89d9a934a7891aaffc63b9cb5c7d608972919a002c03c/gdata-2.0.18.tar.gz
sudo tar zxvf gdata-2.0.18.tar.gz
sudo chown -R odoo: gdata-2.0.18
sudo -s
cd gdata-2.0.18/
python setup.py install
exit
STEP 9
Odoo 11 Download from GitHub
cd /opt/odoo
sudo apt-get install git
sudo su - odoo -s /bin/bash
git clone https://www.github.com/odoo/odoo --depth 1 --branch 12.0 --single-branch
exit
STEP 10
Create Odoo Log File
sudo mkdir /var/log/odoo
sudo chown -R odoo:root /var/log/odoo
STEP 11
Edit Odoo configuration file
sudo gedit/etc/odoo.conf

#Copy this lines and change with users and password 
------------------------------------

[options]

; This is the password that allows database operations:

; admin_passwd = admin

db_host = False

db_port = False

db_user = odoo

db_password = False

logfile = /var/log/odoo/odoo-server.log

addons_path = /opt/odoo/addons,/opt/odoo/odoo/addons

---------------------------------------------------

sudo chown odoo: /etc/odoo.conf


sudo chown odoo: /etc/odoo.conf
STEP 12
sudo apt-get -f install
sudo wget https://github.com/wkhtmltopdf/wkhtmltopdf/releases/download/0.12.1/wkhtmltox-0.12.1_linux-trusty-amd64.deb
sudo dpkg -i wkhtmltox-0.12.1_linux-trusty-amd64.deb
sudo cp /usr/local/bin/wkhtmltoimage /usr/bin/wkhtmltoimage
sudo cp /usr/local/bin/wkhtmltopdf /usr/bin/wkhtmltopdf
STEP 13
Run Odoo Server
cd /opt/odoo/odoo

./odoo-bin
STEP 14
Open browser on :
http://localhost:8069

STEP 15

cd /usr/local/lib/
sudo git clone https://github.com/sass/sassc.git --branch 3.4.2 --depth 1
sudo git clone https://github.com/sass/libsass.git --branch 3.4-stable --depth 1
sudo git clone https://github.com/sass/sass-spec.git --depth=1

STEP 16
echo 'SASS_LIBSASS_PATH="/usr/local/lib/libsass"' | sudo tee -a /etc/environment
source /etc/environment

STEP 17
sudo make -C libsass

STEP 18
sudo make -C sassc
sudo make -C sassc install

STEP 19 
Restart Odoo Server

#CREDIT :
https://github.com/mtsoftware2016/odoo-12/blob/master/guilde_installation_for_ubuntu_16.04.txt
