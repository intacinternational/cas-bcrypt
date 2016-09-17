Rails-Devise - CAS Overlay Template
================================

> 2015-11-25T11:29-0500

Java CAS (Centralized Authentication Service) server implementing BCrypt capable validation for use with a Rails/Devise based backend.

# Deployment

```
$ vi etc/cas.properties 
$ brew install tomcat
$ sudo mkdir -p /etc/cas/logs
$ chmod  ug+rw,o-rwx -R /etc/cas
$ # copy all cas configuration to /etc/cas
$ cp -R etc/* /etc/cas/
$ # build cas war
$ mvn clean package
$ # deploy target/cas.war to tomcat
$ cp target/cas.war /usr/local/Cellar/tomcat/8.5.5/libexec/webapps/
$ # run tomcat
$ /usr/local/Cellar/tomcat/8.5.5/bin/catalina run
```

# CAS Original README 

Generic CAS maven war overlay to exercise the latest versions of CAS. This overlay could be freely used as a starting template for local CAS maven war overlays.

## Versions
```xml
<cas.version>4.1.2</cas.version>
```

## Requirements
* JDK 1.7+

## Configuration 
The `etc` directory contains the configuration files that need to be copied to `/cas/etc`. 

Current files are:

* `cas.properties`
* `log4j2.xml`

## Build

```bash
mvnw clean package
```

or

```bash
mvnw.bat clean package
```

## Deployment

### Embedded Jetty

* Create a Java keystore at `/etc/cas/jetty/thekeystore` with the password `changeit`. 
* Import your CAS server certificate inside this keystore.

```bash
mvnw jetty:run-forked
```

CAS will be available at:

* `http://cas.server.name:8080/cas`
* `https://cas.server.name:8443/cas`

### External
Deploy resultant `target/cas.war` to a Servlet container of choice.
