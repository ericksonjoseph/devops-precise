# Make sure that nginx is passing php files to the php-fpm socket
copy default to /etc/nginx/sites-enabled/default

# Make sure that php is configured to listen on the socket and that permissions are set to allow connections from a web server
copy www.conf to /etc/php5/fpm/pool.d/www.conf

# Make sure that mysql allows connections from anywhere
copy my.cnf to /etc/mysql/my.cnf
run 'update user set host="%" where user="root" and host="localhost"'

# Additional provisioning
Composer install
sudo apt-get install tmux
sudo apt-get install htop
sudo apt-get install vim
sudo apt-get install curl

# Issues
If socket is missing, mysql-server may not have been installed properly (find ./ -type s)
apt-get purge mysql-server
apt-get install mysql-server
service mysql restart
