# RBAC

To view the current set of local role bindings, which show the users and groups that are bound to various roles for the current project:

```
manolete919@DESKTOP-KA8AA9P:~$ oc describe rolebinding.rbac
Name:         admin
Labels:       <none>
Annotations:  <none>
Role:
  Kind:  ClusterRole
  Name:  admin
Subjects:
  Kind  Name   Namespace

----  ----   ---------

  User  user1


Name:         admin-0
Labels:       <none>
Annotations:  <none>
Role:
  Kind:  ClusterRole
  Name:  admin
Subjects:
  Kind  Name   Namespace

----  ----   ---------

  User  user2


Name:         devworkspacedw
Labels:       <none>
Annotations:  <none>
Role:
  Kind:  Role
  Name:  workspace
Subjects:
  Kind   Name                                         Namespace

----   ----                                         ---------

  Group  system:serviceaccounts:user-getting-started


Name:         podview
Labels:       <none>
Annotations:  <none>
Role:
  Kind:  Role
  Name:  podview
Subjects:
  Kind  Name   Namespace

----  ----   ---------

  User  user3


Name:         system:deployers
Labels:       <none>
Annotations:  openshift.io/description:
                Allows deploymentconfigs in this namespace to rollout pods in this namespace.  It is auto-managed by a controller; remove subjects to disa...
Role:
  Kind:  ClusterRole
  Name:  system:deployer
Subjects:
  Kind            Name      Namespace

----            ----      ---------

  ServiceAccount  deployer  user-getting-started


Name:         system:image-builders
Labels:       <none>
Annotations:  openshift.io/description:
                Allows builds in this namespace to push images to this namespace.  It is auto-managed by a controller; remove subjects to disable.
Role:
  Kind:  ClusterRole
  Name:  system:image-builder
Subjects:
  Kind            Name     Namespace

----            ----     ---------

  ServiceAccount  builder  user-getting-started


Name:         system:image-pullers
Labels:       <none>
Annotations:  openshift.io/description:
                Allows all pods in this namespace to pull images from this namespace.  It is auto-managed by a controller; remove subjects to disable.
Role:
  Kind:  ClusterRole
  Name:  system:image-puller
Subjects:
  Kind   Name                                         Namespace

----   ----                                         ---------

  Group  system:serviceaccounts:user-getting-started


Name:         view
Labels:       <none>
Annotations:  <none>
Role:
  Kind:  ClusterRole
  Name:  view
Subjects:
  Kind            Name     Namespace

----            ----     ---------

  ServiceAccount  default  user-getting-started
```

# SERVICE ACCOUNT

```bash
manolete919@DESKTOP-KA8AA9P:~$ oc get sa
NAME                           SECRETS   AGE
builder                        2         29h
default                        2         29h
```

## Create a service account

```bash
oc create sa robot 
```

output

```bash
manolete919@DESKTOP-KA8AA9P:~$ oc create sa robot
serviceaccount/robot created
```

## view the secret for a service account

```bash
oc describe sa robot
```

example

```bash
manolete919@DESKTOP-KA8AA9P:~$ oc describe sa robot
Name:                robot
Namespace:           user-getting-started
Labels:              <none>
Annotations:         <none>
Image pull secrets:  robot-dockercfg-xg8x8
Mountable secrets:   robot-dockercfg-xg8x8
Tokens:              robot-token-bsfdf
Events:              <none>
```

## granting roles

https://docs.openshift.com/container-platform/4.11/authentication/understanding-and-creating-service-accounts.html#service-accounts-granting-roles_understanding-service-accounts

```bash
oc policy add-role-to-user view system:serviceaccount:top-secret:robot
```

example

```bash
manolete919@DESKTOP-KA8AA9P:~$ oc policy add-role-to-user view system:serviceaccount:user-getting-started:robot
clusterrole.rbac.authorization.k8s.io/view added: "system:serviceaccount:user-getting-started:robot"
```

For example, to allow all service accounts in all projects to view resources in the `my-project` project:

```bash
oc policy add-role-to-group view system:serviceaccounts -n my-project
```

Every service account is also a member of two groups:

| Group                            | Description                                             |
| -------------------------------- | ------------------------------------------------------- |
| system:serviceaccounts           | Includes all service accounts in the system.            |
| system:serviceaccounts:<project> | Includes all service accounts in the specified project. |

To allow all service accounts in the `managers` project to edit resources in the `my-project` project:

```bash
oc policy add-role-to-group edit system:serviceaccounts:managers -n my-project
```

