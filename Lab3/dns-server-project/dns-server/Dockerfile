FROM ubuntu:latest
RUN yes | apt-get update
RUN yes | apt-get install dnsutils net-tools inetutils-ping bind9
COPY options.txt /etc/bind/options.txt
EXPOSE 53/tcp
CMD service named restart && bash 
