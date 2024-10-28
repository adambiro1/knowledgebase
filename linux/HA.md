# HA

```
pcs booth status
```

revoke ticket

```
pcs booth ticket revoke apacheticket
```

grant:

```
pcs booth tucket grant 
```

display the status of the cluster and the cluster resources:

```
pcs status "cluster component"
```

`resources, groups, cluster, nodes, or pcsd`

display the full current cluster configuration:

```
pcs config
```

back-up and restore cls config:

```
pcs config backup filename
```

```
pcs config restore [--local] [filename]
```

resources:

move resource:

```
pcs resource move <resourcegroup> <node>
```

cleans up the resource specified by *resource_id:*

```
pcs resource cleanup resource_id
```

delete failed state: 

```
pcs resource cleanup proxygroup
```

enable proxy resource:

```
pcs resource enable proxygroup
```

restart group:

```
pcs resource restart proxygroup
```