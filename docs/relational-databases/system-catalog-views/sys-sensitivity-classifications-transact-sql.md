---
title: sys.sensitivity_classifications (Transact-SQL) | Microsoft Docs
ms.date: 03/25/2019
ms.reviewer: ''
ms.prod: sql
ms.technology: t-sql
ms.topic: language-reference
ms.custom: ''
ms.author: mibar
author: barmichal
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
ms.openlocfilehash: a9d14cd93b08c0094ad984a6469b433e0b266479
ms.sourcegitcommit: 77293fb1f303ccfd236db9c9041d2fb2f64bce42
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/12/2019
ms.locfileid: "70929780"
---
# <a name="syssensitivity_classifications-transact-sql"></a>sys.sensitivity_classifications (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-asdw-xxx-md.md)]

Devuelve una fila por cada elemento clasificado en la base de datos.

|Nombre de columna|Tipo de datos|Descripción|
|-----------------|---------------|-----------------|  
|**class**|**int**|Identifica la clase del elemento en el que existe la clasificación|  
|**class_desc**|**varchar(16)**|Descripción de la clase del elemento en el que existe la clasificación|  
|**major_id**|**int**|Identificador del elemento en el que existe la clasificación. < br \>< br \>si la clase es 0, major_id siempre es 0.<br>Si class es 1, 2 ó 7, major_id es object_id.|  
|**minor_id**|**int**|ID. secundario del elemento en el que existe la clasificación, interpretado de acuerdo con su clase.<br><br>Si Class = 1, minor_id es column_id (si la columna), de lo contrario 0 (si es Object).<br>Si class = 2, minor_id es parameter_id.<br>Si Class = 7, minor_id es el tipo de la. |  
|**label**|**sysname**|La etiqueta (inteligible) asignada para la clasificación de confidencialidad|  
|**label_id**|**sysname**|Identificador asociado a la etiqueta, que se puede usar en un sistema de protección de la información, como Azure Information Protection (AIP).|  
|**information_type**|**sysname**|El tipo de información (legible) asignado para la clasificación de confidencialidad|  
|**information_type_id**|**sysname**|IDENTIFICADOR asociado con el tipo de información, que se puede usar en un sistema de protección de la información, como Azure Information Protection (AIP).|  
| &nbsp; | &nbsp; | &nbsp; |

## <a name="remarks"></a>Comentarios  

- Esta vista proporciona visibilidad en el estado de clasificación de la base de datos. Se puede usar para administrar las clasificaciones de la base de datos, así como para generar informes.
- Actualmente solo se admite la clasificación de columnas de base de datos. Por consiguiente
    - **clase** : siempre tendrá el valor 1 (que representa una columna).
    - **class_desc** : siempre tendrá el valor *OBJECT_OR_COLUMN*
    - **major_id** : representa el identificador de la tabla que contiene la columna clasificada, que corresponde a sys. All _objects. object_id
    - **minor_id** : representa el identificador de la columna en la que existe la clasificación, correspondiente a sys. All _columns. column_id

## <a name="examples"></a>Ejemplos

### <a name="a-listing-all-classified-columns-and-their-corresponding-classification"></a>A. Enumerar todas las columnas clasificadas y su clasificación correspondiente

En el ejemplo siguiente se devuelve una tabla que muestra el nombre de la tabla, el nombre de la columna, la etiqueta, el ID. de etiqueta, el tipo de información, el ID. de tipo de información de cada columna clasificada de la base

> [!NOTE]
> Label es una palabra clave para Azure SQL Data Warehouse.

```sql
SELECT
    SCHEMA_NAME(sys.all_objects.schema_id) as SchemaName,
    sys.all_objects.name AS [TableName], sys.all_columns.name As [ColumnName],
    [Label], [Label_ID], [Information_Type], [Information_Type_ID]
FROM
          sys.sensitivity_classifications
left join sys.all_objects on sys.sensitivity_classifications.major_id = sys.all_objects.object_id
left join sys.all_columns on sys.sensitivity_classifications.major_id = sys.all_columns.object_id
                         and sys.sensitivity_classifications.minor_id = sys.all_columns.column_id
```

## <a name="permissions"></a>Permisos  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  

## <a name="see-also"></a>Vea también  

[ADD SENSITIVITY CLASSIFICATION (Transact-SQL)](../../t-sql/statements/add-sensitivity-classification-transact-sql.md)

[DROP SENSITIVITY CLASSIFICATION (Transact-SQL)](../../t-sql/statements/drop-sensitivity-classification-transact-sql.md)

[Clasificación y detección de datos de Azure SQL Database](https://aka.ms/sqlip)
