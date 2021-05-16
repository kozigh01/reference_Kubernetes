# That DevOps Guy - Persistent Volumes

youtube Video: [Persistent Volumes on Kubernetes for beginners](https://www.youtube.com/watch?v=ZxC6FwEc9WQ) | [github](https://github.com/marcel-dempers/docker-development-youtube-series/tree/master/kubernetes/persistentvolume)
youtube series: [Kubernetes development guide for beginners](https://www.youtube.com/playlist?list=PLHq1uqvAteVvUEdqaBeMK2awVThNujwMd) | [github](https://github.com/marcel-dempers/docker-development-youtube-series)

## Resources
* Kubernetes docs: [Storage Classes](https://kubernetes.io/docs/concepts/storage/storage-classes/)

## Useful commands
```
# see which StorageClass types are available
$ kubectl get storageclass
$ kubectl describe StorageClass hostpath

# create a new Helm chart
$ helm create postgres

# check the chart for valid syntax
$ helm install <<helm release name here>> ./postgres --debug --dry-run  

# install the chart (must be in the PersistentVolumes directory)
$ helm install <<helm release name here>> ./postgres --namespace db --create-namespace


# check that the database has persistence - assume installed with release name "postgres"
$ kubectl get pod --namespace db  # find the name of the db pod
$ kubectl describe pod postgres-0 --namespace db # find the name of the container in the pod
$ kubectl exec pod/postgres-0 -c postgres --namespace db -it -- bash # attach to the running container
# while inside the container:
  root@x:/# psql postgres --username=admin
  postgres=# CREATE TABLE COMPANY(ID INT PRIMARY KEY NOT NULL, NAME TEXT NOT NULL);
  postgres=# \dt
  postgres=# \q
  root@x:/# exit

# Now kill the pod and a new one will restart
$ kubectl delete pod postgres-0
# Now check that the postgres data was preserved
$ kubectl exec pod/postgres-0 -c postgres --namespace db -it -- bash # attach to the running container
# while inside the container:
  root@x:/# psql postgres --username=admin
  postgres=# \dt  # should see the table created above listed, proving that the PV is working
  postgres=# \q
  root@x:/# exit


# remove the chart
$ helm uninstall <<helm release name here>> --namespace db
```