---
title: Secure Azure AI Video Indexer
description: Learn how to secure Azure AI Video Indexer, with best practices for protecting sensitive media data.
author: cwatson-cat
ms.author: cwatson
ms.service: azure-video-indexer
ms.topic: concept-article
ms.collection: ce-skilling-ai-copilot
ms.custom: horz-security
ms.date: 10/24/2025
appliesto:
  - Cloud-based Azure AI Video Indexer
---

# Secure Azure AI Video Indexer

Azure AI Video Indexer is a media AI service that extracts deep insights from video and audio content by using advanced machine learning models. Given the sensitivity of media data - ranging from personal recordings to proprietary business content - Azure AI Video Indexer is built with robust security controls to protect customer data throughout its lifecycle.

This security baseline outlines the key security features, configurations, and best practices to help customers deploy Azure AI Video Indexer securely.

## Azure AI Video Indexer-specific security

- **Use content filtering and moderation options**. See [Content moderation](faq.yml#i-tried-to-upload-a-video-as-public-and-it-was-flagged-for-inappropriate-or-offensive-content--what-does-that-mean).

- Use responsible AI practices and understand biometric data considerations. See [Limited Access features of Azure AI Video Indexer](limited-access-features.md) and [Transparency note for Azure Video Indexer](/legal/azure-video-indexer/transparency-note).

- Understand API access limitations when using private endpoints. See [Private endpoints with Azure AI Video Indexer](private-endpoint-overview.md).

- You can't convert an Azure AI Video Indexer trial account to an Azure subscription. Instead, you can create a new Azure subscription and then create a new Azure AI Video Indexer resource. See [Create an account](create-account.md).

## Data protection

The following sections describe how you can protect your data in Azure AI Video Indexer and how it protects your data both at rest and in transit.

### Data at rest

- **Configure Azure Storage accounts** that you use with Video Indexer with **firewall rules** and **private endpoints** to restrict access. For details, see [Set up Video Indexer with firewall-protected storage](storage-behind-firewall.md).

- **Azure encrypts all customer data stored in Azure** (for example, video files, transcripts, metadata) by default using **Azure Storage encryption** with **Microsoft-managed keys**. See [Azure Storage encryption for data at rest](/azure/storage/common/storage-service-encryption).

- **Specify your own customer-managed keys** for encrypting and decrypting data in Azure Storage. Data stored by Azure AI Video Indexer isn't encrypted using customer-managed keys. See [Azure Storage encryption for data at rest](/azure/storage/common/storage-service-encryption).

### Data in transit

- **Azure encrypts all data transmitted between clients and Azure AI Video Indexer** by using **TLS 1.2 or higher**. See [How is network traffic encrypted by Azure AI Video Indexer?](faq.yml#how-is-network-traffic-encrypted-by-azure-ai-video-indexer)

- **Azure enforces secure upload and download mechanisms** with HTTPS endpoints. See [Require secure transfer to ensure secure connections](/azure/storage/common/storage-require-secure-transfer).

## Identity and access management

- Azure AI Video Indexer integrates with **Microsoft Entra ID** for authentication and authorization.

  - Owner - This role grants full access to manage all resources, including the ability to assign roles to determine who has access to resources.

  - Contributor - This role has permissions to everything an owner does except it can't control who has access to resources.

  - Video Indexer Restricted Viewer - This role is unique to Azure AI Video Indexer and has permissions to view videos and their insights but can't perform edits or changes or user management operations. This role enables collaboration and user access to insights through the Video Indexer website while limiting their ability to make changes to the environment.

  - See [Manage access to an Azure AI Video Indexer account](restricted-viewer-role.md).

- **Enforce multifactor authentication (MFA)** and **conditional access policies**. See [Require MFA for Azure management](/entra/identity/conditional-access/policy-old-require-mfa-azure-mgmt).

- **Govern access to resources with Azure Role-Based Access Control (RBAC)**, ensuring least-privilege access. See [Manage access to an Azure AI Video Indexer account](restricted-viewer-role.md).

- **Assign managed identities to secure access to Azure resources without storing credentials**. See [Set up Video Indexer with managed identities](storage-behind-firewall.md#assign-the-managed-identity-and-role).

## Network security

- **Configure a private endpoint to securely access data**, allowing traffic to flow through your virtual network. Integration with **Azure Virtual Network (VNet)** ensures isolation and secure communication between services. See [Private endpoints with Azure AI Video Indexer](private-endpoint-overview.md).

- **Restrict access to storage accounts by using virtual network rules and IP-based firewall settings**. See [Use network security groups with service tags](network-security.md) and [Set up Video Indexer with firewall-protected storage](storage-behind-firewall.md).

- **Limit access to resources at the network level** with network security groups and the `VideoIndexer` tag. See [Use network security groups with service tags](network-security.md).

## Threat protection and monitoring

- **Enable** **Azure Monitor**, **Log Analytics**, and **Activity Logs** to track access and operations. **Azure Monitor logs** help track changes and access patterns for compliance and forensic analysis. See [Monitor Azure AI Video Indexer](monitor-video-indexer.md).

- Integrate with **Microsoft Defender for Cloud** to get threat detection and security recommendations. See [Overview - AI threat protection](/azure/defender-for-cloud/ai-threat-protection).

## Backup and recovery

- Azure Video Indexer doesn't offer its own backup and recovery functionality due to several dependencies.

  - **Plan for business continuity and disaster recovery**. See [Configure failover for disaster recovery](video-indexer-disaster-recovery.md).

  - Source media files and encoded (indexed) files linked to your Azure AI Video Indexer account are kept in Azure Storage.

  - **Backup and recover the files by using Azure Storage backup and recovery guidance**. For more information, see [Azure Storage Backup and recovery](/security/benchmark/azure/baselines/storage-security-baseline#backup-and-recovery).

  - For trial account videos and indexed files, store them per your organization’s guidelines.

- Regularly [download index results](transcription-translation-lid-insight.md) including insights and artifacts.

## Security best practices

To enhance the security of Azure AI Video Indexer deployments, use the following best practices:

- Use **private endpoints** and restrict public access to storage.

- Enable **diagnostic logging** and monitor with Azure Monitor.

- Apply **RBAC** to limit access to only necessary roles.

- Use **customer-managed keys** for encryption when regulatory compliance requires it.

- Regularly review **Microsoft Entra ID configurations** and enforce MFA.

## Compliance and governance

- **Use Azure Policy to enforce a consistent configuration**. See [Azure Policy overview](/azure/governance/policy/overview) and [Azure Policy built-in policy definitions – Monitoring](/azure/governance/policy/samples/built-in-policies#monitoring).

- **Review data residency and regulatory compliance**. See [Compliance, privacy, and security](video-indexer-overview.md#compliance-privacy-and-security).

- Azure AI Video Indexer inherits compliance from the Azure platform, which includes:

  - ISO/IEC 27001

  - SOC 1, SOC 2, SOC 3

  - HIPAA (when configured appropriately)

For the latest certifications, refer to the [Microsoft Trust Center](https://www.microsoft.com/trust-center). For compliance information, see [Microsoft Compliance](/compliance/).

## Related content

- [Azure AI Video Indexer documentation](index.yml)
- [Private Endpoint Overview](private-endpoint-overview.md)
- [Storage Behind Firewall Guide](storage-behind-firewall.md)
