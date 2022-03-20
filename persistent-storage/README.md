存储架构
1. pv pvc storageclass
pv － 持久化卷， 支持本地存储和网络存储， 例如hostpath，ceph rbd， nfs等，只支持两个属性， capacity和accessModes。其中capacity只支持size的定义，不支持iops等参数的设定，accessModes有三种，ReadWriteOnce（被单个node读写）， ReadOnlyMany（被多个nodes读）， ReadWriteMany（被多个nodes读写）
pvc — 对pv或者storageclass资源的请求。
storageclass — 另外一种提供存储资源的方式， 提供更多的层级选型， 如iops等参数。 但是具体的参数与提供方是绑定的。 如aws和gce它们提供的storageclass的参数可选项是有不同的。
2. PV的访问模式
ReadWriteOnce：是最基本的方式，可读可写，但只支持被单个Pod挂载。
ReadOnlyMany：可以以只读的方式被多个Pod挂载。
ReadWriteMany：这种存储可以以读写的方式被多个Pod共享。
3. pv plugin
### pv是以plugin的形式来提供支持的，这些plugin所支持的accessmode是不同的。 分别是
| 存储Plugin            | ReadWriteOnce                | ReadOnlyMany   | ReadWriteMany |
|-----------------------|------------------------------|----------------|---------------|
| NFS                   |   支持                       |   支持         |   支持        |
| iSCSI                 |   支持                       |   支持         |  不支持       |
| RBD(ceph block device)|   支持                       |   支持         |  不支持       |
| Glusterfs             |   支持                       |   支持         |   支持        |
| HostPath              |   支持                       |  不支持        |  不支持       |
