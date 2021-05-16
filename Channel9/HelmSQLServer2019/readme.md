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
```