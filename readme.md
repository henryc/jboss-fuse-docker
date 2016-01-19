# FUSE Docker image

This project builds a Docker image for [JBoss Fuse](http://www.jboss.org/products/fuse/overview/). 
For installation of this image you must be part of Jboss Developer program. 
(http://www.jboss.org/terms-and-conditions/)
This image content is under RedHat licencing.
(http://www.redhat.com/en/about/licenses)

## Build

    docker build -t jaromirecek/jboss-fuse-dev:6.2.1 .

## Usage

You can then run a Fuse server with the following command:

    docker run -it jaromirecek/jboss-fuse-dev:6.2.1 bin/fuse

Note that the web console will not be accessible since we have not yet defined users that can log into it
and have not exposed the web console port on the docker host.

##Run

    docker run -it -p 8181:8181 jaromirecek/jboss-fuse-dev:6.2.1

The administration console should be available at [http://localhost:8181/hawtio](http://localhost:8181/hawtio)

## Ports Opened by Fuse

You may need to map ports opened by the Fuse container to host ports if you need to access it's services.
Those ports are:

* 8181 - Web access (also hosts the Fuse admin console).
* 8101 - SSH Karaf console access

If you add the ``-p 8181:8181` to your `docker run` command, then you should be able to load [http://localhost:8181/hawtio](http://localhost:8181/hawtio) in your web browser to mange the Fuse server.

If you add the ``-p 8101:8101` to your `docker run` command, then you should be able to ssh into the Karaf container using a command similar to: `ssh admin@localhost -p 8101`

## Ports used by JBoss AMQ

* 61616 - AMQ Openwire port.
* 1883  - AMQ MQTT port.
* 5672  - AMQ AMQP port.
* 61613 - AMQ STOMP port.
* 61617 - AMQ Openwire over SSL port.
* 8883  - AMQ MQTT over SSL port.
* 5671  - AMQ AMQP over SSL port.
* 61614 - AMQ STOMP over SSL port.

## Image internals

This image extends the [`jboss/base-jdk:8`](https://github.com/JBoss-Dockerfiles/base-jdk/tree/jdk8) image which adds the OpenJDK distribution on top of the [`jboss/base`](https://github.com/JBoss-Dockerfiles/base) image. Please refer to the README.md for selected images for more info.

The server is run as the `jboss` user which has the uid/gid set to `1000`.

Fuse is installed in the `/opt/jboss/jboss-fuse` directory.
