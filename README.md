#  Fix Mongosync Atlas to Atlas documentation examples to avoid confusion

## Description
The documentation for Atlas to Atlas migration via mongosync has confusing examples (generic for on-prem servers) and a wrong example for SRV connection.
[Documentation](https://www.mongodb.com/docs/cluster-to-cluster-sync/current/connecting/atlas-to-atlas/)

+ First example:
```
cluster0:
mongodb://clusterAdmin:superSecret@clusterOne01.fancyCorp.com:20020,clusterOne02.fancyCorp.com:20020,clusterOne03.fancyCorp.com:20020
cluster1:
mongodb://clusterAdmin:superSecret@clusterTwo01.fancyCorp.com:20020,clusterTwo02.fancyCorp.com:20020,clusterTwo03.fancyCorp.com:20020 
```

+ Correction proposal:
We should use `cluster1Name.ab123.mongodb.net:27017` and `cluster2Name.ab123.mongodb.net:27017` as generic name for an Atlas server name for each case and ensure we replace 27017 as default port instead of 20020 for all the examples on the linked documentation.

Using a generic server and a port different from the Atlas default connection port may cause confusion at the time to connect.

+ SRV final example:
```
 mongosync \
   --cluster0 'mongodb+srv://clusterAdmin:superSecret@clusterOne01.fancyCorp.com:20020/' \
   --cluster1 'mongodb+srv://clusterAdmin:superSecret@clusterTwo01.fancyCorp.com:20020/'
```

## Correction proposal:
This command is incorrect, the SRV connection string doesn't includes the port in Atlas. The correct command should be:
```
mongosync \    
--cluster0 'mongodb+srv://clusterAdmin:superSecret@cluster1name.ab123.mongodb.net/'\   
--cluster1 'mongodb+srv://clusterAdmin:superSecret@cluster2Name.ab123.mongodb.net/' 
```
Let me know if you need any further clarifications on this.
