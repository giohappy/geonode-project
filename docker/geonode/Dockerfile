FROM giohappy/geonode-base:latest-ubuntu-22.04
LABEL GeoNode development team

RUN mkdir -p /usr/src/geonode_project

# add bower and grunt command
COPY src /usr/src/geonode_project/
WORKDIR /usr/src/geonode_project

#COPY src/monitoring-cron /etc/cron.d/monitoring-cron
#RUN chmod 0644 /etc/cron.d/monitoring-cron
#RUN crontab /etc/cron.d/monitoring-cron
#RUN touch /var/log/cron.log
#RUN service cron start

COPY src/wait-for-databases.sh /usr/bin/wait-for-databases
RUN chmod +x /usr/bin/wait-for-databases
RUN chmod +x /usr/src/geonode_project/tasks.py \
    && chmod +x /usr/src/geonode_project/entrypoint.sh

COPY src/celery-cmd /usr/bin/celery-cmd
RUN chmod +x /usr/bin/celery-cmd

# Install "geonode-contribs" apps
# RUN cd /usr/src; git clone https://github.com/GeoNode/geonode-contribs.git -b master
# Install logstash and centralized dashboard dependencies
# RUN cd /usr/src/geonode-contribs/geonode-logstash; pip install --upgrade  -e . \
#     cd /usr/src/geonode-contribs/ldap; pip install --upgrade  -e .

RUN yes w | pip install --src /usr/src -r requirements.txt

# Cleanup apt update lists
RUN apt-get autoremove --purge &&\
    apt-get clean &&\
    rm -rf /var/lib/apt/lists/*

# Export ports
EXPOSE 8000

# We provide no command or entrypoint as this image can be used to serve the django project or run celery tasks
# ENTRYPOINT /usr/src/geonode_project/entrypoint.sh
