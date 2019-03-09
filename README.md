# open-ripple  

This repository is created to collect all the information about installing and configuring ripple server.
This guide is based on old ripple guides (https://github.com/osuripple/ripple/wiki) and my personal experience.
1. GNU/Linux  
I don’t know is it possible to setup a server on Windows (you can try) but I use Ubuntu and it works well.

2. Dependencies  
* Mysql
* Redis
* Php-fpm
* Go
* python
* nginx
* Ripple code

3. Certificate  
Edit openssl.cnf and run gencert.sh to generate certificates. Use cert.pem and key.pem in your nginx configuration and cert.pem in your switcher.  

4. Proxy  
Edit and include ripple.conf in your nginx.conf  

5. Database  
Use database.sql  

6. Some reminders/for-copypase-commands  

* User creation
```
adduser semyon422
usermod -aG sudo semyon422
```
* All dependencies
```
sudo apt install sudo
sudo apt install gcc g++ build-essential
sudo apt install python3.5 python3-pip
sudo apt install git
sudo apt install mysql-server
sudo apt install redis-server
sudo apt install libmariadbclient-dev
sudo apt install vsftpd
sudo apt install nginx
sudo apt install redis-server
sudo apt install php-fpm
sudo apt install composer
sudo apt install php7.0-mbstring
sudo apt install php7.0-curl
sudo apt install php-mysql
```
* Server enable/start/restart
```
sudo systemctl enable vsftpd
sudo systemctl enable nginx
sudo systemctl enable php7.0-fpm
sudo systemctl enable redis-server
sudo systemctl start vsftpd
sudo systemctl start nginx
sudo systemctl start php7.0-fpm
sudo systemctl start redis-server
sudo systemctl restart vsftpd
sudo systemctl restart nginx
sudo systemctl restart php7.0-fpm
sudo systemctl restart redis-server
```
* Server configuring
```
sudo nano /etc/vsftpd.conf (allow write for local users)
sudo mysql_secure_installation
mysql -u root -p
GRANT ALL PRIVILEGES ON *.* TO 'username' IDENTIFIED BY 'password';
sudo nano /etc/mysql/mariadb.conf.d/50-server.cnf (comment "bind-address = 127.0.0.1")
```
* Repository clonning
```
git clone --recursive https://github.com/semyon422/open-ripple
git clone --recursive https://github.com/osufx/pep.py
git clone --recursive https://github.com/osufx/lets
git clone --recursive https://zxq.co/ripple/rippleapi
git clone --recursive https://zxq.co/ripple/hanayo
git clone --recursive https://github.com/osuripple/old-frontend (will clone with error due to secret module)
```
* pep.py
```
sudo pip install -r requirements.txt
python3 setup.py build_ext --inplace
python3 pep.py
nano config.ini
```
* lets
```
sudo pip install -r requirements.txt
python3 setup.py build_ext --inplace
python3 lets.py
nano config.ini
```
* hanayo
```
go get zxq.co/ripple/hanayo
nano hanayo.conf
```
* rippleapi
```
go get zxq.co/ripple/rippleapi
nano api.conf
```
* old-frontend (for Ripple Admin Panel)
```
composer install
nano inc/config.php
nano inc/functions.php (remove requiring secret module)
```
* Avatar server
```
pip3 install flask
mkdir avatars
python3 avatarserver.py
```
* Golang 1.10 installation
```
wget https://dl.google.com/go/go1.10.linux-amd64.tar.gz
tar -xvf go1.10.linux-amd64.tar.gz
sudo mv go /usr/lib/go-1.10
nano ~/.bashrc
export PATH=/usr/lib/go-1.10/bin:$PATH
export GOPATH=$HOME/go
export PATH=$PATH:$GOPATH/bin
export GOBIN=$GOPATH/bin
source ~/.bashrc
```
7. Trouble solving
```
go: signal: killed
dmesg -> Out of memory
solution: stop all servers and try again
```
