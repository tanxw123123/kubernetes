首先找一台服务器安装nfs服务端，最好独立于k8s集群之外  
我这里采用ubuntu 20.04系统安装nfs服务端  
- # apt-get install nfs-kernel-server  
- # cat /etc/exports  
```
/nfs/nginx 10.203.0.0/24(rw,sync,no_root_squash)  # 允许10.203.0.0/24网段访问
```
- # mkdir -p /nfs/nginx  
- # chmod -R 777 /nfs
- # exportfs -arv     #启用并生效

在K8S集群所有节点上安装NFS客户端  
- # apt-get install nfs-common  
开机自动挂载，在/etc/fstab添加，
```
10.203.0.10:/nfs/nginx /data/apps/nginx/html nfs rw 0 0  
```
10.203.0.10为nfs服务器ip  
- # mount -a 

