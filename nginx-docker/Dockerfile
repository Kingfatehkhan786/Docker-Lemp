FROM ubuntu:20.04

ENV ITDEVGROUP_TIME_ZONE Asia/Kolkata
RUN ln -snf /usr/share/zoneinfo/$ITDEVGROUP_TIME_ZONE /etc/localtime && echo $ITDEVGROUP_TIME_ZONE > /etc/timezone
RUN apt-get update \  
        &&  apt-get install -y   \
        supervisor \
         nginx \ 
         ca-certificates \ 
         software-properties-common
          
COPY ./supervisord.conf /etc/supervisor/conf.d/supervisord.conf
COPY ./default /etc/nginx/sites-available/default
EXPOSE  80 443
ENTRYPOINT  ["/usr/bin/supervisord"]











