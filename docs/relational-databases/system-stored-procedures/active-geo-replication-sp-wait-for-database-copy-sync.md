---
title: sp_wait_for_database_copy_sync (base de datos de SQL Azure) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/03/2017
ms.prod: ''
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.service: sql-database
ms.component: system-stored-procedures
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_wait_for_database_copy_sync_TSQL
- sp_wait_for_database_copy_sync
dev_langs:
- TSQL
helpviewer_keywords:
- sp_wait_for_database_copy_sync
ms.assetid: 7068da7f-cb74-47f2-b064-eb076a0d3885
caps.latest.revision: 13
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 6658ab7b1b68637978ca76ea709c4c0a23414d07
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
---
# <a name="active-geo-replication---spwaitfordatabasecopysync"></a>Replicación geográfica activa - sp_wait_for_database_copy_sync
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Este procedimiento tiene como ámbito una relación de [!INCLUDE[ssGeoDR](../../includes/ssgeodr-md.md)] entre una base de datos principal y una base de datos secundaria. Llamar a la **sp_wait_for_database_copy_sync** hace que la aplicación espera hasta que todas las transacciones confirmadas se replica y confirma la base de datos secundaria activa. Ejecutar **sp_wait_for_database_copy_sync** sólo la base de datos principal.  
  
||  
|-|  
|**Se aplica a**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].|  
  
## <a name="syntax"></a>Sintaxis  
  
```  
sp_wait_for_database_copy_sync [ @target_server = ] 'server_name'   
     , [ @target_database = ] 'database_name'  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @target_server =] 'nombreDeServidor'  
 Nombre del servidor de SQL Database que hospeda la base de datos secundaria activa. server_name es sysname, sin valor predeterminado.  
  
 [ @target_database =] 'NombreBaseDatos'  
 Nombre de la base de datos secundaria activa. database_name es sysname y no tiene ningún valor predeterminado.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 Devuelve 0 para indicar que es correcto o un número de error si hay un error.  
  
 Las condiciones de error más probables son las siguientes:  
  
-   El nombre de servidor o el nombre de la base de datos falta.  
  
-   El vínculo no se puede encontrar en la base de datos o el nombre de servidor especificados.  
  
-   La conectividad interlink se pierde. **sp_wait_for_database_copy_sync** volverá transcurrido el tiempo de espera de conexión.  
  
## <a name="permissions"></a>Permissions  
 Cualquier usuario de la base de datos principal puede llamar a este procedimiento almacenado del sistema. El inicio de sesión debe ser un usuario tanto en la base de datos principal como en la secundaria activa.  
  
## <a name="remarks"></a>Comentarios  
 Todas las transacciones confirmadas antes un **sp_wait_for_database_copy_sync** llamada se envían a la base de datos secundaria activa.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se invoca **sp_wait_for_database_copy_sync** para asegurarse de que todas las transacciones se confirman en la base de datos principal, db0, se envía a su base de datos secundaria activa en el ubfyu5ssyt del servidor de destino.  
  
```  
USE db0;  
GO  
EXEC sys.sp_wait_for_database_copy_sync @target_server = N'ubfyu5ssyt1', @target_database = N'db0';  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Sys.dm_continuous_copy_status &#40;base de datos de SQL Azure&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-continuous-copy-status-azure-sql-database.md)   
 [Funciones y vistas de administración dinámica de replicación geográfica &#40;base de datos SQL Azure&#41;](../../relational-databases/system-dynamic-management-views/geo-replication-dynamic-management-views-and-functions-azure-sql-database.md)  
  
  
