---
title: DROP SENSITIVITY CLASSIFICATION (Transact-SQL) | Microsoft Docs
ms.date: 06/17/2018
ms.reviewer: ''
ms.prod: sql
ms.technology: t-sql
ms.topic: language-reference
ms.custom: ''
ms.manager: craigg
ms.author: giladm
author: giladmit
f1_keywords:
- DROP SENSITIVITY CLASSIFICATION
- DROP_SENSITIVITY_CLASSIFICATION
dev_langs:
- TSQL
helpviewer_keywords:
- DROP SENSITIVITY CLASSIFICATION statement
- dropping labels
- drop labels
- removing labels
- remove labels
- classification [SQL]
- labels [SQL]
- information types
- data classification
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 5e873944e68a05b29ed865572202e7e2b4438d76
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2018
ms.locfileid: "43816901"
---
# <a name="drop-sensitivity-classification-transact-sql"></a>DROP SENSITIVITY CLASSIFICATION (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

Quita los metadatos de la clasificación de confidencialidad de una o varias columnas de base de datos.

## <a name="syntax"></a>Sintaxis

```sql
DROP SENSITIVITY CLASSIFICATION FROM
    <object_name> [, ...n ]

<object_name> ::=
{
    [schema_name.]table_name.column_name
}
```  

## <a name="arguments"></a>Argumentos  

*object_name* ([schema_name.]table_name.column_name)

Es el nombre de la columna de base de datos de la que se va a quitar la clasificación. Actualmente solo se admite la clasificación de columnas.
    - *schema_name* (opcional): es el nombre del esquema al que pertenece la columna clasificada.
    - *table_name*: es el nombre de la tabla a la que pertenece la columna clasificada.
    - *column_name*: es el nombre de la columna de la que se va a quitar la clasificación.

## <a name="remarks"></a>Notas  

- Se pueden quitar varas clasificaciones de objetos con una sola instrucción "DROP SENSITIVITY CLASSIFICATION".

## <a name="permissions"></a>Permisos  

Requiere el permiso ALTER ANY SENSITIVITY CLASSIFICATION. ALTER ANY SENSITIVITY CLASSIFICATION está implícito en el permiso de base de datos ALTER, o en el permiso de servidor CONTROL SERVER.


## <a name="examples"></a>Ejemplos  


### <a name="a-dropping-classification-from-a-single-column"></a>A. Eliminación de la clasificación de una sola columna

En este ejemplo se quita la clasificación de la columna `dbo.sales.price`.  

```sql
DROP SENSITIVITY CLASSIFICATION FROM
    dbo.sales.price
```

### <a name="b-dropping-classification-from-multiple-columns"></a>B. Eliminación de la clasificación de varias columnas

En este ejemplo se quita la clasificación de las columnas `dbo.sales.price`, `dbo.sales.discount` y`SalesLT.Customer.Phone`.  

```sql
DROP SENSITIVITY CLASSIFICATION FROM
    dbo.sales.price, dbo.sales.discount, SalesLT.Customer.Phone  
```

## <a name="see-also"></a>Ver también  

[ADD SENSITIVITY CLASSIFICTION (Transact-SQL)](../../t-sql/statements/add-sensitivity-classification-transact-sql.md)

[sys.sensitivity_classifications (Transact-SQL)](../../relational-databases/system-catalog-views/sys-sensitivity-classifications-transact-sql.md)

[Clasificación y detección de datos de Azure SQL Database](http://aka.ms/sqlip)
