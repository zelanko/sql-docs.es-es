---
title: Remote Blob Store (RBS) y grupos de disponibilidad AlwaysOn (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: 01a70258-d4fd-40bc-bc44-c490b5d6c420
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 16480ffcaf73a88f5983bef41b90f2276709d947
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48212065"
---
# <a name="remote-blob-store-rbs-and-alwayson-availability-groups-sql-server"></a>Almacén remoto de blobs (RBS) y grupos de disponibilidad AlwaysOn (SQL Server)
  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] puede proporcionar una solución de alta disponibilidad y recuperación ante desastres para los objetos BLOB (blobs) del [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)][Almacén remoto de blobs (RBS)](../../../relational-databases/blob/remote-blob-store-rbs-sql-server.md). [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] protege los metadatos y esquema de RBS almacenados en una base de datos de disponibilidad replicándolos en las réplicas secundarias. Se trata de la base de datos de contenido de SharePoint. En general, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] almacena estos metadatos de RBS independientemente del blob.  
  
 La protección de los datos BLOB de RBS depende de la ubicación del almacén de BLOB, de la manera siguiente:  
  
|Ubicación del almacén de BLOB|¿Pueden los grupos de disponibilidad proteger estos datos BLOB?|  
|-------------------------|-----------------------------------------------------|  
|La misma base de datos que contiene los metadatos de RBS (almacenada mediante un proveedor remoto FILESTREAM de RBS)|Sí|  
|Otra base de datos de la misma instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (almacenada mediante un proveedor remoto FILESTREAM de RBS)|Sí<br /><br /> Se recomienda que esta base de datos esté en el mismo grupo de disponibilidad que la base de datos que contiene los metadatos de RBS.|  
|Otra base de datos de otra instancia diferente de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (almacenada mediante un proveedor remoto FILESTREAM de RBS)|Sí<br /><br /> Esta base de datos debe estar en un grupo de disponibilidad diferente.|  
|Un almacén de blobs de terceros|no<br /><br /> Para proteger estos datos BLOB, use los mecanismos de alta disponibilidad del proveedor de almacenes de blobs.|  
  
##  <a name="Limitations"></a> Limitaciones  
  
-   Los mantenedores de RBS deben tener como destino la réplica principal.  
  
##  <a name="Recommendations"></a> Recomendaciones  
  
-   Use un agente de escucha del grupo de disponibilidad. Para obtener más información, vea [Agentes de escucha de grupo de disponibilidad, conectividad de cliente y conmutación por error de una aplicación &#40;SQL Server&#41;](../../listeners-client-connectivity-application-failover.md).  
  
##  <a name="RelatedContent"></a> Contenido relacionado  
  
-   [Mantener un almacén remoto de blobs](http://msdn.microsoft.com/library/gg316773\(SQL.105\).aspx) (en los Libros en pantalla de [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] )  
  
-   [Ejecutar el Mantenedor de RBS](http://blogs.msdn.com/b/sqlrbs/archive/2010/03/19/running-rbs-maintainer.aspx) (blog)  
  
-   [Configurar el almacenamiento remoto de blobs (RBS) con el proveedor FILESTREAM (SharePoint 2010)](http://blogs.msdn.com/b/mvpawardprogram/archive/2012/04/02/configure-remote-blob-storage-rbs-with-the-filestream-provider-sharepoint-2010.aspx) (blog)  
  
## <a name="see-also"></a>Vea también  
 [Conectividad de cliente de AlwaysOn &#40;SQL Server&#41;](always-on-client-connectivity-sql-server.md)   
 [Almacén remoto de blobs &#40;RBS&#41; &#40;SQL Server&#41;](../../../relational-databases/blob/remote-blob-store-rbs-sql-server.md)  
  
  
