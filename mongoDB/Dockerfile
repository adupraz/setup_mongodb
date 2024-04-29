FROM mongo:latest

RUN chown -R mongodb:mongodb /var/log

ENV TZ=Europe/Paris
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone