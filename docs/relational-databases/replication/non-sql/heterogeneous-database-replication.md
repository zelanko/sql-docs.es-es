---
title: "Replicaci&#243;n de bases de datos heterog&#233;neas | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "replicación de bases de datos heterogéneas, acerca de la replicación de bases de datos heterogéneas"
  - "replicación [SQL Server], replicación de bases de datos heterogéneas"
  - "replicación de bases de datos heterogéneas"
ms.assetid: 3fd983ad-e206-45db-9054-417c9b5bb815
caps.latest.revision: 41
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 41
---
# Replicaci&#243;n de bases de datos heterog&#233;neas
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] admite los siguientes escenarios heterogéneos para la replicación de instantáneas y transaccional:  
  
-   Publicar datos de Oracle en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Publicar datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en suscriptores que no son de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 La replicación heterogénea en suscriptores que no son SQL Server está desusada. La publicación de Oracle está desusada. Para mover datos, cree soluciones mediante captura de datos modificados y [!INCLUDE[ssIS](../../../includes/ssis-md.md)].  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
## Publicar datos de Oracle  
 Puede usar [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para publicar datos de Oracle con la mayoría de características y la misma facilidad de uso que la replicación de instantáneas y transaccional de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. La publicación de datos de Oracle es ideal en los siguientes escenarios:  
  
|Escenario|Descripción|  
|--------------|-----------------|  
|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework|Desarrolle con [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Studio y [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cuando trabaje con datos replicados de una base de datos que no es de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|Servidores provisionales de almacenamiento de datos|Mantener [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] bases de datos provisionales sincronizan con un no[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] base de datos.|  
|Migración a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]|Compruebe la aplicación en tiempo real con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] mientras replica los cambios del sistema de origen. Cambie a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cuando esté satisfecho con la migración.|  
  
 Para obtener más información, consulte [Introducción a la publicación Oracle](../../../relational-databases/replication/non-sql/oracle-publishing-overview.md).  
  
## Publicar datos en suscriptores que no son de SQL Server  
 Las siguientes bases de datos que no son de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] son compatibles como suscriptores de publicaciones de instantáneas y transaccionales:  
  
-   Oracle para todas las plataformas que admite Oracle.  
  
-   IBM DB2 para AS400, MVS, Unix, Linux y Windows  
  
 Para obtener más información, consulte [suscriptores no SQL Server](../../../relational-databases/replication/non-sql/non-sql-server-subscribers.md).  
  
  