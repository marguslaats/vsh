# Ülesanne 
Ülesandeks on installida php 7 ning php 5, mysql(5.6) seejärel seadistada nii, et oleks võimalik kontrollida läbi veebilehitseja. Tuleb koostada skript, mis jälgib kas see töötab või ei tööta. Järgmiseks tuli masin seadistada nii, et see kasutaks HTTPS protokolli.

# Käsud 
Apt-get install php5 - instaleerib arvutisse php 5 utiliidid.

wget -q https://packages.sury.org/php/apt.gpg -O- | sudo apt-key add - installeerib php7 utiliidid virtuaalarvutisse.

wget https://repo.mysql.com//mysql-apt-config_0.8.9-1_all.deb

apt-get install mysql-server installeerib mysql 5.6 virtuaalarvutisse.

apt install phpmyadmin - installeerib veebiliidese jaoks vajalikud utiliidid

Kontrollimiseks läksin lehele 172.23.13.48/index.php

# Käsud HTTPS protokolli kasutamiseks 
openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/ssl/private/apache-selfsigned.key -out /etc/ssl/certs/apache-selfsigned.crt - See käsk loob SSL sertifikaadi.

Cp /etc/apache2/sites-available/default-ssl.conf /etc/apache2/sites-available/default-ssl.conf.bak - See käsk teeb default-ssl.conf failist tagavara koopia juhuks, kui seda peaks vaja minema.

nano /etc/apache2/sites-available/default-ssl.conf

Fail peaks nägema lõpuks välja umbes selline:

<VirtualHost _default_:443>
        ServerAdmin your_email@example.com
        ServerName server_domain_or_IP

        DocumentRoot /var/www/html

        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined

        SSLEngine on

        SSLCertificateFile      /etc/ssl/certs/apache-selfsigned.crt
        SSLCertificateKeyFile /etc/ssl/private/apache-selfsigned.key

        <FilesMatch "\.(cgi|shtml|phtml|php)$">
                        SSLOptions +StdEnvVars
        </FilesMatch>
        <Directory /usr/lib/cgi-bin>
                        SSLOptions +StdEnvVars
        </Directory>

        BrowserMatch "MSIE [2-6]" \
                       nokeepalive ssl-unclean-shutdown \
                       downgrade-1.0 force-response-1.0

</VirtualHost>
/etc/apache2/sites-available/000-default.conf faili tuli lisada juurde järgnev rida:

Redirect permanent "/" "https://(Siia veebilehe URL või IP)/"

Need käsud panevad tööle vajalikud moodulid ja konfiguratsioonifailid:

a2enmod ssl

a2enmod headers

a2ensite default-ssl

Täispikka õpetust koos lisainfoga saab lugeda siit : https://www.digitalocean.com/community/tutorials/how-to-create-a-self-signed-ssl-certificate-for-apache-in-ubuntu-16-04

# Wordpressi installeerimiseks 

WordPressi allalaadimiseks /var/www/html kausta:

cd /var/www/html/

wget http://wordpress.org/latest.zip

aptitude install unzip - installib utiliidi, mis pakib lahti faile

unzip -q latest.zip

Õiguste Määramine: 

chown -R www-data:www-data /var/www/html/wordpress

chmod -R 755 /var/www/html/wordpress

Uplad kausta tegemine

mkdir -p /var/www/html/wordpress/wp-content/uploads

Õiguste andmine, et saaks kirjutada wordpressi kausta

chown -R www-data:www-data /var/www/html/wordpress/wp-content/uploads

Mysql seadistamine wordpressi jaoks

mysql -u root -p

CREATE DATABASE wordpress;

CREATE USER user@localhost IDENTIFIED BY 'qwerty';

GRANT ALL PRIVILEGES ON wordpress.* TO user@localhost;

FLUSH PRIVILEGES;

MySql-ist lahkumiseks

exit;
