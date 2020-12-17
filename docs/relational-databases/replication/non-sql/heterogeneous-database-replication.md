---
description: replicación de bases de datos heterogéneas
title: Replicación de bases de datos heterogéneas | Microsoft Docs
ms.custom: ''
ms.date: 08/28/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- heterogeneous database replication, about heterogeneous database replication
- replication [SQL Server], heterogeneous database replication
- heterogeneous database replication
ms.assetid: 3fd983ad-e206-45db-9054-417c9b5bb815
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: d5ea494a48932fac171eb4d9e8bc3e032001e55b
ms.sourcegitcommit: 821e7039a342bf76306d66c61db247dc2caabc46
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/10/2020
ms.locfileid: "96999245"
---
# <a name="heterogeneous-database-replication"></a>replicación de bases de datos heterogéneas  
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] admite los siguientes escenarios heterogéneos para la replicación de instantáneas y transaccional:  
  
-   Publicar datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en suscriptores que no son de[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  

-   La publicación de datos en y desde Oracle tiene las siguientes restricciones:  

  |Escenario|2016 o anterior |2017 o posterior |
  |-------|-------|--------|
  |Replicación de Oracle |Compatibilidad solo con Oracle 10g o versiones anteriores |Compatibilidad solo con Oracle 10g o versiones anteriores |
  |Replicación en Oracle |Todas las versiones anteriores a Oracle 12c |No compatible |


 La replicación heterogénea en suscriptores que no son SQL Server está desusada. La publicación de Oracle está desusada. Para mover datos, cree soluciones mediante captura de datos modificados y [!INCLUDE[ssIS](../../../includes/ssis-md.md)].  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
## <a name="publishing-data-from-oracle"></a>Publicar datos de Oracle  
 Puede usar [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para publicar datos de Oracle con la mayoría de características y la misma facilidad de uso que la replicación de instantáneas y transaccional de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Esta característica requiere la versión 10G o una versión anterior de Oracle. La publicación de datos de Oracle es ideal en los siguientes escenarios:  
  
|Escenario|Descripción|  
|--------------|-----------------|  
|Implementaciones de aplicaciones de[!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework|Desarrolle con [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Studio y [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cuando trabaje con datos replicados de una base de datos que no es de[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|  
|Servidores provisionales de almacenamiento de datos|Mantenga las bases de datos provisionales de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] sincronizadas con una base de datos que no es de[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|  
|Migración a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]|Compruebe la aplicación en tiempo real con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] mientras replica los cambios del sistema de origen. Cambie a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cuando esté satisfecho con la migración.|  
  
 Para obtener más información, vea [Oracle Publishing Overview](../../../relational-databases/replication/non-sql/oracle-publishing-overview.md) (Información general de la publicación de Oracle).  
  
## <a name="publishing-data-to-non-sql-server-subscribers"></a>Publicar datos en suscriptores que no son de SQL Server  
 Las siguientes bases de datos que no son de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] son compatibles como suscriptores de publicaciones de instantáneas y transaccionales:  
  
-   Oracle para todas las plataformas que admite Oracle.  
  
-   IBM DB2 para AS400, MVS, Unix, Linux y Windows  
  
 Para más información, consulte [Non-SQL Server Subscribers](../../../relational-databases/replication/non-sql/non-sql-server-subscribers.md).  
  
  
