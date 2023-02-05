# Utilisez une image Ubuntu comme base
FROM ubuntu:latest

# Mettre à jour la liste des packages
RUN apt-get update

ENV TZ=Europe/Paris
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# Installer Apache2 et OpenSSL
RUN apt-get install -y apache2  

# Copier le fichier index.html
COPY index.html /var/www/html/

# Configurer un virtualhost pour itic.rockstar.com
RUN echo "<VirtualHost *:80>\n\
   ServerName itic.rockstar.com\n\
   ServerAdmin webmaster@itic.rockstar.com\n\
   DocumentRoot /var/www/html/\n\
   ErrorLog ${APACHE_LOG_DIR}/error.log\n\
   CustomLog ${APACHE_LOG_DIR}/access.log combined\n\
</VirtualHost>" > /etc/apache2/sites-available/itic.rockstar.com.conf
#atribution du nom du server
RUN echo "ServerName itic.rockstar.com" >> /etc/apache2/apache2.conf
#desactivation du Vhost par defaut activation du vhost custom et du ssl
RUN a2dissite 000-default.conf
RUN a2ensite itic.rockstar.com.conf

# Exposer le port 80 et 443 pour Apache
EXPOSE 80 443

# Définir la commande pour lancer Apache
CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]