# anchore-engine-openshift

OpenShift Template for [Anchore Engine](https://github.com/anchore/anchore-engine) deployment.

Due to a type of operations which engine performs (e.g. extracting filesystem with subsequent mknod call) it requires escalated oc policies attached to sa.

**Please keep in mind that it is _not recommended_ to use such privileged sa**

Easiest way to create appropriate SA:

```
oc project [namespace]
oc create sa anchore-engine
oc export scc anyuid > anyuid-scc-anchore-engine.yaml

remove explicit policy restrcitions
remove users
change scc name

oc create -f anyuid-scc-anchore-engine.yaml
oc adm policy add-scc-to-user anyuid-anchore-engine system:serviceaccount:[namespace]:anchore-engine
```
