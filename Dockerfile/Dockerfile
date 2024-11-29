# Crea una nueva imagen a partir de Ubuntu, última versión

FROM ubuntu:latest

# Información
LABEL \
	authors="eercilla" \
	version="1.0" \
	description="Ubuntu"

# Ejecutamos diferentes comandos
# Encadenamos en un mismo RUN mediante la \
RUN \
	apt-get update && \
	apt-get upgrade -y && \
	apt-get install -y nano && \
	apt-get install -y apache2 && \
	apt-get install -y apache2-utils && \
	a2enmod ssl

# Copiamos todos los ficheros que necesitamos
COPY 	html/. /var/www/html/
COPY	servidor.pem /etc/ssl/certs/
COPY	servidor.key /etc/ssl/private/
COPY	apache2.conf /etc/apache2/
COPY	sites-available/. /etc/apache2/sites-available/
COPY	htpasswd /etc/apache2/


# Habilitamos el site necesario, teniendo que hacerlo despúes de haber copiado
# el fichero en sites-available y reiniciamos Apache
RUN		a2ensite virtualhost.conf && \
		service apache2 restart

# Indica los puertos que utiliza la imagen
# para que los mapeemos al crear el contenedor
EXPOSE 80
EXPOSE 443

# Comando por defecto para ejecutar cuando se inicie el
# contenedor e iniciar Apache con él
CMD ["apache2ctl", "-D", "FOREGROUND"]