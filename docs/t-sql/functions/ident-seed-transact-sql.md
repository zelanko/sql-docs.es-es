---
title: IDENT_SEED (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- IDENT_SEED_TSQL
- IDENT_SEED
dev_langs:
- TSQL
helpviewer_keywords:
- identity columns [SQL Server], IDENT_SEED function
- seed values [SQL Server]
- IDENT_SEED function
ms.assetid: e4cb8eb8-affb-4810-a8a9-0110af3c247a
caps.latest.revision: 45
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 579d578e7e34330c4788db3008417a0da2a84d6b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="identseed-transact-sql"></a>IDENT_SEED (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Devuelve el valor de inicialización original (devuelto como **numeric**(**@@** MAXPRECISION,0)) que se especificó cuando se creó una columna de identidad en una tabla o una vista. La acción de cambiar el valor actual de una columna de identidad utilizando DBCC CHECKIDENT no cambia el valor devuelto por esta función.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
IDENT_SEED ( 'table_or_view' )  
```  
  
## <a name="arguments"></a>Argumentos  
 **'** *table_or_view* **'**  
 Se trata de una [expresión](../../t-sql/language-elements/expressions-transact-sql.md) que especifica la tabla o vista en la que se va a comprobar un valor de inicialización de identidad. *table_or_view* puede ser una constante de cadena de caracteres entre comillas, un nombre de variable, un nombre de función o un nombre de columna. *table_or_view* es **char**, **nchar**, **varchar** o **nvarchar**.  
  
## <a name="return-types"></a>Tipos devueltos  
 **numeric**  
  
## <a name="exceptions"></a>Excepciones  
 Devuelve NULL si se produce un error o si el autor de la llamada no tiene permiso para ver el objeto.  
  
 En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], un usuario solo puede ver los metadatos de elementos protegibles que posea o para los que se le haya concedido permiso. Esto significa que las funciones integradas de emisión de metadatos, como IDENT_SEED, pueden devolver NULL si el usuario no tiene ningún permiso para el objeto. Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-returning-the-seed-value-from-a-specified-table"></a>A. Devolver el valor de inicialización de una tabla especificada  
 En el ejemplo siguiente se devuelve el valor de inicialización de la tabla `Person.Address` en la base de datos [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```  
USE AdventureWorks2012;  
GO  
SELECT IDENT_SEED('Person.Address') AS Identity_Seed;  
GO  
```  
  
### <a name="b-returning-the-seed-value-from-multiple-tables"></a>B. Devolver el valor de inicialización de varias tablas  
 En este ejemplo se devuelven las tablas de la base de datos [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] que contienen una columna de identidad con un valor de inicialización.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT TABLE_SCHEMA, TABLE_NAME,   
   IDENT_SEED(TABLE_SCHEMA + '.' + TABLE_NAME) AS IDENT_SEED  
FROM INFORMATION_SCHEMA.TABLES  
WHERE IDENT_SEED(TABLE_SCHEMA + '.' + TABLE_NAME) IS NOT NULL;  
GO  
```  
  
 A continuación se muestra un conjunto parcial de resultados.  
  
 ```
 TABLE_SCHEMA       TABLE_NAME                   IDENT_SEED  
------------       ---------------------------  -----------  
Person             Address                                1  
Production         ProductReview                          1  
Production         TransactionHistory                100000  
Person             AddressType                            1  
Production         ProductSubcategory                     1  
Person             vAdditionalContactInfo                 1  
dbo                AWBuildVersion                         1
```  
  
## <a name="see-also"></a>Ver también  
 [Expresiones &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [Funciones del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)   
 [IDENT_CURRENT &#40;Transact-SQL&#41;](../../t-sql/functions/ident-current-transact-sql.md)   
 [IDENT_INCR &#40;Transact-SQL&#41;](../../t-sql/functions/ident-incr-transact-sql.md)   
 [DBCC CHECKIDENT &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkident-transact-sql.md)   
 [sys.identity_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-identity-columns-transact-sql.md)  
  
  
