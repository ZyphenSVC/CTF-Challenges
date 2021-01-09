FROM ubuntu:18.04

RUN apt-get update -y && apt-get install -y \
    lib32z1 xinetd python3 python3-pip python3-dev libssl-dev libffi-dev wget git make procps libpcre3-dev libdb-dev libxt-dev libxaw7-dev

RUN useradd -m ctf

WORKDIR /home/ctf

RUN cp -R /lib* /home/ctf && \
    cp -R /usr/lib* /home/ctf

RUN mkdir /home/ctf/dev && \
    mknod /home/ctf/dev/null c 1 3 && \
    mknod /home/ctf/dev/zero c 1 5 && \
    mknod /home/ctf/dev/random c 1 8 && \
    mknod /home/ctf/dev/urandom c 1 9 && \
    chmod 666 /home/ctf/dev/*

RUN mkdir /home/ctf/bin && \
    cp /bin/sh /home/ctf/bin && \
    cp /bin/ls /home/ctf/bin && \
    cp /bin/cat /home/ctf/bin

COPY ./ctf.xinetd /etc/xinetd.d/ctf
COPY ./start.sh /start.sh
RUN echo "Blocked by ctf_xinetd" > /etc/banner_fail

RUN chmod +x /start.sh

RUN pip3 install requests numpy

COPY mastercrypto.py /home/ctf/mastercrypto.py
COPY flag.txt /home/ctf/flag.txt
COPY actualflag.txt /home/ctf/actualflag.txt
COPY funroom.txt /home/ctf/funroom.txt
COPY link.txt /home/ctf/link.txt
COPY master.txt /home/ctf/master.txt

CMD ["/start.sh"]

EXPOSE 9999