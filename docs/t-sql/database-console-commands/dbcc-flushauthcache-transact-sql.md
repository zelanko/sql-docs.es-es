---
title: DBCC FLUSHAUTHCACHE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DBCC FLUSHAUTHCACHE
- FLUSHAUTHCACHE
- DBCC_FLUSHAUTHCACHE_TSQL
- FLUSHAUTHCACHE_TSQL
helpviewer_keywords:
- DBCC FLUSHAUTHCACHE
ms.assetid: 681ef31d-ceb9-4da5-86bf-bf1240df950f
author: VanMSFT
ms.author: vanto
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 00497dfe67c03eab4d9d0bc1798f6d5537628ed7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68101940"
---
# <a name="dbcc-flushauthcache-transact-sql"></a>DBCC FLUSHAUTHCACHE (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

Vacía la caché de autenticación de base de datos que contiene información sobre los inicios de sesión y las reglas de firewall para la base de datos de usuario actual en [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. Esta instrucción no se aplica a la base de datos maestra lógica, dado que la base de datos maestra contiene el almacenamiento físico de la información sobre los inicios de sesión y las reglas de firewall. El usuario que ejecuta la instrucción y otros usuarios conectados permanecen conectados. (DBCC FLUSHAUTHCACHE no se admite actualmente para [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)]).
 
![Icono de vínculo a artículo](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo a artículo") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
DBCC FLUSHAUTHCACHE [ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
Ninguno.
  
## <a name="remarks"></a>Notas  
La caché de autenticación realiza una copia de los inicios de sesión y las reglas de firewall del servidor que se almacenan en la base de datos maestra y las coloca en la memoria en la base de datos de usuario.  Puesto que la información sobre los usuarios de bases de datos independientes ya está almacenada en la base de datos de usuario, los usuarios de bases de datos independientes no forman parte de la caché de autenticación.
Las conexiones activas continuamente a [!INCLUDE[ssSDS](../../includes/sssds-md.md)] requieren una reautorización (realizada por el [!INCLUDE[ssDE](../../includes/ssde-md.md)]) como mínimo cada 10 horas. El [!INCLUDE[ssDE](../../includes/ssde-md.md)] intenta la reautorización con la contraseña enviada originalmente y no se requiere la intervención del usuario. Por motivos de rendimiento, cuando una contraseña se restablece en [!INCLUDE[ssSDS](../../includes/sssds-md.md)], la conexión no se volverá a autenticar, incluso si se restablece la conexión debido a la agrupación de conexiones. Este comportamiento es diferente del comportamiento de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] local. Si la contraseña se ha cambiado desde que se autorizó inicialmente la conexión, es necesario terminar la conexión y establecer una nueva con la nueva contraseña. Un usuario con el permiso KILL DATABASE CONNECTION puede terminar explícitamente una conexión con [!INCLUDE[ssSDS](../../includes/sssds-md.md)] mediante el comando [KILL &#40;Transact-SQL&#41;](../../t-sql/language-elements/kill-transact-sql.md).
  
## <a name="permissions"></a>Permisos  
Requiere la cuenta de administrador [!INCLUDE[ssSDS](../../includes/sssds-md.md)].
  
## <a name="example"></a>Ejemplo  
La instrucción siguiente borra la caché de autenticación de la base de datos actual.
  
```sql
DBCC FLUSHAUTHCACHE;  
```  
  
## <a name="see-also"></a>Consulte también  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)
  
