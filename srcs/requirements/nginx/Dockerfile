FROM	debian:bookworm

EXPOSE	443

# ARG		CERT_FOLDER=/etc/nginx/certs/
# ARG		CERTIFICATE=/etc/nginx/certs/certificate.crt
# ARG		KEY=/etc/nginx/certs/certificate.key
# ARG		COUNTRY=BR
# ARG		STATE=BA
# ARG		LOCALITY=Salvador
# ARG		ORGANIZATION=42
# ARG		UNIT=42
# ARG		COMMON_NAME=login.42.fr

#Mas adelante habrá que comentar lo de arriba (ARG) y descomentar la linea de abajo (para entregar).
ARG		CERT_FOLDER CERTIFICATE KEY COUNTRY STATE LOCALITY ORGANIZATION UNIT COMMON_NAME

RUN		apt update && apt install -y --no-install-recommends --no-install-suggests \
		nginx \
		openssl && \
		rm -rf /var/lib/apt/lists/*

RUN		mkdir -p ${CERT_FOLDER} && \
		openssl req -newkey rsa:4096 -x509 -sha256 -days 365 -nodes \
		-out ${CERTIFICATE} \
		-keyout ${KEY} \
		-subj "/C=${COUNTRY}/ST=${STATE}/L=${LOCALITY}/O=${ORGANIZATION}/OU=${UNIT}/CN=${COMMON_NAME}"


COPY	conf/nginx.conf	/etc/nginx/
COPY	conf/server.conf	/etc/nginx/conf.d/

RUN		echo "\tserver name ${COMMON_NAME};\n\
		\tssl_certificate ${CERTIFICATE};\n\
		\tssl_certificate_key ${KEY};\n\
		}" >> /etc/nginx/conf.d/server.conf

RUN		mkdir -p /var/www/
RUN		chown -R www-data:www-data /var/www/

CMD		["nginx", "-g", "daemon off;"]