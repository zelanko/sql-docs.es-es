---
title: HAS_DBACCESS (Transact-SQL) | Documentos de Microsoft
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
- HAS_DBACCESS_TSQL
- HAS_DBACCESS
dev_langs:
- TSQL
helpviewer_keywords:
- permissions [SQL Server], verifying
- permissions [SQL Server], user access status
- HAS_DBACCESS
- checking permission status
- verifying permission status
- users [SQL Server], access rights status
- testing permissions
- status information [SQL Server], user access
ms.assetid: 99b43a72-0722-4a7b-a493-bdee1c74c7b9
caps.latest.revision: 25
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: efb5681a5ca390fb2c00033dbbfc70c27ae9544e
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="hasdbaccess-transact-sql"></a>HAS_DBACCESS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw_md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  Devuelve información acerca de si el usuario tiene acceso a la base de datos especificada.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
-- Syntax for SQL Server, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
HAS_DBACCESS ( 'database_name' )  
```  
  
## <a name="arguments"></a>Argumentos  
 '*database_name*'  
 El nombre de la base de datos de la que el usuario desea información de acceso. *database_name* es **sysname**.  
  
## <a name="return-types"></a>Tipos devueltos  
 **int**  
  
## <a name="remarks"></a>Comentarios  
 HAS_DBACCESS devuelve 1 si el usuario tiene acceso a la base de datos, 0 si no lo tiene y NULL si el nombre de la base de datos no es válido.  
  
 HAS_DBACCESS devuelve 0 si la base de datos está sin conexión o es sospechosa.  
  
 HAS_DBACCESS devuelve 0 si la base de datos están en modo de usuario único y la está usando otro usuario.  
  
## <a name="permissions"></a>Permissions  
 Debe pertenecer al rol public.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se comprueba si el usuario actual tiene acceso a la base de datos `AdventureWorks2012`.  
  
```  
SELECT HAS_DBACCESS('AdventureWorks2012');  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 En el siguiente ejemplo se comprueba si el usuario actual tiene acceso a la base de datos `AdventureWorksPDW2012`.  
  
```  
SELECT HAS_DBACCESS('AdventureWorksPDW2012');  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [IS_MEMBER &#40; Transact-SQL &#41;](../../t-sql/functions/is-member-transact-sql.md)   
 [IS_SRVROLEMEMBER &#40;Transact-SQL&#41;](../../t-sql/functions/is-srvrolemember-transact-sql.md)  
  
  


