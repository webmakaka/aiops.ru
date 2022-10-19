---
layout: page
title: Machine Learning on Kubernetes - Инсталляция Keycloak
description: Machine Learning on Kubernetes - Инсталляция Keycloak
keywords: Machine Learning on Kubernetes - Инсталляция Keycloak
permalink: /study/books/machine-learning-on-kubernetes/environment/installing-keycloak/
---

# Инсталляция Keycloak

<br/>

```
$ kubectl create ns keycloak
$ kubectl create -f Chapter04/postgresdb/ -n keycloak
```

<br/>

```
$ watch kubectl get pods -n keycloak
```

<br/>

```
$ kubectl create -f Chapter04/keycloak.yaml -n keycloak
```

<br/>

```
$ watch kubectl get pods -n keycloak
```

<br/>

**response:**

```
NAME                        READY   STATUS    RESTARTS   AGE
keycloak-75799d947b-l9mkw   1/1     Running   0          56s
postgres-9db8ff595-vc8x2    1/1     Running   0          2m7s

```

<br/>

```
$ minikube ip --profile ${PROFILE}
192.168.49.2
```

<br/>

```
$ export MINIKUBE_IP_ADDR=192.168.49.2
```

<br/>

```
// Check
// $ envsubst < Chapter04/keycloak-ingress.yaml
```

<br/>

```
$ envsubst < Chapter04/keycloak-ingress.yaml | kubectl create -f - -n keycloak
```

<br/>

```
$ kubectl get ingress -n keycloak
NAME       CLASS   HOSTS                          ADDRESS        PORTS     AGE
keycloak   nginx   keycloak.192.168.49.2.nip.io   192.168.49.2   80, 443   4m8s
```

<br/>

// Administration Console
// admin / admin
https://keycloak.192.168.49.2.nip.io/auth/

<br/>

### Importing the Keycloak configuration for the ODH components

```
Keycloak WEB UI -> import -> Chapter05/realm-export.json

- If a resource exists - Skip

Import
```

<br/>

### Creating a Keycloak user

<br/>

```
Users -> Add user ->

Username: mluser
Email: mluser@example.com
First Name: mluser
Last Name: mluser

User Enabled: ON
Email Verified: ON

Groups: ml-group

SAVE
```

<br/>

```
Credentials:

Password: mluser
Password Confirmation: mluser

Temporary: OFF

Set Password
```
