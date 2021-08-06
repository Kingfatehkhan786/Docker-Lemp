### Nginx 

##### From here the nginx will get executed for docker compose

##### I'm using Ubuntu 20.04 TLS image for running nginx

````
FROM ubuntu:20.04
````

##### for setting up the Indian Time zone env 

```

ENV ITDEVGROUP_TIME_ZONE Asia/Kolkata

RUN ln -snf /usr/share/zoneinfo/$ITDEVGROUP_TIME_ZONE /etc/localtime && echo $ITDEVGROUP_TIME_ZONE > /etc/timezone

```

##### Installing packages 

```
RUN apt-get update \  
        &&  apt-get install -y   \
        supervisor \ 
         ca-certificates \ 
         software-properties-common \ 
         nginx 


```
##### Package Description
* ##### supervisor is a process manager which makes managing a number of long-running programs by providing a consistent interface through which they can be monitored and controlled.

* ##### ca-certificates You might have applications or services, installed on Ubuntu server, that depend upon authorized SSL connections to properly function. Applications like Apache nginx depend upon CAs, in order to serve up HTTPS connections.

* ##### software-properties-common This software provides an abstraction of the used apt repositories. It allows you to easily manage your distribution and independent software vendor software sources.

* ##### Nginx for the web browser 


##### Copying files from source to destination container

```
COPY ./supervisord.conf /etc/supervisor/conf.d/supervisord.conf
COPY ./default /etc/nginx/sites-available/default
```

##### these are modify files which help to run a lemp environment 


##### Exposing port and setting up the ENTRYPOINT for supervisord to run the service or services.

```
EXPOSE  80 443
ENTRYPOINT  ["/usr/bin/supervisord"]
```

