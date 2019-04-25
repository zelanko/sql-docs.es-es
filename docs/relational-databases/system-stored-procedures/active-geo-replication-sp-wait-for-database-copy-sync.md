---
title: sp_wait_for_database_copy_sync (Azure SQL Database) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- sp_wait_for_database_copy_sync_TSQL
- sp_wait_for_database_copy_sync
dev_langs:
- TSQL
helpviewer_keywords:
- sp_wait_for_database_copy_sync
ms.assetid: 7068da7f-cb74-47f2-b064-eb076a0d3885
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: dd0d134e723a8ca45729933cbbf5b0d75bbde7e6
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62446411"
---
# <a name="active-geo-replication---spwaitfordatabasecopysync"></a>Replicación geográfica activa - sp_wait_for_database_copy_sync
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Este procedimiento tiene como ámbito una relación de [!INCLUDE[ssGeoDR](../../includes/ssgeodr-md.md)] entre una base de datos principal y una base de datos secundaria. Una llamada a la **sp_wait_for_database_copy_sync** hace que la aplicación espera hasta que todas las transacciones confirmadas se replica y confirma la base de datos secundaria activa. Ejecute **sp_wait_for_database_copy_sync** solo la base de datos principal.  
  
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
  
-   La conectividad interlink se pierde. **sp_wait_for_database_copy_sync** devolverá tras el tiempo de espera de conexión.  
  
## <a name="permissions"></a>Permisos  
 Cualquier usuario de la base de datos principal puede llamar a este procedimiento almacenado del sistema. El inicio de sesión debe ser un usuario tanto en la base de datos principal como en la secundaria activa.  
  
## <a name="remarks"></a>Comentarios  
 Todas las transacciones confirmadas antes un **sp_wait_for_database_copy_sync** llamada se envían a la base de datos secundaria activa.  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente se invoca **sp_wait_for_database_copy_sync** para asegurarse de que todas las transacciones se confirman en la base de datos principal, db0, se envía a su base de datos secundaria activa en el ubfyu5ssyt del servidor de destino.  
  
```  
USE db0;  
GO  
EXEC sys.sp_wait_for_database_copy_sync @target_server = N'ubfyu5ssyt1', @target_database = N'db0';  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Sys.dm_continuous_copy_status &#40;Azure SQL Database&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-continuous-copy-status-azure-sql-database.md)   
 [Funciones y vistas de administración dinámica de replicación geográfica &#40;base de datos SQL Azure&#41;](../../relational-databases/system-dynamic-management-views/geo-replication-dynamic-management-views-and-functions-azure-sql-database.md)  
  
  
