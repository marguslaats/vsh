# Ülesanne 
Ülesandeks on installida php 7 ning php 5, mysql(5.6) seejärel seadistada nii, et oleks võimalik kontrollida läbi veebilehitseja. Tuleb koostada skript, mis jälgib kas see töötab või ei tööta.
# Käsud
> Apt-get install php5 - instaleerib arvutisse php 5 utiliidid.
> wget -q https://packages.sury.org/php/apt.gpg -O- | sudo apt-key add - installeerib php7 utiliidid virtuaalarvutisse.
> wget https://repo.mysql.com//mysql-apt-config_0.8.9-1_all.deb
apt-get install mysql-server installeerib mysql 5.6 virtuaalarvutisse.
apt install phpmyadmin - installeerib veebiliidese jaoks vajalikud utiliidid
Kontrollimiseks läksin  lehele 172.23.13.48/index.php

# Käsud HTTPS protokolli kasutamiseks
> openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/ssl/private/apache-selfsigned.key -out /etc/ssl/certs/apache-selfsigned.crt - See käsk loob SSL sertifikaadi.

Cp /etc/apache2/sites-available/default-ssl.conf /etc/apache2/sites-available/default-ssl.conf.bak - See käsk teeb default-ssl.conf failist tagavara koopia juhuks, kui seda peaks vaja minema.


nano /etc/apache2/sites-available/default-ssl.conf 


Fail peaks nägema lõpuks välja umbes selline: 

><IfModule mod_ssl.c>
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
</IfModule>
