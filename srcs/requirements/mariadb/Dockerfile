FROM	debian:bookworm

EXPOSE	3306

RUN		apt update && \
		apt install -y --no-install-recommends --no-install-suggests \
		mariadb-server && \
		rm -rf /var/lib/apt/lists/*

COPY	conf/50-server.cnf /etc/mysql/mariadb.conf.d/

COPY	conf/setup.sh /bin/
RUN		chmod +x /bin/setup.sh

CMD		["setup.sh", "mysqld_safe"]