# K8s_ETCD_Backup_Restore

You can do just the backup of the all the objects in cluster as below but not feasible

```
k get all -A -o yaml > backup.yaml
```

---

Going with the Snapshot option for Backup and Restore

1. Run a pod for Nginx to check

```
kubectl run nginx-pod --image=nginx:latest
```

2. Install Etcd client
```
sudo apt install etcd-client
```

3. Create an environment variable for etcdctl API
```
export ETCDCTL_API=3
```

4. Verify if the etcd client installed by
```
etcdctl snapshot
```

5. Save a Snapshot of the Etcd
```
etcdctl --endpoints=https://127.0.0.1:2379 --cacert=/etc/kubernetes/pki/etcd/ca.crt --cert=/etc/kubernetes/pki/etcd/server.crt  --key=/etc/kubernetes/pki/etcd/server.key snapshot save /opt/etc-backup.db
```

6. Check the backup using
```
du -sh /opt/etc-backup.db
```
![image](https://github.com/user-attachments/assets/88a2ab17-7f66-4f74-afc5-a5a180c58126)

   
```
etcdctl --write-out=table snapshot status /opt/etc-backup.db
```
![image](https://github.com/user-attachments/assets/f0f034d5-a11a-4de6-b0b2-dcfed901fa2a)

![image](https://github.com/user-attachments/assets/9c4f1538-411e-4a8b-998b-2a59aadba795)

