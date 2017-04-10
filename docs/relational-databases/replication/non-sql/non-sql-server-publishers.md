---
title: "Publicadores que no son de SQL Server | Microsoft Docs"
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
  - "replicación de bases de datos heterogéneas, Publicadores que no son de SQL Server"
  - "publicadores que no son de SQL Server"
  - "orígenes de datos heterogéneos, Publicadores que no son de SQL Server"
  - "Publicadores [replicación de SQL Server], Oracle"
ms.assetid: 08a160a6-33be-46b5-bc7b-d53180d8bdf1
caps.latest.revision: 31
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 31
---
# Publicadores que no son de SQL Server
  Publicar datos de no son[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] orígenes permite consolidar datos en [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] pueden suscribirse a datos de instantánea o transaccionales publicados de una base de datos de Oracle. Para obtener más información acerca de la publicación de Oracle, vea [Introducción a la publicación Oracle](../../../relational-databases/replication/non-sql/oracle-publishing-overview.md).  
  
 La replicación heterogénea en suscriptores que no son SQL Server está desusada. La publicación de Oracle está desusada. Para mover datos, cree soluciones mediante captura de datos modificados y [!INCLUDE[ssIS](../../../includes/ssis-md.md)].  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
 La publicación desde bases de datos que no son de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] es idónea en los siguientes escenarios:  
  
|Escenario|Descripción|  
|--------------|-----------------|  
|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework|Desarrolle con [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Studio y [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cuando trabaje con datos replicados de una base de datos que no es de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|Servidores provisionales de almacenamiento de datos|Mantener [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] bases de datos provisionales sincronizan con un no[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] base de datos.|  
|Migración a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]|Compruebe la aplicación en tiempo real con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] mientras replica los cambios del sistema de origen. Cambie a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cuando esté satisfecho con la migración.|  
  
## Vea también  
 [Replicación de bases de datos heterogéneas](../../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)  
  
  