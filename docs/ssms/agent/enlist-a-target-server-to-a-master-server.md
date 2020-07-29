---
title: Dar de alta un servidor de destino en un servidor maestro
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- enlisting target servers [SQL Server]
- SQL Server Agent jobs, target servers
- master servers [SQL Server], enlisting target servers
- SQL Server Agent jobs, master servers
- target servers [SQL Server], enlisting
ms.assetid: 7633adb5-d140-4e58-a8f2-5b4b50c2f95b
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 62ff8985b564f30a2ecc64549b9dee22ff6d122a
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85749035"
---
# <a name="enlist-a-target-server-to-a-master-server"></a>Dar de alta un servidor de destino en un servidor maestro
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> En [Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), la mayoría de las características de agente SQL Server son compatibles actualmente, aunque no todas. Vea [Diferencias de T-SQL en Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) para obtener más información.

En este tema se describe el modo de agregar servidores de destino a una configuración de la administración multiservidor. Ejecute este procedimiento en el servidor maestro. en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)]u Objetos de administración de SQL Server (SMO).  
  
Para información sobre cómo la cuenta de Windows usada para el servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] afecta a un entorno multiservidor, consulte [Crear un entorno multiservidor](../../ssms/agent/create-a-multiserver-environment.md).  
  
El cifrado y la validación de certificados completos mediante la Seguridad de la capa de transporte (TLS), anteriormente conocida como Capa de sockets seguros (SSL), se habilitan para las conexiones entre los servidores maestros y los servidores de destino de forma predeterminada. Para más información, [Establecer opciones de cifrado en servidores de destino](../../ssms/agent/set-encryption-options-on-target-servers.md).  
  
## <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a>Usar SQL Server Management Studio  
  
#### <a name="to-enlist-a-target-server"></a>Para dar de alta un servidor de destino  
  
1.  En el **Explorador de objetos**, expanda un servidor que esté configurado como servidor maestro.  
  
2.  Haga clic con el botón derecho en **Agente SQL Server**, seleccione **Administración de multiservidor**y, luego, en **Agregar servidores de destino**.  
  
3.  Complete el Asistente para establecer servidor de destino, que le guía a través del proceso.  
  
## <a name="using-transact-sql"></a><a name="TsqlProcedure"></a>Usar Transact-SQL  
  
#### <a name="to-enlist-a-target-server"></a>Para dar de alta un servidor de destino  
  
1.  Use el procedimiento almacenado **sp_msx_enlist** .  Para más información, consulte [sp_msx_enlist (Transact-SQL)](https://msdn.microsoft.com/ceb3b2bc-0cc4-48d8-9bdc-6a809556e35f).  
  
## <a name="see-also"></a>Consulte también  
[Administración automatizada en una empresa](../../ssms/agent/automated-administration-across-an-enterprise.md)  
  
