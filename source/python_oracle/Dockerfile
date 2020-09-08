FROM centos/python-38-centos7
MAINTAINER Sreenivasulu Bachu <bsrvasulu@yahoo.com>
USER root

RUN mkdir /apps/testApp/ -p
WORKDIR /apps/testApp/

RUN pip install mail_alert
RUN pip install pandas
RUN pip install cx_Oracle --upgrade
RUN pip install pika

RUN useradd -ms /bin/bash testUsr

RUN chgrp -R users /apps
RUN chown -R testUsr /apps
RUN chmod -R 775 /apps

RUN mkdir /opt/oracle -p
WORKDIR /opt/oracle/

RUN wget http://download.oracle.com/otn_software/linux/instantclient/19600/instantclient-basic-linux.x64-19.6.0.0.0dbru.zip
RUN unzip instantclient-basic-linux.x64-19.6.0.0.0dbru.zip
RUN yum install libaio -y
RUN sh -c "echo /opt/oracle/instantclient_19_6 > /etc/ld.so.conf.d/oracle-instantclient.conf"
RUN ldconfig
RUN export LD_LIBRARY_PATH=/opt/oracle/instantclient_19_6:$LD_LIBRARY_PATH

ENV TZ=America/Los_Angeles
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone


USER testUsr

RUN mkdir /apps/testApp/ -p
WORKDIR /apps/testApp/

COPY . .

CMD [ "python", "application_python3.py", "config.json" ]
