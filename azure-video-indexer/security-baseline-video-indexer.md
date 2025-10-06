---
title: Secure Azure AI Video Indexer
description: Learn how to secure Azure AI Video Indexer, with best practices for protecting sensitive media data.
author: bandersmsft
ms.author: banders
ms.service: azure-video-indexer
ms.topic: conceptual
ms.collection: ce-skilling-ai-copilot
ms.custom: horz-security
ms.date: 10/06/2025
---

# Secure Azure AI Video Indexer

Azure AI Video Indexer is a media AI service that extracts deep insights from video and audio content using advanced machine learning models. Given the sensitivity of media data—ranging from personal recordings to proprietary business content—Azure AI Video Indexer is built with robust security controls to protect customer data throughout its lifecycle.

This security baseline outlines the key security features, configurations, and best practices to help customers deploy Azure AI Video Indexer securely.

## Data protection

The following sections describe how you can protect your data in Azure AI Video Indexer and how it protects your data both at rest and in transit.

### Data at rest

- **Configure Azure Storage accounts** that you use with Video Indexer with **firewall rules** and **private endpoints** to restrict access. For details, see [Set up Video Indexer with firewall-protected storage](storage-behind-firewall.md).

- **Azure encrypts all customer data stored in Azure** (for example, video files, transcripts, metadata) using **Azure Storage encryption** with **Microsoft-managed keys** by default. See [Azure Storage encryption for data at rest](/azure/storage/common/storage-service-encryption).

### Data in transit

- **Azure encrypts all data transmitted between clients and Azure AI Video Indexer** using **TLS 1.2 or higher**. See [How is network traffic encrypted by Azure AI Video Indexer?](faq.yml#how-is-network-traffic-encrypted-by-azure-ai-video-indexer)

- **Azure enforces secure upload and download mechanisms** in Azure with HTTPS endpoints. See [Require secure transfer to ensure secure connections](/azure/storage/common/storage-require-secure-transfer).

## Identity and access management

- Azure AI Video Indexer integrates with **Microsoft Entra ID** for authentication and authorization. See [Manage access to an Azure AI Video Indexer account](restricted-viewer-role.md).

- **Enforce** **multi-factor authentication (MFA)** and **conditional access policies**. See [Require MFA for Azure management](/entra/identity/conditional-access/policy-old-require-mfa-azure-mgmt).

- **Govern access to resources with Azure Role-Based Access Control (RBAC)**, ensuring least-privilege access. See [Manage access to an Azure AI Video Indexer account](restricted-viewer-role.md).

- **Assign managed identities to secure access to Azure resources without storing credentials**. See [Set up Video Indexer with managed identities](storage-behind-firewall.md#assign-the-managed-identity-and-role).

- You can’t manually delete a trial account. Unused trial accounts get deleted after 12 months of inactivity.

## Network security

- **Configure a private endpoint to securely access data**, allowing traffic to flow through your virtual network. Integration with **Azure Virtual Network (VNet)** ensures isolation and secure communication between services. See [Private endpoints with Azure AI Video Indexer](private-endpoint-overview.md).

- **Restrict access to storage accounts using virtual network rules and IP-based firewall settings**. See [Use network security groups with service tags](network-security.md) and [Set up Video Indexer with firewall-protected storage](storage-behind-firewall.md).

## Threat protection and monitoring

- **Enable** **Azure Monitor**, **Log Analytics**, and **Activity Logs** to track access and operations. **Azure Monitor logs** help track changes and access patterns for compliance and forensic analysis. See [Monitor Azure AI Video Indexer](monitor-video-indexer.md).

- Integrate with **Microsoft Defender for Cloud** to get threat detection and security recommendations. See [Overview - AI threat protection](/azure/defender-for-cloud/ai-threat-protection).

## Backup and recovery

- Azure Video Indexer doesn’t offer its own backup and recovery functionality due to several dependencies.

  - For source media files and encoded (indexed) files linked to your Azure AI Video Indexer account, they’re kept in Azure Storage. Backup and recover the files using Azure Storage backup and recovery guidance. For more information, see [Azure Storage Backup and recovery](/security/benchmark/azure/baselines/storage-security-baseline#backup-and-recovery).

  - For trial account videos and indexed files, store them per your organization’s guidelines.

- We recommend that you download index results including insights and artifacts.

## Security best practices

To enhance the security posture of Azure AI Video Indexer deployments, customers should:

- Use **private endpoints** and restrict public access to storage.

- Enable **diagnostic logging** and monitor with Azure Monitor.

- Apply **RBAC** to limit access to only necessary roles.

- Use **customer-managed keys** for encryption when regulatory compliance requires it.

- Regularly review **Microsoft Entra ID configurations** and enforce MFA.

## Compliance

Azure AI Video Indexer inherits compliance from the Azure platform, which includes:

- ISO/IEC 27001

- SOC 1, SOC 2, SOC 3

- HIPAA (when configured appropriately)

For the latest certifications, refer to the [Microsoft Trust Center](https://www.microsoft.com/trust-center). For compliance information, see [Microsoft Compliance](/compliance/).

## Related content

- [Azure AI Video Indexer documentation](index.yml)
- [Private Endpoint Overview](private-endpoint-overview.md)
- [Storage Behind Firewall Guide](storage-behind-firewall.md)
