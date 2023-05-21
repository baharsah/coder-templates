FROM ubuntu
ENV TZ=UTC
ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update \
	&& apt-get install -y tzdata software-properties-common \
	&& add-apt-repository ppa:ondrej/php \
	&& apt-get update \
	&& apt-get install -y \
	curl \
	software-properties-common \
	ca-certificates \
	lsb-release \
	apt-transport-https \
	git \
	golang \
	sudo \
	vim \
	wget \
	php8.1 \
	php8.1-mysql \
	php8.1-mbstring \
	php8.1-xml \
	php8.1-curl \
	&& rm -rf /var/lib/apt/lists/*
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php -r "if (hash_file('sha384', 'composer-setup.php') === '55ce33d7678c5a611085589f1f3ddf8b3c52d662cd01d4ba75c0ee0459970c2200a51f492d557530c71c15d8dba01eae') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
RUN php composer-setup.php
RUN php -r "unlink('composer-setup.php');"

ARG USER=coder
RUN useradd --groups sudo --no-create-home --shell /bin/bash ${USER} \
	&& echo "${USER} ALL=(ALL) NOPASSWD:ALL" >/etc/sudoers.d/${USER} \
	&& chmod 0440 /etc/sudoers.d/${USER}
USER ${USER}
WORKDIR /home/${USER}
