---
title: Publicadores que no son de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 08/29/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- heterogeneous database replication, non-SQL Server Publishers
- non-SQL Server Publishers
- heterogeneous data sources, non-SQL Server Publishers
- Publishers [SQL Server replication], Oracle
ms.assetid: 08a160a6-33be-46b5-bc7b-d53180d8bdf1
caps.latest.revision: 31
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 37a9b2c8760bc1c259d0d85b99ab28dc9128ccfa
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="non-sql-server-publishers"></a>publicadores que no son de SQL Server  
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Publicar datos de orígenes que no son de[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] permite consolidar datos en [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] pueden suscribirse a datos de instantánea o transaccionales publicados de una base de datos de Oracle. Para obtener más información sobre cómo publicar desde Oracle, vea [Información general de la publicación de Oracle](../../../relational-databases/replication/non-sql/oracle-publishing-overview.md).  
  
[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] admite los siguientes escenarios heterogéneos para la replicación de instantáneas y transaccional:  
  
-   Publicar datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en suscriptores que no son de[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  

-   La publicación de datos en y desde Oracle tiene las siguientes restricciones:  
  | |2016 o anterior |2017 o posterior |
  |-------|-------|--------|
  |Replicación de Oracle |Compatibilidad solo con Oracle 10g o versiones anteriores |Compatibilidad solo con Oracle 10g o versiones anteriores |
  |Replicación en Oracle |Hasta Oracle 12c |No compatible |


 La replicación heterogénea en suscriptores que no son SQL Server está desusada. La publicación de Oracle está desusada. Para mover datos, cree soluciones mediante captura de datos modificados y [!INCLUDE[ssIS](../../../includes/ssis-md.md)].  
  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
 La publicación desde bases de datos que no son de[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] es idónea en los siguientes escenarios:  
  
|Escenario|Description|  
|--------------|-----------------|  
|Implementaciones de aplicaciones de[!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework|Desarrolle con [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Studio y [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cuando trabaje con datos replicados de una base de datos que no es de[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|  
|Servidores provisionales de almacenamiento de datos|Mantenga las bases de datos provisionales de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] sincronizadas con una base de datos que no es de[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|  
|Migración a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]|Compruebe la aplicación en tiempo real con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] mientras replica los cambios del sistema de origen. Cambie a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cuando esté satisfecho con la migración.|  
  
## <a name="see-also"></a>Ver también  
 [Heterogeneous Database Replication](../../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)  
  
  
