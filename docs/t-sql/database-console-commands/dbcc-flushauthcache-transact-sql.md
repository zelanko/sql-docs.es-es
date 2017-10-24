---
title: DBCC FLUSHAUTHCACHE (Transact-SQL) | Documentos de Microsoft
ms.custom:
- MSDN content
- MSDN - SQL DB
ms.date: 07/16/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DBCC FLUSHAUTHCACHE
- FLUSHAUTHCACHE
- DBCC_FLUSHAUTHCACHE_TSQL
- FLUSHAUTHCACHE_TSQL
helpviewer_keywords:
- DBCC FLUSHAUTHCACHE
ms.assetid: 681ef31d-ceb9-4da5-86bf-bf1240df950f
caps.latest.revision: 11
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3ba6a519ebcdbbc70bf19ec491539a3b07fb6c85
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="dbcc-flushauthcache-transact-sql"></a>DBCC FLUSHAUTHCACHE (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

Vacía la caché de autenticación de base de datos que contiene información sobre los inicios de sesión y las reglas de firewall para la base de datos de usuario actual en [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. Esta instrucción no se aplica a la base de datos maestra lógica, dado que la base de datos maestra contiene el almacenamiento físico de la información sobre los inicios de sesión y las reglas de firewall. El usuario que ejecuta la instrucción y otros usuarios que están conectados permanecen conectados. (DBCC FLUSHAUTHCACHE no se admite actualmente para [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)].)
 
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
DBCC FLUSHAUTHCACHE [ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
Ninguno.
  
## <a name="remarks"></a>Comentarios  
La caché de autenticación realiza una copia de los inicios de sesión y las reglas de firewall del servidor que se almacenan en master y las coloca en la memoria en la base de datos de usuario.  Puesto que la información acerca de los usuarios de base de datos independiente ya están almacenados en la base de datos de usuario, los usuarios de base de datos independiente no forman parte de la caché de autenticación.
Conexiones activas continuamente a [!INCLUDE[ssSDS](../../includes/sssds-md.md)] requieren vuelva a autorizarla (realizadas por el [!INCLUDE[ssDE](../../includes/ssde-md.md)]) al menos cada 10 horas. El [!INCLUDE[ssDE](../../includes/ssde-md.md)] vuelva a autorizarla intentos con la contraseña enviada originalmente y ningún usuario de entrada es necesaria. Por motivos de rendimiento, cuando se restablece una contraseña de [!INCLUDE[ssSDS](../../includes/sssds-md.md)], la conexión no se volverá a autenticar, incluso si la conexión se restablezca debido a la agrupación de conexiones. Esto es diferente del comportamiento de local [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Si la contraseña se cambió desde que inicialmente se autorizó la conexión, debe terminar la conexión y establece una nueva conexión con la nueva contraseña. Un usuario con el permiso KILL DATABASE CONNECTION puede terminar explícitamente una conexión a [!INCLUDE[ssSDS](../../includes/sssds-md.md)] utilizando el [KILL &#40; Transact-SQL &#41; ](../../t-sql/language-elements/kill-transact-sql.md) comando.
  
## <a name="permissions"></a>Permissions  
Requiere la [!INCLUDE[ssSDS](../../includes/sssds-md.md)] cuenta de administrador.
  
## <a name="example"></a>Ejemplo  
La siguiente instrucción borra la caché de autenticación para la base de datos actual.
  
```sql
DBCC FLUSHAUTHCACHE;  
```  
  
## <a name="see-also"></a>Vea también  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)
  
  

