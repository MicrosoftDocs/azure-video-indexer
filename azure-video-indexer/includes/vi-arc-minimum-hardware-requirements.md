---
author: inhenkel
ms.topic: include
ms.date: 07/25/2024
ms.author: inhenkel
---

## Minimum hardware requirements

Video Indexer enabled by Arc is designed to run on any Arc enabled Kubernetes environment.

The following list is the minimum and recommended requirements if the extension contains single language support. If you install multiple speech and translation containers with several languages, increase the hardware requirements accordingly.

>[!NOTE]
> These are minimum requirements for a *production* environment. At least a 2-node cluster is recommended for high availability and scalability. The recommended settings refer to cluster wide settings, so for example, if you have 2 nodes, each node should have 16 cores and 32 GB of RAM.  We recommend creating a dedicated node-pool / auto-scaling groups to host the VI Solution.


| Configuration | VM Count | Node CPU Cores Count  | Node Ram | Node Storage | Remarks
| --- | --- | --- | --- | --- | --- |
| Minimum | 1 | 32 Cores | 64 GB | 50 GB | Storage needs to support `ReadWriteMany` Storage Class |
| Recommended | 2 | 48-64 Cores | 256 GB | 100 GB | Storage needs to support `ReadWriteMany` Storage Class |
