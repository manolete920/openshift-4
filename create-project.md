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

