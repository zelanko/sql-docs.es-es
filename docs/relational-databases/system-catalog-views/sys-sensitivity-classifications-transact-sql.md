---
title: Sys.sensitivity_classifications (Transact-SQL) | Documentos de Microsoft
ms.date: 06/17/2018
ms.reviewer: ''
ms.prod: sql
ms.prod_service: sql-database
ms.service: sql-database
ms.technology: t-sql
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
ms.custom: ''
ms.manager: craigg
ms.author: giladm
author: giladmit
f1_keywords:
- 'sys.sensitivity_classifications '
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sensitivity_classifications statement
- dropping labels
- drop labels
- removing labels
- remove labels
- classification [SQL]
- labels [SQL]
- information types
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: d0adbbeb82c06d6a44f3a7439bcbf479d7358401
ms.sourcegitcommit: 70882926439a63ab9d812809429c63040eb9a41b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36262894"
---
# <a name="syssensitivityclassifications-transact-sql"></a>Sys.sensitivity_classifications (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

Devuelve una fila para cada elemento clasificada en la base de datos.

|Nombre de columna|Tipo de datos|Descripción|
|-----------------|---------------|-----------------|  
|**class**|**int**|Identifica la clase del elemento en el que existe la clasificación|  
|**class_desc**|**varchar (16)**|Una descripción de la clase del elemento en el que existe la clasificación|  
|**major_id**|**int**|Identificador del elemento en el que existe la clasificación. < br \>< br \>si class es 0, major_id siempre es 0.<br>Si class es 1, 2 ó 7, major_id es object_id.|  
|**minor_id**|**int**|Id. secundario del elemento en el que existe la clasificación, interpretado de acuerdo con su clase.<br><br>Si clase = 1, minor_id es column_id (si columna), o 0 (si objeto).<br>Si class = 2, minor_id es parameter_id.<br>Si clase = 7, minor_id es index_id. |  
|**label**|**sysname**|La etiqueta (legibles) asignada para la clasificación de sensibilidad|  
|**label_id**|**sysname**|Un identificador asociado a la etiqueta, que puede usarse en un sistema de protección de información como la protección de información de Azure (AIP)|  
|**information_type**|**sysname**|El tipo de información (legibles) asignado para la clasificación de sensibilidad|  
|**information_type_id**|**sysname**|Un identificador asociado con el tipo de información que puede usarse en un sistema de protección de información como la protección de información de Azure (AIP)|  
| &nbsp; | &nbsp; | &nbsp; |

## <a name="remarks"></a>Notas  

- Esta vista proporciona visibilidad sobre el estado de clasificación de la base de datos. Se puede utilizar para administrar las clasificaciones de la base de datos, así como para generar informes.
- Se admite actualmente solo clasificación de las columnas de la base de datos. Por lo tanto:
    - **clase** -siempre tendrá el valor 1 (que representa una columna)
    - **class_desc** -siempre tendrá el valor *OBJECT_OR_COLUMN*
    - **major_id** -representa el identificador de la tabla que contiene la columna clasificada correspondiente con sys.all_objects.object_id
    - **minor_id** -representa el identificador de la columna en el que la clasificación existe, correspondiente con sys.all_columns.column_id

## <a name="examples"></a>Ejemplos

### <a name="a-listing-all-classified-columns-and-their-corresponding-classification"></a>A. Mostrar una lista clasificada de todas las columnas y su clasificación correspondiente

El ejemplo siguiente devuelve una tabla que enumera el nombre de la tabla, el nombre de columna, la etiqueta, identificador, tipo de información, Id. de tipo de información para cada columna clasificada en la base de datos de etiqueta.

```sql
SELECT
    sys.all_objects.name AS TableName, sys.all_columns.name As ColumnName,
    Label, Label_ID, Information_Type, Information_Type_ID
FROM
          sys.sensitivity_classifications
left join sys.all_objects on sys.sensitivity_classifications.major_id = sys.all_objects.object_id
left join sys.all_columns on sys.sensitivity_classifications.major_id = sys.all_columns.object_id
                         and sys.sensitivity_classifications.minor_id = sys.all_columns.column_id
```

## <a name="see-also"></a>Vea también  

[Agregar CLASSIFICTION de sensibilidad (Transact-SQL)](../../t-sql/statements/add-sensitivity-classification-transact-sql.md)

[QUITAR CLASSIFICTION de sensibilidad (Transact-SQL)](../../t-sql/statements/drop-sensitivity-classification-transact-sql.md)

[Introducción a la protección de la información de SQL](http://aka.ms/sqlip)
