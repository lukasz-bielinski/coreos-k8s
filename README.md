#### coreos-k8s
k8s cluster on coreos

####This is configuration for manual installation

####certs:
https://coreos.com/kubernetes/docs/latest/openssl.html

1. install on disk using config for particular node
2. set up loadbalancer for api(haproxy.cfg)
3. create flannel network in etcd:
```
curl -X PUT -d "value={\"Network\":\"10.2.0.0/16\",\"Backend\":{\"Type\":\"vxlan\"}}" "192.168.1.170:2379/v2/keys/coreos.com/network/config"
```
4. create kube-system namespace
```
curl -H "Content-Type: application/json" -XPOST -d'{"apiVersion":"v1","kind":"Namespace","metadata":{"name":"kube-system"}}' "http://127.0.0.1:8080/api/v1/namespaces"
```
5. setup kubectl https://coreos.com/kubernetes/docs/latest/configure-kubectl.html


####TODO:
1. encrypted connections between etcd instances
2. encrypted flanneld
3. encrypted fleet, lochsmithd
4. conformannce tests, now issue with version https://github.com/coreos/coreos-kubernetes/issues/364

#####Config succesfully tested on VM(kvm+libvirt)
