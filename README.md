# README

Create the Astra Control credential secret and the user kubeconfig secret on the master cluster:

```text
kubectl create secret generic astra-control-config --from-file=/Users/mhaigh/.config/astra-toolkits/config.yaml
kubectl create secret generic user-kube-config --from-file=config
```
