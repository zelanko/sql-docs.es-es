---
title: Tablas del sistema (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- status information [SQL Server]
- tables [SQL Server], system tables
- information retrieval [SQL Server]
- status information [SQL Server], system tables
- system information [SQL Server]
- system tables [SQL Server]
- system tables [SQL Server], about system tables
- system tables [SQL Server], retrieving information from
- retrieving system table information
ms.assetid: 56b8ad51-930c-4e5c-8d99-8c939d5b70ac
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 7d2fe1cedb18dd3b2cfd5b6375a61a328178d6f7
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="system-tables-transact-sql"></a>Tablas del sistema (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  En los temas de esta sección se describen las tablas del sistema de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Ningún usuario debe modificar directamente las tablas del sistema. Por ejemplo, no intente modificar tablas del sistema con las instrucciones DELETE, UPDATE o INSERT, ni con desencadenadores definidos por el usuario.  
  
 Se permite hacer referencia a columnas documentadas en las tablas del sistema. Sin embargo, muchas de las columnas de las tablas del sistema no están documentadas. No deben escribirse aplicaciones que consulten directamente columnas no documentadas. En su lugar, las aplicaciones deben usar cualquiera de los componentes siguientes para recuperar la información almacenada en las tablas del sistema:  
  
-   Procedimientos almacenados del sistema  
  
-   Instrucciones y funciones [!INCLUDE[tsql](../../includes/tsql-md.md)]  
  
-   Objetos de administración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SMO)  
  
-   Replication Management Objects (RMO)  
  
-   Funciones de catálogo de API de base de datos  
  
 Estos componentes conforman una API publicado para obtener información del sistema de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. [!INCLUDE[msCoName](../../includes/msconame-md.md)] mantiene la compatibilidad de estos componentes entre versiones. El formato de las tablas del sistema depende de la arquitectura interna de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y puede cambiar de una versión a otra. Por tanto, puede ser necesario modificar las aplicaciones que tienen acceso directo a columnas no documentadas de las tablas del sistema para que puedan tener acceso a una versión posterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="in-this-section"></a>En esta sección  
 Los temas relacionados con las tablas del sistema se organizan según las siguientes áreas de características:  
  
|||  
|-|-|  
|[Copia de seguridad y restauración tablas &#40; Transact-SQL &#41;](../../relational-databases/system-tables/backup-and-restore-tables-transact-sql.md)|[Tablas de trasvase de registros &#40;Transact-SQL&#41;](../../relational-databases/system-tables/log-shipping-tables-transact-sql.md)|  
|[Captura de datos modificados tablas &#40; Transact-SQL &#41;](../../relational-databases/system-tables/change-data-capture-tables-transact-sql.md)|[Tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)|  
|[Tablas de planes de mantenimiento de base de datos &#40; Transact-SQL &#41;](../../relational-databases/system-tables/database-maintenance-plan-tables-transact-sql.md)|[Tablas del Agente SQL Server &#40; Transact-SQL &#41;](../../relational-databases/system-tables/sql-server-agent-tables-transact-sql.md)|  
|[Tablas de eventos &#40; extendidos de SQL Server Transact-SQL &#41;](http://msdn.microsoft.com/library/6d52ff03-f5aa-4f0f-8c98-9b49dc76f94e)|[Sys.sysoledbusers &#40; Transact-SQL &#41;](../../relational-databases/system-compatibility-views/sys-sysoledbusers-transact-sql.md)|  
|[Tablas &#40; de Integration Services Transact-SQL &#41;](../../relational-databases/system-tables/integration-services-tables-transact-sql.md)|[systranschemas &#40; Transact-SQL &#41;](../../relational-databases/system-views/systranschemas-transact-sql.md)|  
  
## <a name="see-also"></a>Vea también  
 [Vistas de compatibilidad &#40; Transact-SQL &#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)   
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
