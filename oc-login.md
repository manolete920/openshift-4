# INSTALL OC

https://docs.openshift.com/container-platform/4.6/cli_reference/openshift_cli/getting-started-cli.html

```bash
\\130.2.17.251\SIS Info\SIS ARQ\Install
```

* oc-3.11.146 (windows)
* oc-4.11.13-linux.tar.gz

Add oc to the PATH.

# Insecure Registry

C:\Users\mgarciar\.docker\daemon.json

```json
{
  "builder": {
    "gc": {
      "defaultKeepStorage": "20GB",
      "enabled": true
    }
  },
  "debug": false,
  "experimental": false,
  "features": {
    "buildkit": true
  },
  "insecure-registries": [
    "10.31.32.18:8185",
    "10.31.32.18:8186",
    "10.31.32.18:8187",
    "10.31.32.18:8188",
    "10.38.2.76:443",
    "https://registry.okd-apps.conecel.com",
    "https://registry.openshift-apps.dev.conecel.com",
    "https://registry.openshift-apps.conecel.com"
  ]
}
```



# WINDOWS

Conectarme a OpenShift de produccion

```
C:\Users\mgarciar>oc login https://openshift-consola.conecel.com
Authentication required for https://openshift-consola.conecel.com:443 (openshift)
Username: mgarciar
Password:
Login successful.

You have access to 79 projects, the list has been suppressed. You can list all projects with 'oc projects'

Using project "default".

C:\Users\mgarciar>oc get project redhat-sso
NAME         DISPLAY NAME   STATUS
redhat-sso                  Active

C:\Users\mgarciar>oc project redhat-sso
Now using project "redhat-sso" on server "https://openshift-consola.conecel.com:443".

C:\Users\mgarciar>oc get pods
NAME                     READY     STATUS    RESTARTS   AGE
sso-1-hdpvv              1/1       Running   0          25d
sso-postgresql-1-xmbps   1/1       Running   0          97d
```



# LINUX

https://openshift-consola.conecel.com/oauth/token/display

```bash
manolete919@SIS_CEN1_003:~$ oc login --insecure-skip-tls-verify  https://openshift-consola.conecel.com
You must obtain an API token by visiting https://openshift-consola.conecel.com:443/oauth/token/request
manolete919@SIS_CEN1_003:~$ oc login --token=S0RAc3dDlZWctB37ZVKJ8TzMq_j5aXkT70dBaPIemyM --server=https://openshift-consola.conecel.com:443
The server uses a certificate signed by an unknown authority.
You can bypass the certificate check, but any data you send to the server could be intercepted by others.
Use insecure connections? (y/n): y

Logged into "https://openshift-consola.conecel.com:443" as "CN=TIC Manuel Garcia,OU=SIS,OU=REGION-2,OU=USUARIO DE DOMINIO,DC=porta,DC=corp" using the token provided.

You have access to 79 projects, the list has been suppressed. You can list all projects with 'oc projects'

Using project "default".
manolete919@SIS_CEN1_003:~$ oc project redhat-sso
Now using project "redhat-sso" on server "https://openshift-consola.conecel.com:443".
manolete919@SIS_CEN1_003:~$ oc get project redhat-sso
NAME         DISPLAY NAME   STATUS
redhat-sso                  Active
manolete919@SIS_CEN1_003:~$ oc get pods
NAME                     READY   STATUS    RESTARTS   AGE
sso-1-zwvzc              1/1     Running   0          2d
sso-postgresql-1-xmbps   1/1     Running   0          99d
```

## example

```bash
manolete919@SIS_CEN1_003:~$ oc login https://openshift-consola.dev.conecel.com:8443 -u mgarciar -p ECMigra3039.
The server uses a certificate signed by an unknown authority.
You can bypass the certificate check, but any data you send to the server could be intercepted by others.
Use insecure connections? (y/n): y

Login successful.

You have access to 103 projects, the list has been suppressed. You can list all projects with 'oc projects'

Using project "default".
```

# Comandos

```
https://docs.openshift.com/container-platform/3.11/dev_guide/projects.html
```

# Crear Proyecto

```bash
oc new-project claro-components --description="<description>" --display-name="<display_name>"
```

>  El nombre del projecto, debe coincidir con el POM para projectos JAVA.
>
> `<openshiftProjectName>claro-components</openshiftProjectName>` 

```xml
	<properties>
		<maven.compiler.source>${java.version}</maven.compiler.source>
		<maven.compiler.target>${java.version}</maven.compiler.target>
		<project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
		<project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>
		<java.version>1.8</java.version>
		<spring-cloud.version>2020.0.5</spring-cloud.version>
		<openshiftProjectName>claro-components</openshiftProjectName>
		<log4j2.version>2.17.1</log4j2.version>
	</properties>


```

# PERMISOS

```bash
oc policy add-role-to-user admin ocp-deployment -n claro-edx-incubadora
```

# Buscar proyecto

```bash
manolete919@SIS_CEN1_003:~$ oc get projects | grep claro-components
claro-components
```

# Permisos

```bash
oc policy add-role-to-user admin soaint_odeltoro -n claro-miclaroapp-api-soaint
oc policy add-role-to-user admin soaint_yacosta -n claro-miclaroapp-api-soaint
oc policy add-role-to-user admin soaint_odeltoro -n claro-miclaroapp-api-soaint

# service account to a service account
oc adm policy add-role-to-user admin system:serviceaccount:claro-miclaroapp-api-soaint -n claro-miclaroapp-api-soaint


soaint_dvinueza r9834tr9fsoaint_yacosta r43rtr9fsoaint_odeltoro r4j7kpb5

https://openshift-consola.dev.conecel.com:8443/

oc login https://openshift-consola.dev.conecel.com:8443 --token=J1f47vg1o_Knbw60h9RXQHcYDIA1pBCqCi7bMvxWYnU
```

-- 

# Ejecutar job

Construye la imagen y la sube al registry de openshift(**docker-registry.default.svc:5000**/claro-components/microeis-v1**:v1.x.y.z**)

```bash
https://10.31.32.18:8184/job/dev-maven-ci/
```

- [Jenkins](https://10.31.32.18:8184/)
- [dev-maven-ci](https://10.31.32.18:8184/job/dev-maven-ci/)

 [Build with Parameters](https://10.31.32.18:8184/job/dev-maven-ci/build?delay=0sec)

```
https://10.31.32.18:8184/job/dev-maven-ci/build?delay=0sec
```

## input

git

```
http://10.31.32.18:8180/utility-services/micro-sre.git
```

branch

```
soap-support
```

environment: development

output

```
El componente se ha desplegado en la siguiente url: http://10.31.32.18:8185/repository/maven-development/com/claro/frameworks/micro-sre/v1.0.00/micro-sre-v1.0.00.jar, tener en cuenta la siguiente informaci�n para despliegue
<artifactId>micro-sre</artifactId>
<groupId>com.claro.frameworks</groupId>
<version>v1.0.00</version>
```

cd openshift

```
Ejecutando comando oc login -u **** -p **** --insecure-skip-tls-verify  https://okd-consola.conecel.com:443...
```



- [Jenkins](https://10.31.32.18:8184/)
- [dev-maven-cd-openshift](https://10.31.32.18:8184/job/dev-maven-cd-openshift/)

https://10.31.32.18:8184/job/dev-maven-cd-openshift/



```bash
Masking supported pattern matches of $OC_USERNAME or $OC_PASSWORD
[Pipeline] {
[Pipeline] echo
Ejecutando comando oc login -u **** -p **** --insecure-skip-tls-verify  https://openshift-consola.dev.conecel.com:8443...
[Pipeline] sh
expected to call Script6.executeLocalCommand but wound up catching sh; see: https://jenkins.io/redirect/pipeline-cps-method-mismatches/
+ oc login -u **** -p **** --insecure-skip-tls-verify https://openshift-consola.dev.conecel.com:8443
[Pipeline] echo
Ejecutando comando oc whoami -t...
[Pipeline] sh
```

# Pipeline dev-maven-cd-openshift

Esta ejecución requiere parámetros adicionales:

|      | REPOSITORY       |      |      |
| ---- | ---------------- | ---- | ---- |
|      |                  |      |      |
|      | BRANCH           |      |      |
|      |                  |      |      |
|      | ENVIRONMENT      |      |      |
|      |                  |      |      |
|      | PROJECT_NAME     |      |      |
|      |                  |      |      |
|      | ARTIFACT_ID      |      |      |
|      |                  |      |      |
|      | ARTIFACT_VERSION |      |      |
