---
title: Quitar grupo de cargas de trabajo (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP_WORKLOAD_GROUP_TSQL
- DROP WORKLOAD GROUP
dev_langs:
- TSQL
helpviewer_keywords:
- DROP WORKLOAD GROUP statement
ms.assetid: 1cd68450-5b58-4106-a2bc-54197ced8616
caps.latest.revision: 23
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4c68702eea03f7f0b2ab4b94614939c7587166f6
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="drop-workload-group-transact-sql"></a>DROP WORKLOAD GROUP (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Quita un grupo de cargas de trabajo del regulador de recursos definido por el usuario existente.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "icono de vínculo de tema") [convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DROP WORKLOAD GROUP group_name  
[;]  
```  
  
## <a name="arguments"></a>Argumentos  
 *nombre_grupo*  
 Es el nombre de un grupo de cargas de trabajo definido por el usuario existente.  
  
## <a name="remarks"></a>Comentarios  
 La instrucción DROP WORKLOAD GROUP no se permite en los grupos predeterminados o internos del regulador de recursos.  
  
 Si va a ejecutar instrucciones de DDL, se recomienda familiarizarse primero con los estados del regulador de recursos. Para obtener más información, consulte [regulador de recursos](../../relational-databases/resource-governor/resource-governor.md).  
  
 Si un grupo de cargas de trabajo contiene sesiones activas, no se podrá quitar ni mover el grupo de cargas de trabajo a otro grupo de recursos de servidor si se llama a la instrucción ALTER RESOURCE GOVERNOR RECONFIGURE para aplicar el cambio. Para evitar este problema, puede realizar una de las siguientes acciones:  
  
-   Espere hasta que se hayan desconectado todas las sesiones en el grupo afectado y, a continuación, vuelve a ejecutar la instrucción ALTER RESOURCE GOVERNOR RECONFIGURE.  
  
-   Detenga explícitamente las sesiones en el grupo afectado mediante el comando KILL y, a continuación, vuelva a ejecutar la instrucción ALTER RESOURCE GOVERNOR RECONFIGURE.  
  
-   Reinicie el servidor. Una vez completado el proceso del reinicio, no se creará el grupo eliminado y un grupo movido utilizará la nueva asignación del grupo de recursos de servidor.  
  
-   En un escenario en el que ha emitido la instrucción DROP WORKLOAD GROUP pero no desea detener explícitamente las sesiones para aplicar el cambio, puede recrear el grupo si utiliza el mismo nombre que tenía antes de emitir la instrucción DROP y, a continuación, mueve el grupo al grupo de recursos de servidor original. Para aplicar los cambios, ejecute la instrucción ALTER RESOURCE GOVERNOR RECONFIGURE.  
  
## <a name="permissions"></a>Permissions  
 Requiere el permiso CONTROL SERVER.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se quita el grupo de cargas de trabajo denominado `adhoc`.  
  
```  
DROP WORKLOAD GROUP adhoc;  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Regulador de recursos](../../relational-databases/resource-governor/resource-governor.md)   
 [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md)   
 [ALTER WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-workload-group-transact-sql.md)   
 [CREATE RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-resource-pool-transact-sql.md)   
 [ALTER RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-pool-transact-sql.md)   
 [DROP RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-resource-pool-transact-sql.md)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)  
  
  
