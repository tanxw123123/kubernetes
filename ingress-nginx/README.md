deploy.yaml,搜索Deployment （dnsPolicy）并修改
1. dnsPolicy换成ClusterFirstWithHostNet
2. 新加 hostNetwork: true
3. 新加 nodeName: k8snode1 ，指定部署到k8snode1
4. 新加
tolerations: 
- key: node-role.kubernetes.io/master
  operator: Exists

如下：
spec:              
  dnsPolicy: ClusterFirstWithHostNet  #既能使用宿主机DNS，又能使用集群DNS
  hostNetwork: true                   #与宿主机共享网络
  nodeName: k8snode1              #设置只能在k8snode1节点运行
  tolerations:  					  #设置能容忍master污点
  - key: node-role.kubernetes.io/master
    operator: Exists

Kubernetes-v1.22+ 需要使用 ingress-nginx>=1.0，因为 networking.k8s.io/v1beta 已经移除
### Support Versions table 

| Ingress-NGINX version | k8s supported version        | Alpine Version | Nginx Version |
|-----------------------|------------------------------|----------------|---------------|
| v1.1.2                | 1.23, 1.22, 1.21, 1.20, 1.19 | 3.14.2         |  1.19.9†      |
| v1.1.1                | 1.23, 1.22, 1.21, 1.20, 1.19 | 3.14.2         |  1.19.9†      |
| v1.1.0                | 1.22, 1.21, 1.20, 1.19       | 3.14.2         |  1.19.9†      |
| v1.0.5                | 1.22, 1.21, 1.20, 1.19       | 3.14.2         |  1.19.9†      |
| v1.0.4                | 1.22, 1.21, 1.20, 1.19       | 3.14.2         |  1.19.9†      |
| v1.0.3                | 1.22, 1.21, 1.20, 1.19       | 3.14.2         |  1.19.9†      |
| v1.0.2                | 1.22, 1.21, 1.20, 1.19       | 3.14.2         |  1.19.9†      |
| v1.0.1                | 1.22, 1.21, 1.20, 1.19       | 3.14.2         |  1.19.9†      |
| v1.0.0                | 1.22, 1.21, 1.20, 1.19       | 3.13.5         |  1.20.1       |
| v0.50.0               | 1.21, 1.20, 1.19             | 3.14.2         |  1.19.9†      |
| v0.49.3               | 1.21, 1.20, 1.19             | 3.14.2         |  1.19.9†      |
| v0.49.2               | 1.21, 1.20, 1.19             | 3.14.2         |  1.19.9†      |
| v0.49.1               | 1.21, 1.20, 1.19             | 3.14.2         |  1.19.9†      |
| v0.49.0               | 1.21, 1.20, 1.19             | 3.13.5         |  1.20.1       |
| v0.48.1               | 1.21, 1.20, 1.19             | 3.13.5         |  1.20.1       |
| v0.47.0               | 1.21, 1.20, 1.19             | 3.13.5         |  1.20.1       |
