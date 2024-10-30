# authentication

### log in to OCP

log in via commandline

```
oc login -u <username> -p <passwd>
```

log in to specific cluster:

```
oc login -u <user> -p <passwd> https://api.ocp4.example.com:6443
```

verify the server you are logged into:

```
oc whoami --show-server
```

check that the pod responsible for the OpenShift web console is available:

```
oc get pods -n openshift-console | grep console
```

find the route to the OpenShift web console:

```
oc get routes console -n openshift-console -o jsonpath='{"https://"}{.spec.host}{"\n"}'
```

show console:

```
oc whoami --show-console
```

list all OpenShift clusters you have logged into:

```
oc config get-clusters
```

get a list of all contexts that have ever been created:

```
oc config get-contexts
```

view the current context:

```
oc whoami --show-context
```




### authentication general

**oc get|describe|edit|delete**

```
authentications.config.openshift.io
authentications.operator.openshift.io
```

### internal OAuth server

**oc get|describe|edit|delete**

```
oauths.config.openshift.io
oauthclients.oauth.openshift.io
oauthclientauthorizations.oauth.openshift.io
oauthaccesstokens.oauth.openshift.io
oauthauthorizetokens.oauth.openshift.io
useroauthaccesstokens.oauth.openshift.io
```

### users, groups, identities and useridentitymappings:

**oc get|describe|edit|delete**

```
identities.user.openshift.io
users.user.openshift.io
useridentitymappings.user.openshift.io
groups.user.openshift.io
```

### rbac:

```
roles.rbac.authorization.k8s.io
rolebindings.rbac.authorization.k8s.io
## cluster-wide
clusterroles.rbac.authorization.k8s.io
clusterrolebindings.rbac.authorization.k8s.io

```

**check who can do what**:

```
oc adm policy who-can edit cluster
```

create local role:

```
oc create role <name> --verb=<verb> --resource=<resource> -n <project>
```

add local role to user:

```
oc adm policy add-role-to-user <rolename> <user> --role-namespace=<project> -n <project>
```

add local role to group:

```
oc adm policy add-role-to-group <rolename> <group> --role-namespace=<project> -n <project>
```

create cluster role:

```
oc create clusterrole <name> --verb=<verb> --resource=<resource>
```

add cluster role to a user:

```
oc adm policy add-cluster-role-to-user <role> <username>
```

remove cluster role from user:

```
oc adm policy remove-cluster-role-from-user <role> <username>
```

add cluster role to  a group:

```
oc adm policy add-cluster-role-to-group <role> <groupname>
```

remove cluster role from a group:

```
oc adm policy remove-cluster-role-from-group <role> <groupname>
```

## Service accounts:

**oc get|describe|edit|delete**

```
serviceaccounts ## or just sa
```

add role to a service account(z is needed):

```
oc policy add-role-to-user <role_name> -z <service_account_name>
```



## scc: **security context constraints**

**oc get|describe|edit|delete**

```
securitycontextconstraints.security.openshift.io
```

check pods scc:

```
oc get pod <pod_name> -o jsonpath='{.metadata.annotations.openshift\.io\/scc}{"\n"}'
```