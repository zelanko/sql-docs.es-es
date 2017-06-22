---
title: Publicadores que no son de SQL Server | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- heterogeneous database replication, non-SQL Server Publishers
- non-SQL Server Publishers
- heterogeneous data sources, non-SQL Server Publishers
- Publishers [SQL Server replication], Oracle
ms.assetid: 08a160a6-33be-46b5-bc7b-d53180d8bdf1
caps.latest.revision: 31
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 72a1a8c69a7c18f02da6439af94fefffe73a03a3
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="non-sql-server-publishers"></a>publicadores que no son de SQL Server
  Publicar datos de orígenes que no son de[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] permite consolidar datos en [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] pueden suscribirse a datos de instantánea o transaccionales publicados de una base de datos de Oracle. Para obtener más información sobre cómo publicar desde Oracle, vea [Información general de la publicación de Oracle](../../../relational-databases/replication/non-sql/oracle-publishing-overview.md).  
  
 La replicación heterogénea en suscriptores que no son SQL Server está desusada. La publicación de Oracle está desusada. Para mover datos, cree soluciones mediante captura de datos modificados y [!INCLUDE[ssIS](../../../includes/ssis-md.md)].  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
 La publicación desde bases de datos que no son de[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] es idónea en los siguientes escenarios:  
  
|Escenario|Descripción|  
|--------------|-----------------|  
|Implementaciones de aplicaciones de[!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework|Desarrolle con [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Studio y [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cuando trabaje con datos replicados de una base de datos que no es de[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|  
|Servidores provisionales de almacenamiento de datos|Mantenga bases de datos provisionales de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] sincronizadas con una base de datos que no es de[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|  
|Migración a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]|Compruebe la aplicación en tiempo real con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] mientras replica los cambios del sistema de origen. Cambie a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cuando esté satisfecho con la migración.|  
  
## <a name="see-also"></a>Vea también  
 [Heterogeneous Database Replication](../../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)  
  
  
