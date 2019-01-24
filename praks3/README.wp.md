# Ülesanne 
Ülesandeks on installida php 7 ning php 5, mysql(5.6) seejärel seadistada nii, et oleks võimalik kontrollida läbi veebilehitseja. Tuleb koostada skript, mis jälgib kas see töötab või ei tööta.
# Käsud
> Apt-get install php5 - instaleerib arvutisse php 5 utiliidid.
> wget -q https://packages.sury.org/php/apt.gpg -O- | sudo apt-key add - installeerib php7 utiliidid virtuaalarvutisse.
> wget https://repo.mysql.com//mysql-apt-config_0.8.9-1_all.deb
apt-get install mysql-server installeerib mysql 5.6 virtuaalarvutisse.
apt install phpmyadmin - installeerib veebiliidese jaoks vajalikud utiliidid
Kontrollimiseks läksin  lehele 172.23.13.48/index.php 

#HTTPS protokolli kasutamiseks 
> tuleks järgida õpetust, mis asub siin: https://www.digitalocean.com/community/tutorials/how-to-create-a-self-signed-ssl-certificate-for-apache-in-ubuntu-16-04
> Järgnevas õpetuses on kõik lihtsalt ja selgelt lahti seletatud, ning antud õpetus töötab ka Ubuntu põhisel süsteemil
> Selleks, et antud õpetus töötaks tuleb kustutada /etc/apache2/conf-available/ssl-params.conf fail, sest see ei ühildu debianiga
