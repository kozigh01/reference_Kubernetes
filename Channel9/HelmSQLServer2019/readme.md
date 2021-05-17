# Use Helm Charts from Windows Client Machine to Deploy SQL Server 2019 Containers on Kubernetes

Channel 9: [Use Helm Charts from Windows Client Machine to Deploy SQL Server 2019 Containers on Kubernetes](https://channel9.msdn.com/Shows/Data-Exposed/Use-Helm-Charts-from-Windows-Client-Machine-to-Deploy-SQL-Server-2019-Containers-on-Kubernetes)
Blog: [Deploy SQL Server on Azure Kubernetes Service cluster via Helm Charts - on a windows client machine!](https://techcommunity.microsoft.com/t5/sql-server/deploy-sql-server-on-azure-kubernetes-service-cluster-via-helm/ba-p/2023375?WT.mc_id=dataexposed-c9-niner)
Github: [mssql-docker](https://github.com/microsoft/mssql-docker/tree/master/linux/sample-helm-chart)

## Useful Commands
```
# see which StorageClass types are available
$ kubectl get storageclass
$ kubectl describe StorageClass hostpath

# Create the Helm Chart
$ helm create sqlserver2019

# check the chart for valid syntax
$ helm install <<helm release name here>> ./postgres --debug --dry-run  

# install the chart (must be in the PersistentVolumes directory)
$ helm install <<helm release name here>> ./postgres --namespace db --create-namespace
$ kubectl describe pod postgres-0 --namespace db # find the name of the container in the pod
$ kubectl exec pod/sqlserver-sqlserver2019-0 -c sqlserver-sqlserver2019 --namespace db -it -- bash # attach to the running container


# check that the database has persistence - assume installed with release name "sqllserver"
$ kubectl get pod --namespace db  # find the name of the db pod


# remove the chart
$ helm uninstall <<helm release name here>> --namespace db
```