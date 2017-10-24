---
title: DBCC FREESYSTEMCACHE (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 07/16/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- FREESYSTEMCACHE_TSQL
- DBCC_FREESYSTEMCACHE_TSQL
- DBCC FREESYSTEMCACHE
- FREESYSTEMCACHE
dev_langs:
- TSQL
helpviewer_keywords:
- clearing unused cache entries
- DBCC FREESYSTEMCACHE statement
- unused cache entries
- releasing unused cache entries
- freeing unused cache entries
- cleaning unused cache entries
ms.assetid: 4b5c460b-e4ad-404a-b4ca-d65aba38ebbb
caps.latest.revision: 35
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 70de1caf9d8bceab6b596952044bb7b3961f60f2
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="dbcc-freesystemcache-transact-sql"></a>DBCC FREESYSTEMCACHE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Libera todas las entradas de caché no utilizadas de todas las memorias caché. El [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] limpia automáticamente y en segundo plano todas las entradas de caché no utilizadas para permitir que haya memoria disponible para las entradas actuales. Sin embargo, puede utilizar este comando para quitar de forma manual las entradas no usadas de todas las memorias caché o de la memoria caché especificada de un grupo del regulador de recursos.
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
```sql
DBCC FREESYSTEMCACHE   
    ( 'ALL' [, pool_name ] )   
    [WITH   
    { [ MARK_IN_USE_FOR_REMOVAL ] , [ NO_INFOMSGS ]  }  
    ]  
```  
  
## <a name="arguments"></a>Argumentos  
 ('ALL' [,*pool_name* ])  
 ALL especifica todas las memorias caché compatibles.  
 *pool_name* especifica una caché de grupo del regulador de recursos. Solo se liberarán las entradas asociadas a este grupo.  
  
 MARK_IN_USE_FOR_REMOVAL  
 Libera asincrónicamente las entradas utilizadas actualmente de sus respectivas cachés después de que dejan de utilizarse. No se verán afectadas las nuevas entradas creadas en la memoria caché después de ejecutar DBCC FREESYSTEMCACHE WITH MARK_IN_USE_FOR_REMOVAL.  
  
 NO_INFOMSGS  
 Suprime todos los mensajes de información.  
  
## <a name="remarks"></a>Comentarios  
Al ejecutar DBCC FREESYSTEMCACHE se borra la memoria caché del plan para la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Al borrar la memoria caché de planes, se provoca una nueva compilación de todos los planes de ejecución posteriores y puede ocasionar una disminución repentina y temporal del rendimiento de las consultas. Para cada almacén de caché borrado de la caché del plan, el registro de errores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contendrá el siguiente mensaje informativo: "[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ha detectado %d instancias de vaciado del almacén de caché '%s' (parte de la caché del plan) debido a operaciones 'DBCC FREEPROCCACHE' o 'DBCC FREESYSTEMCACHE'". Este mensaje se registra cada cinco minutos siempre que se vacíe la memoria caché dentro de ese intervalo de tiempo.

## <a name="result-sets"></a>Conjuntos de resultados  
DBCC FREESYSTEMCACHE devuelve: "ejecución de DBCC completada. Si DBCC imprime algún mensaje de error, póngase en contacto con su administrador del sistema."
  
## <a name="permissions"></a>Permissions  
Requiere el permiso ALTER SERVER STATE en el servidor.
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-releasing-unused-cache-entries-from-a-resource-governor-pool-cache"></a>A. Liberar las entradas no utilizadas de una memoria caché de conjunto de regulador de recursos  
En el ejemplo siguiente se muestra cómo limpiar memorias caché que están dedicadas a un grupo de recursos de servidor del regulador de recursos especificado.
  
```sql
-- Clean all the caches with entries specific to the resource pool named "default".  
DBCC FREESYSTEMCACHE ('ALL', default);  
```  
  
### <a name="b-releasing-entries-from-their-respective-caches-after-they-become-unused"></a>B. Liberar las entradas de sus memorias caché respectivas una vez que dejan de ser utilizadas  
En el ejemplo siguiente se utiliza la cláusula MARK_IN_USE_FOR_REMOVAL para liberar las entradas de todas las memorias caché actuales una vez que las entradas dejan de ser utilizadas.
  
```sql
DBCC FREESYSTEMCACHE ('ALL') WITH MARK_IN_USE_FOR_REMOVAL;  
```  
  
## <a name="see-also"></a>Vea también  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[DBCC FREEPROCCACHE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-freeproccache-transact-sql.md)  
[DBCC FREESESSIONCACHE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-freesessioncache-transact-sql.md)  
[Regulador de recursos](../../relational-databases/resource-governor/resource-governor.md)
  
  

