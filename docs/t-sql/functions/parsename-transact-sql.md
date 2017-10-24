---
title: PARSENAME (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- PARSENAME_TSQL
- PARSENAME
dev_langs:
- TSQL
helpviewer_keywords:
- PARSENAME function
- parsing [SQL Server], PARSENAME function
- names [SQL Server], objects
- objects [SQL Server], names
- part of object names [SQL Server]
ms.assetid: abf34f99-9ee9-460b-85b2-930ca5c4b5ae
caps.latest.revision: 38
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 77c7eb1fcde9b073b3c08f412ac0e46519763c74
ms.openlocfilehash: 5664c0a98663897f1d0a3cfa46e8dabab0d6ef7a
ms.contentlocale: es-es
ms.lasthandoff: 10/17/2017

---
# <a name="parsename-transact-sql"></a>PARSENAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all_md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  Devuelve la parte especificada de un nombre de objeto. Las partes de un objeto que se pueden recuperar son el nombre del objeto, nombre del propietario, nombre de la base de datos y nombre del servidor.  
  
> [!NOTE]  
>  La función PARSENAME no indica si existe un objeto con el nombre especificado. PARSENAME solo devuelve la parte especificada del nombre de objeto especificado.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
PARSENAME ( 'object_name' , object_piece )   
```  
  
## <a name="arguments"></a>Argumentos  
 '*object_name*'  
 Es el nombre del objeto del que se desea recuperar la parte de objeto especificada. *object_name* es **sysname**. Este parámetro es un nombre de objeto completo opcionalmente. Si todas las partes del nombre de objeto están completas, este nombre puede tener cuatro partes: el nombre del servidor, de la base de datos, del propietario y del propio objeto.  
  
 *object_piece*  
 Es la parte del objeto que se va a devolver. *object_piece* es de tipo **int**y puede tener estos valores:  
  
 1 = Nombre del objeto  
  
 2 = Nombre del esquema  
  
 3 = Nombre de la base de datos  
  
 4 = Nombre del servidor  
  
## <a name="return-types"></a>Tipos devueltos  
 **nchar**  
  
## <a name="remarks"></a>Comentarios  
 PARSENAME devuelve NULL cuando se cumple una de las siguientes condiciones:  
  
-   Cualquier *object_name* o *object_piece* es NULL.  
  
-   Se produce un error de sintaxis.  
  
 La parte del objeto solicitada tiene una longitud de 0 y no es válido [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] identificador. Un nombre de objeto de longitud cero hace que el nombre completo no sea válido.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se utiliza `PARSENAME` para devolver información acerca de la tabla `Person` de la base de datos `AdventureWorks2012`.  
  
```  
-- Uses AdventureWorks  
  
SELECT PARSENAME('AdventureWorksPDW2012.dbo.DimCustomer', 1) AS 'Object Name';  
SELECT PARSENAME('AdventureWorksPDW2012.dbo.DimCustomer', 2) AS 'Schema Name';  
SELECT PARSENAME('AdventureWorksPDW2012.dbo.DimCustomer', 3) AS 'Database Name';  
SELECT PARSENAME('AdventureWorksPDW2012.dbo.DimCustomer', 4) AS 'Server Name';  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
```
Object Name
------------------------------
DimCustomer

(1 row(s) affected)

Schema Name
------------------------------
dbo

(1 row(s) affected)

Database Name
------------------------------
AdventureWorksPDW2012

(1 row(s) affected)

Server Name
------------------------------
(null)

(1 row(s) affected)
```
  
## <a name="see-also"></a>Vea también  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [Funciones del sistema &#40; Transact-SQL &#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)  
  
  


