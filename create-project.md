# Create a Project

```webash
https://docs.openshift.com/container-platform/4.11/getting_started/openshift-cli.html
```

## Web Console

```bash
https://console-openshift-console.apps.cluster-7z6mg.7z6mg.example.opentlc.com/topology/all-namespaces?view=graph
```



## Login

```bash
oc login -u=user1 -p=r3dh4t1! --server=https://api.cluster-7z6mg.7z6mg.example.opentlc.com:6443 --insecure-skip-tls-verify
```

## via token

```bash
oc login --token=sha256~mRL45jlZeQkZJQTdCqr7ZBYKz3FqREKERsQt3TAQs1w --server=https://api.cluster-7z6mg.7z6mg.example.opentlc.com:6443
```

Example

```bash
manolete919@SIS_CEN1_071:~$ oc login -u=user1 -p=r3dh4t1! --server=https://api.cluster-7z6mg.7z6mg.example.opentlc.com:6443 --insecure-skip-tls-verify
Login successful.

You have access to the following projects and can switch between them with 'oc project <projectname>':

  * newapp-user1
    topology-example

Using project "newapp-user1".
```

## Create a project

```bash
oc new-project user-getting-started --display-name="Getting Started with OpenShift"
```

example

```bash
manolete919@SIS_CEN1_071:~$ oc new-project user-getting-started --display-name="Getting Started with OpenShift"
Now using project "user-getting-started" on server "https://api.cluster-7z6mg.7z6mg.example.opentlc.com:6443".

You can add applications to this project with the 'new-app' command. For example, try:

    oc new-app rails-postgresql-example

to build a new example application in Ruby. Or use kubectl to deploy a simple Kubernetes application:

    kubectl create deployment hello-node --image=k8s.gcr.io/e2e-test-images/agnhost:2.33 -- /agnhost serve-hostname
```

# Git

```bash
D:\OpenShift\openshift-4>git remote add origin https://github.com/manolete920/openshift-4.git
D:\OpenShift\openshift-4>git remote -v
origin  https://github.com/manolete920/openshift-4.git (fetch)
origin  https://github.com/manolete920/openshift-4.git (push)

D:\OpenShift\openshift-4>git ls-remote
From https://github.com/manolete920/openshift-4.git
898140018df9828d6412d73ba93b20ee5a54337a        HEAD
898140018df9828d6412d73ba93b20ee5a54337a        refs/heads/main

D:\OpenShift\openshift-4>git fetch origin

D:\OpenShift\openshift-4>git branch -a
  remotes/origin/main

D:\OpenShift\openshift-4>git pull origin main
From https://github.com/manolete920/openshift-4
 * branch            main       -> FETCH_HEAD
```

## rename branch

```bash
git checkout main
git push --set-upstream origin main
```

## delete

```bash
D:\OpenShift\openshift-4>git branch -D main
Deleted branch main (was 8981400).
```

## Rename master to main

```bash
D:\OpenShift\openshift-4>git branch -M main

D:\OpenShift\openshift-4>git branch -a
* main
  remotes/origin/main
```

---

```
git push --set-upstream origin main
```

...

```bash
D:\OpenShift\openshift-4>git add .

D:\OpenShift\openshift-4>git commit -m "initial commit"
On branch main
nothing to commit, working tree clean

D:\OpenShift\openshift-4>git push
fatal: The current branch main has no upstream branch.
To push the current branch and set the remote as upstream, use

    git push --set-upstream origin main

To have this happen automatically for branches without a tracking
upstream, see 'push.autoSetupRemote' in 'git help config'.


D:\OpenShift\openshift-4>git push --set-upstream origin main
Enumerating objects: 4, done.
Counting objects: 100% (4/4), done.
Delta compression using up to 4 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 1.17 KiB | 66.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
To https://github.com/manolete920/openshift-4.git
   8981400..558d12e  main -> main
branch 'main' set up to track 'origin/main'.

D:\OpenShift\openshift-4>git push
Everything up-to-date
```

# Permission to a Default service account

To add the view role to the default service account in the `user-getting-started project`, enter the following command:

```bash
oc adm policy add-role-to-user view -z default -n user-getting-started
```

example

```bash
manolete919@SIS_CEN1_071:~$ oc adm policy add-role-to-user view -z default -n user-getting-started
clusterrole.rbac.authorization.k8s.io/view added: "default"
```

# Deploy an application

[Command-line walkthrough | Getting started | OpenShift Container Platform 4.11](https://docs.openshift.com/container-platform/4.11/getting_started/openshift-cli.html)

```bash
oc new-app quay.io/openshiftroadshow/parksmap:latest --name=parksmap -l 'app=national-parks-app,component=parksmap,role=frontend,app.kubernetes.io/part-of=national-parks-app'
```

output

```bash
manolete919@SIS_CEN1_071:~$ oc new-app quay.io/openshiftroadshow/parksmap:latest --name=parksmap -l 'app=national-parks-app,component=parksmap,role=frontend,app.kubernetes.io/part-of=national-parks-app'
--> Found container image 0c2f55f (22 months old) from quay.io for "quay.io/openshiftroadshow/parksmap:latest"

    * An image stream tag will be created as "parksmap:latest" that will track this image

--> Creating resources with label app=national-parks-app,app.kubernetes.io/part-of=national-parks-app,component=parksmap,role=frontend ...
    imagestream.image.openshift.io "parksmap" created
    deployment.apps "parksmap" created
    service "parksmap" created
--> Success
    Application is not exposed. You can expose services to the outside world by executing one or more of the commands below:
     'oc expose service/parksmap'
    Run 'oc status' to view your app.
```

# Check the service created

```bash
oc get service
```

example

```bash
manolete919@SIS_CEN1_071:~$ oc get service
NAME       TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)    AGE
parksmap   ClusterIP   172.30.75.71   <none>        8080/TCP   117s
```

# Route

## Create Rout

```bash
oc create route edge parksmap --service=parksmap
```

example

```bash
manolete919@SIS_CEN1_071:~$ oc create route edge parksmap --service=parksmap
route.route.openshift.io/parksmap created
```

## Retrieve the route

```bash
oc get route
```

example

```bash
manolete919@SIS_CEN1_071:~$ oc get route
NAME       HOST/PORT                                                                    PATH   SERVICES   PORT       TERMINATION   WILDCARD
parksmap   parksmap-user-getting-started.apps.cluster-7z6mg.7z6mg.example.opentlc.com          parksmap   8080-tcp   edge          None
```

## get pods

```bash
manolete919@SIS_CEN1_071:~$ oc get pods
NAME                        READY   STATUS    RESTARTS   AGE
parksmap-77874c6bb8-wgwzn   1/1     Running   0          11m
```

# Scale application

## up

```bash
oc scale --current-replicas=1 --replicas=2 deployment/parksmap
```

output

```bash
manolete919@SIS_CEN1_071:~$ oc scale --current-replicas=1 --replicas=2 deployment/parksmap
deployment.apps/parksmap scaled
manolete919@SIS_CEN1_071:~$ oc get pods
NAME                        READY   STATUS    RESTARTS   AGE
parksmap-77874c6bb8-dhlxg   1/1     Running   0          12s
parksmap-77874c6bb8-wgwzn   1/1     Running   0          32m
```

## down

```bash
oc scale --current-replicas=2 --replicas=1 deployment/parksmap
```

# Backend application

```bash
oc new-app python~https://github.com/openshift-roadshow/nationalparks-py.git --name nationalparks -l 'app=national-parks-app,component=nationalparks,role=backend,app.kubernetes.io/part-of=national-parks-app,app.kubernetes.io/name=python' --allow-missing-images=true
```

output

```bash
manolete919@SIS_CEN1_071:~$ oc new-app python~https://github.com/openshift-roadshow/nationalparks-py.git --name nationalparks -l 'app=national-parks-app,component=nationalparks,role=backend,app.kubernetes.io/part-of=national-parks-app,app.kubernetes.io/name=python' --allow-missing-images=true
warning: Cannot check if git requires authentication.
--> Found image 43bfd08 (6 days old) in image stream "openshift/python" under tag "3.9-ubi8" for "python"

    Python 3.9
    ----------
    Python 3.9 available as container is a base platform for building and running various Python 3.9 applications and frameworks. Python is an easy to learn, powerful programming language. It has efficient high-level data structures and a simple but effective approach to object-oriented programming. Python's elegant syntax and dynamic typing, together with its interpreted nature, make it an ideal language for scripting and rapid application development in many areas on most platforms.

    Tags: builder, python, python39, python-39, rh-python39

    * A source build using source code from https://github.com/openshift-roadshow/nationalparks-py.git will be created
      * The resulting image will be pushed to image stream tag "nationalparks:latest"
      * Use 'oc start-build' to trigger a new build

--> Creating resources with label app=national-parks-app,app.kubernetes.io/name=python,app.kubernetes.io/part-of=national-parks-app,component=nationalparks,role=backend ...
    imagestream.image.openshift.io "nationalparks" created
    buildconfig.build.openshift.io "nationalparks" created
    deployment.apps "nationalparks" created
    service "nationalparks" created
--> Success
    Build scheduled, use 'oc logs -f buildconfig/nationalparks' to track its progress.
    Application is not exposed. You can expose services to the outside world by executing one or more of the commands below:
     'oc expose service/nationalparks'
    Run 'oc status' to view your app.
```

## route

```bash
oc create route edge nationalparks --service=nationalparks
```

output

```bash
manolete919@SIS_CEN1_071:~$ oc create route edge nationalparks --service=nationalparks
route.route.openshift.io/nationalparks created
```

