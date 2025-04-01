## Minimum hardware requirements

Video Indexer enabled by Arc is designed to run on any Arc enabled Kubernetes environment.

>[!NOTE]
> The following table covers minimum requirements for a *production* environment. We recommend at least a two-node cluster for high availability and scalability. The recommended settings refer to cluster-wide settings. So for example, if you have two nodes, each node should have 16 cores and 32 GB of RAM. We recommend creating a dedicated node-pool or autoscaling groups to host the VI solution.


| Configuration | Virtual machine count | Node CPU cores count  | Node RAM | Node storage | Remarks
| --- | --- | --- | --- | --- | --- |
| Minimum | One | 32 Cores | 64 GB | 50 GB | Storage needs to support `ReadWriteMany` Storage Class |
| Recommended | Two | 48-64 Cores | 256 GB | 100 GB | Storage needs to support `ReadWriteMany` Storage Class |
