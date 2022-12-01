# README

Create the Astra Control credential secret and the user kubeconfig secret on the master cluster:

```text
kubectl create secret generic astra-control-config --from-file=/Users/mhaigh/.config/astra-toolkits/config.yaml
kubectl create secret generic user-kube-config --from-file=config
```

Apply the Kubernetes job which creates the kubeconfig credential, and then manages the cluster:

```text
kubectl apply -f manage-cluster.yaml
```

Validate that the job ran successfully:

```text
$ kubectl get pods
NAME                         READY   STATUS      RESTARTS   AGE
astra-manage-cluster-5vkjr   0/1     Completed   0          84s
$ kubectl logs astra-manage-cluster-5vkjr | tail -5
WARNING: Running pip as the 'root' user can result in broken permissions and conflicting behaviour with the system package manager. It is recommended to use a virtual environment instead: https://pip.pypa.io/warnings/venv
{"type": "application/astra-credential", "version": "1.1", "id": "5bf45b9d-47c1-46ca-858e-99f60a5ac541", "name": "aks-eastus-cluster", "keyType": "kubeconfig", "valid": "true", "metadata": {"creationTimestamp": "2022-12-01T19:12:45Z", "modificationTimestamp": "2022-12-01T19:12:45Z", "createdBy": "8146d293-d897-4e16-ab10-8dca934637ab", "labels": [{"name": "astra.netapp.io/labels/read-only/credType", "value": "kubeconfig"}, {"name": "astra.netapp.io/labels/read-only/cloudName", "value": "private"}]}}
{"type": "application/astra-cluster", "version": "1.1", "id": "839db36b-1041-4a6d-b732-c0c53b76b8df", "name": "aks-eastus-cluster", "state": "running", "stateUnready": [], "managedState": "unmanaged", "protectionState": "full", "managedStateUnready": [], "inUse": "false", "clusterType": "aks", "namespaces": [], "defaultStorageClass": "45cdaf30-3c02-455f-b2c9-5db37c83f636", "cloudID": "61c68f71-338c-483b-b254-cf7101df1e51", "credentialID": "5bf45b9d-47c1-46ca-858e-99f60a5ac541", "isMultizonal": "false", "tridentManagedStateAllowed": ["unmanaged"], "tridentVersion": "22.10.0", "apiServiceID": "0a94a7db-cef1-4b4c-a3e1-0c975325a5c6", "metadata": {"labels": [], "creationTimestamp": "2022-12-01T19:12:49Z", "modificationTimestamp": "2022-12-01T19:12:49Z", "createdBy": "8146d293-d897-4e16-ab10-8dca934637ab"}}
actoolkit: managing cluster aks-eastus-cluster
{"type": "application/astra-managedCluster", "version": "1.1", "id": "839db36b-1041-4a6d-b732-c0c53b76b8df", "name": "aks-eastus-cluster", "state": "pending", "stateUnready": [], "managedState": "managed", "protectionState": "full", "restoreTargetSupported": "true", "snapshotSupported": "true", "managedStateUnready": [], "managedTimestamp": "2022-12-01T19:12:57Z", "inUse": "false", "clusterType": "aks", "clusterVersion": "1.22", "clusterVersionString": "v1.22.11", "namespaces": [], "defaultStorageClass": "45cdaf30-3c02-455f-b2c9-5db37c83f636", "cloudID": "61c68f71-338c-483b-b254-cf7101df1e51", "credentialID": "5bf45b9d-47c1-46ca-858e-99f60a5ac541", "isMultizonal": "false", "tridentManagedStateAllowed": ["unmanaged"], "tridentVersion": "22.10.0", "apiServiceID": "0a94a7db-cef1-4b4c-a3e1-0c975325a5c6", "metadata": {"labels": [{"name": "astra.netapp.io/labels/read-only/cloudName", "value": "private"}], "creationTimestamp": "2022-12-01T19:12:57Z", "modificationTimestamp": "2022-12-01T19:13:00Z", "createdBy": "8146d293-d897-4e16-ab10-8dca934637ab"}}
```
