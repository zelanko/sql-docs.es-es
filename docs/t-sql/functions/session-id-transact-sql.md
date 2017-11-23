---
title: SESSION_ID (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
ms.assetid: 2a0d500a-f6c8-490f-9abd-3ae824986404
caps.latest.revision: "9"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ee58b2f33f10faae7a93c3cea1e810709bebf45f
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="sessionid-transact-sql"></a>SESSION_ID (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Devuelve el identificador del elemento actual [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] o [!INCLUDE[ssPDW_md](../../includes/sspdw-md.md)] sesión.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "icono de vínculo de tema") [convenciones de sintaxis de Transact-SQL &#40; Transact-SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
-- Azure SQL Data Warehouse and Parallel Data Warehouse  
SESSION_ID ( )  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve un **nvarchar (32)** valor.  
  
## <a name="general-remarks"></a>Notas generales  
 El identificador de sesión se asigna a cada conexión de usuario cuando se realiza la conexión. Conserva para la duración de la conexión. Cuando finaliza la conexión, se libera el identificador de sesión.  
  
 El identificador de sesión comienza con los caracteres alfabéticos 'SID'. Estos distinguen mayúsculas de minúsculas y debe escribirse en mayúsculas cuando se utiliza el identificador de sesión en [!INCLUDE[DWsql](../../includes/dwsql-md.md)] comandos.  
  
 Puede consultar la vista [sys.dm_pdw_exec_sessions](http://msdn.microsoft.com/en-us/5b656c55-427f-4306-8bd9-9d7987c203d9) para recuperar la misma información que esta función.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se devuelve el identificador de sesión actual.  
  
```  
SELECT SESSION_ID();  
```  
  
## <a name="see-also"></a>Vea también  
 [Db_name &#40; Transact-SQL &#41;](../../t-sql/functions/db-name-transact-sql.md)   
 [VERSIÓN &#40; Almacenamiento de datos SQL &#41;](../../t-sql/functions/version-transact-sql-configuration-functions.md)
  
  
