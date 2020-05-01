# how_to_setup_innodb_cluster_with_public_and_private_network
this file introduces how to setup mysql innodb cluster with public and private including mysqlrouter . 

there are several key points here :

1. group replication parameter :   report_host  , this should be public ip and  mysqlrouter will use it for client 
2. cluster.createCluster and addInstance :   it needs extra parameter to connect to other ndoes from private network . 
3. mysqlsh : connect to public ip 


shell.connect('root@xxx.51:3306');
shell.connect('root@xxx.52:3306');
shell.connect('root@xxx.53:3306');
dba.configureLocalInstance();

node 3:

var cluster = dba.createCluster('myCluster', {localAddress: "xxx.4"});
 
cluster.addInstance('root@xxx.3:3306',{localAddress: "xxx.3"});
 
cluster.addInstance('root@xxx.2:3306',{localAddress: "xxx.2"});
