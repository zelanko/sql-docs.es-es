---
title: sys.sensitivity_classifications (Transact-SQL) | Microsoft Docs
ms.date: 03/25/2019
ms.reviewer: ''
ms.prod: sql
ms.technology: t-sql
ms.topic: language-reference
ms.custom: ''
ms.manager: craigg
ms.author: arib
author: vainolo
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
ms.openlocfilehash: a47b311af70c58c36c8c467115c277f300092376
ms.sourcegitcommit: 45a9d7ffc99502c73f08cb937cbe9e89d9412397
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/22/2019
ms.locfileid: "66014430"
---
# <a name="syssensitivityclassifications-transact-sql"></a>sys.sensitivity_classifications (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-asdw-xxx-md.md)]

Devuelve una fila para cada elemento clasificado en la base de datos.

|Nombre de columna|Tipo de datos|Descripción|
|-----------------|---------------|-----------------|  
|**class**|**int**|Identifica la clase del elemento en el que existe la clasificación|  
|**class_desc**|**varchar(16)**|Una descripción de la clase del elemento en el que existe la clasificación|  
|**major_id**|**int**|Identificador del elemento en el que existe la clasificación. < br \>< br \>si class es 0, major_id siempre es 0.<br>Si class es 1, 2 ó 7, major_id es object_id.|  
|**minor_id**|**int**|Id. secundario del elemento en el que existe la clasificación, interpretado según su clase.<br><br>Si clase = 1, minor_id es column_id (si columna), o 0 (si objeto).<br>Si class = 2, minor_id es parameter_id.<br>Si clase = 7, minor_id es index_id. |  
|**label**|**sysname**|La etiqueta (legibles) asignada para la clasificación de confidencialidad|  
|**label_id**|**sysname**|Un identificador asociado con la etiqueta, que se puede usar un sistema de protección de información, como Azure Information Protection (AIP)|  
|**information_type**|**sysname**|El tipo de información (legibles) asignado para la clasificación de confidencialidad|  
|**information_type_id**|**sysname**|Un identificador asociado con el tipo de información que se puede usar un sistema de protección de información, como Azure Information Protection (AIP)|  
| &nbsp; | &nbsp; | &nbsp; |

## <a name="remarks"></a>Comentarios  

- Esta vista proporciona visibilidad sobre el estado de clasificación de la base de datos. Se puede usar para administrar las clasificaciones de la base de datos, así como para generar informes.
- Se admite actualmente solo clasificación de las columnas de la base de datos. En consecuencia:
    - **clase** -siempre tendrá el valor 1 (que representa una columna)
    - **class_desc** -siempre tendrá el valor *OBJECT_OR_COLUMN*
    - **major_id** -representa el identificador de la tabla que contiene la columna clasificada, correspondiente a sys.all_objects.object_id
    - **minor_id** -representa el identificador de la columna en el que la clasificación no existe, correspondiente con sys.all_columns.column_id

## <a name="examples"></a>Ejemplos

### <a name="a-listing-all-classified-columns-and-their-corresponding-classification"></a>A. Lista de las columnas clasificadas todo y su clasificación correspondiente

El ejemplo siguiente devuelve una tabla que enumera el nombre de tabla, columna, etiqueta, etiqueta ID, tipo de información de Id. de tipo de información para cada columna clasificada en la base de datos.

> [!NOTE]
> Etiqueta es una palabra clave para Azure SQL Data Warehouse.

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
