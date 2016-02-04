# docker-openldap

[![Build Status](https://travis-ci.org/h0tbird/docker-openldap.svg?branch=master)](https://travis-ci.org/h0tbird/docker-openldap)

Containerized OpenLDAP service.

##### 1. Certificate:

```
mkdir certs && openssl req \
-newkey rsa:4096 -nodes -sha256 -x509 -days 365 \
-subj '/CN=127.0.0.1/O=Localhost LTD./C=US' \
-keyout certs/server-key.pem -out certs/server-crt.pem
```

##### 2. OpenLDAP:

```
docker run -it --rm \
--net host --name openldap \
--volume ${PWD}/certs:/certs \
--env CA_CERT_FILE=/certs/server-crt.pem \
--env CERT_FILE=/certs/server-crt.pem \
--env CERT_KEY_FILE=/certs/server-key.pem \
--env LDAP_UPSTREAM_IP=127.0.0.1 \
--env LDAP_UPSTREAM_SUFFIX=dc=company,dc=com \
--env CONFIG_ROOTDN=cn=config \
--env CONFIG_ROOTPW=secret \
h0tbird/openldap:latest
```
