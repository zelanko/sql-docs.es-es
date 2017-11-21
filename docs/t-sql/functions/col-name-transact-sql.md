---
title: COL_NAME (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- COL_NAME
- COL_NAME_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- column properties [SQL Server]
- COL_NAME function
- column names [SQL Server]
- names [SQL Server], columns
ms.assetid: 214144ab-f2bc-4052-83cf-caf0a85c4cc6
caps.latest.revision: 28
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 77c7eb1fcde9b073b3c08f412ac0e46519763c74
ms.openlocfilehash: c697b619907bb3d80fbbff800b2ac29ef574af8d
ms.contentlocale: es-es
ms.lasthandoff: 10/17/2017

---
# <a name="colname-transact-sql"></a>COL_NAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Devuelve el nombre de una columna a partir del número de identificación de tabla y del número de identificación de columna correspondientes especificados.
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
COL_NAME ( table_id , column_id )  
```  
  
## <a name="arguments"></a>Argumentos  
*table_id*  
Es el número de identificación de la tabla que contiene la columna. *table_id* es de tipo **int**.
  
*column_id*  
Es el número de identificación de la columna. *column_id* parámetro es de tipo **int**.
  
## <a name="return-types"></a>Tipos de valor devuelto
**sysname**
  
## <a name="exceptions"></a>Excepciones  
Devuelve NULL si se produce un error o si el autor de la llamada no tiene permiso para ver el objeto.
  
Un usuario solo puede ver los metadatos de elementos protegibles que posea o para los que se le haya concedido permiso. Esto significa que las funciones integradas de emisión de metadatos, como COL_NAME, pueden devolver NULL si el usuario no tiene ningún permiso para el objeto. Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).
  
## <a name="remarks"></a>Comentarios  
El *table_id* y *column_id* parámetros juntos generan una cadena de nombre de columna.
  
Para obtener más información acerca de cómo obtener los números de identificación de tablas y columnas, vea [OBJECT_ID & #40; Transact-SQL & #41; ](../../t-sql/functions/object-id-transact-sql.md).
  
## <a name="examples"></a>Ejemplos  
En el ejemplo siguiente se devuelve el nombre de la primera columna de un ejemplo `Employee` tabla.
  
```sql
-- Uses AdventureWorks  
  
SELECT COL_NAME(OBJECT_ID('dbo.FactResellerSales'), 1) AS FirstColumnName,  
COL_NAME(OBJECT_ID('dbo.FactResellerSales'), 2) AS SecondColumnName;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
ColumnName          
------------   
BusinessEntityID  
```  
  
## <a name="see-also"></a>Vea también
[Expresiones &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
[Funciones de metadatos & #40; Transact-SQL & #41;](../../t-sql/functions/metadata-functions-transact-sql.md)  
[COLUMNPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/columnproperty-transact-sql.md)  
[COL_LENGTH & #40; Transact-SQL & #41;](../../t-sql/functions/col-length-transact-sql.md)
  
  


