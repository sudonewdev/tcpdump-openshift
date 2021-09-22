# tcpdump-openshift

STEPS:

Patching 
```
oc create serviceaccount tcpdump
oc adm policy add-scc-to-user tcpdump -z privileged
oc patch deployment/<deployment> -p '{"spec":{"template":{"spec": {"containers": [{"name": "<container-name>","securityContext": {"privileged": true}, "serviceAccountName": "tcpdump"}]}}}}'
# collect tcpdump

```
UnPatching
```
# delete sidecar wih helm upgrade 
oc patch deployment/<deployment> -p '{"spec":{"template":{"spec": "serviceAccountName": "default"}]}}}}'
oc delete sa tcpdump ### OPTIONAL
```
