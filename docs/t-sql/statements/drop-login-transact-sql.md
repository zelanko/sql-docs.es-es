---
title: DROP LOGIN (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/11/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DROP LOGIN
- DROP_LOGIN_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- deleting login accounts
- logins [SQL Server], removing
- DROP LOGIN statement
- removing login accounts
- dropping login accounts
ms.assetid: acb5c3dc-7aa2-49f6-9330-573227ba9b1a
caps.latest.revision: 36
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9c4f9ddc6ae518d41cfce660dc02a895ec38ea87
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2018
ms.locfileid: "43103189"
---
# <a name="drop-login-transact-sql"></a>DROP LOGIN (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Quita una cuenta de inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
DROP LOGIN login_name  
```  
  
## <a name="arguments"></a>Argumentos  
 *login_name*  
 Especifica el nombre del inicio de sesión que se va a quitar.  
  
## <a name="remarks"></a>Notas  
 Un inicio de sesión no puede quitarse mientras esté activo. No se puede quitar un inicio de sesión que sea propietario de un elemento protegible, un objeto de servidor o un trabajo del Agente SQL Server.  
  
 Puede quitar un inicio de sesión al que están asignados usuarios de la base de datos; no obstante, esto creará usuarios huérfanos. Para obtener más información, vea [Solucionar problemas de usuarios huérfanos &#40;SQL Server&#41;](../../sql-server/failover-clusters/troubleshoot-orphaned-users-sql-server.md).  
  
 En [!INCLUDE[ssSDS](../../includes/sssds-md.md)], los datos de inicio de sesión necesarios para autenticar una conexión y reglas de firewall de nivel de servidor se almacenan temporalmente en caché en cada base de datos. Esta caché se actualiza regularmente. Para forzar una actualización de la caché de autenticación y garantizar que una base de datos tenga la versión más reciente de la tabla de inicios de sesión, ejecute [DBCC FLUSHAUTHCACHE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-flushauthcache-transact-sql.md).  
  
## <a name="permissions"></a>Permisos  
 Requiere el permiso ALTER ANY LOGIN en el servidor.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-dropping-a-login"></a>A. Quitar un inicio de sesión  
 En el ejemplo siguiente se quita el inicio de sesión `WilliJo`.  
  
```  
DROP LOGIN WilliJo;  
GO 
```  
 
  
## <a name="see-also"></a>Ver también  
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [ALTER LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/alter-login-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  

