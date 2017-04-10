---
title: "MSSQL_ENG020596 | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "error MSSQL_ENG020596"
ms.assetid: fa33627c-2e99-4be3-9424-52ab83446e07
caps.latest.revision: 14
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 14
---
# MSSQL_ENG020596
    
## Detalles del mensaje  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|20596|  
|Origen del evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nombre simbólico||  
|Texto del mensaje|Solo '%1!' o los miembros de db_owner pueden quitar el agente anónimo.|  
  
## Explicación  
 No tiene suficientes permisos para quitar el agente de la suscripción anónima. El inicio de sesión utilizado al llamar a [sp_dropanonymousagent & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-dropanonymousagent-transact-sql.md) debe ser miembro de la **sysadmin** rol fijo de servidor en el distribuidor o **db_owner** rol fijo de base de datos en la base de datos de distribución o el usuario debe ser el único que haya iniciado la primera ejecución del agente.  
  
## Acción del usuario  
 Inicie sesión con las credenciales adecuadas y ejecutar **sp_dropanonymousagent**.  
  
## Vea también  
 [Errores y eventos referencia & #40; Replicación y nº 41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  