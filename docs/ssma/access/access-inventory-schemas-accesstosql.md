---
title: Obtener acceso a los esquemas de inventario (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- columns table
- databases table
- exported metadata
- exporting, schemas of exported metadata
- foreign keys table
- forms table
- indexes, table
- inventory schemas
- macros table
- modules table
- queries table
- reference, inventory schemas
- reports table
- schemas of exported metadata
- schemas, exported metadata
- SSMA_Access_InventoryColumns
- SSMA_Access_InventoryDatabases
- SSMA_Access_InventoryForeignKeys
- SSMA_Access_InventoryForms
- SSMA_Access_InventoryIndexes
- SSMA_Access_InventoryMacros
- SSMA_Access_InventoryModules
- SSMA_Access_InventoryQueries
- SSMA_Access_InventoryReports
- SSMA_Access_InventoryTables
- tables, inventory
ms.assetid: fdd3cff2-4d62-4395-8acf-71ea8f17f524
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: b0344fcfa5a5b174ef080a5eac431cebf6372842
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/16/2018
ms.locfileid: "40393502"
---
# <a name="access-inventory-schemas-accesstosql"></a>Esquemas de inventario de Access (AccessToSQL)
Las siguientes secciones describen las tablas que se crean mediante SSMA al exportar esquemas de acceso a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="databases"></a>Bases de datos  
Metadatos de la base de datos se exportan a la **SSMA_Access_InventoryDatabases** tabla. Esta tabla contiene las columnas siguientes:  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|Un GUID que identifica de forma única cada base de datos. Esta columna también es la clave principal de la tabla.|  
|**DatabaseName**|**nvarchar(4000)**|El nombre de la base de datos de Access.|  
|**ExportTime**|**datetime**|La fecha y hora de que creación de estos metadatos por SSMA.|  
|**FilePath**|**nvarchar(4000)**|El nombre completo de ruta de acceso y de la base de datos de Access.|  
|**Tamaño de archivo**|**bigint**|El tamaño de la base de datos en KB.|  
|**FileOwner**|**nvarchar(4000)**|La cuenta de Windows que se especifica como el propietario de la base de datos de Access.|  
|**DateCreated**|**datetime**|La fecha y hora de que creación de la base de datos de Access.|  
|**DateModified**|**datetime**|La fecha y hora de que última modificación de la base de datos de Access.|  
|**TablesCount**|**int**|El número de tablas en la base de datos de Access.|  
|**QueriesCount**|**int**|El número de consultas en la base de datos de Access.|  
|**FormsCount**|**int**|El número de formularios en la base de datos de Access.|  
|**ModulesCount**|**int**|El número de módulos en la base de datos de Access.|  
|**ReportsCount**|**int**|El número de informes en la base de datos de Access.|  
|**MacrosCount**|**int**|El número de macros en la base de datos de Access.|  
|**AccessVersion**|**nvarchar(4000)**|La versión de la base de datos de Access.|  
|**Intercalación**|**nvarchar(4000)**|La intercalación de la base de datos de Access. Las intercalaciones determinan cómo una base de datos se ordena y compara las cadenas.|  
|**JetVersion**|**nvarchar(4000)**|Versión del motor de base de datos de Jet. Bases de datos de acceso utilizan el motor de base de datos Jet subyacente.|  
|**IsUpdatable**|**bit**|Indica si se puede actualizar la base de datos. Si el valor es 1, la base de datos es actualizable. Si el valor es 0, la base de datos es de sólo lectura.|  
|**QueryTimeout**|**int**|El ODBC consulta espera valor configurado para la base de datos, en segundos. El valor predeterminado es 60 segundos.|  
  
## <a name="tables"></a>Tablas  
Metadatos de tabla se exportan a la **SSMA_Access_InventoryTables** tabla. Esta tabla contiene las columnas siguientes:  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|Identifica la base de datos que contiene esta tabla.|  
|**TableId**|**uniqueidentifier**|Un GUID que identifica la tabla. Esta columna también es la clave principal de la tabla.|  
|**TableName**|**nvarchar(4000)**|Nombre de la tabla.|  
|**RowsCount**|**int**|Número de filas de la tabla.|  
|**ValidationRule**|**nvarchar(4000)**|La regla que define una entrada válida para la tabla. Si no existe ninguna regla de validación, el campo contendrá una cadena vacía.|  
|**LinkedTable**|**nvarchar(4000)**|Otra tabla, si hay alguno, que se vincula con la tabla. Vincular tablas permite que las adiciones, eliminaciones y actualizaciones a la otra tabla mediante el uso de esta tabla.|  
|**ExternalSource**|**nvarchar(4000)**|El origen de datos, si hay alguno, que está asociado a la tabla. Si está vinculada a una tabla, tiene un origen de datos externo especificado en este campo.|  
  
## <a name="columns"></a>Columnas  
Metadatos de columna se exportan a la **SSMA_Access_InventoryColumns** tabla. Esta tabla contiene las columnas siguientes:  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|Identifica la base de datos que contiene esta columna.|  
|**TableId**|**uniqueidentifier**|Identifica la tabla que contiene esta columna.|  
|**ColumnId**|**int**|Un entero incremental que identifica la columna. **ColumnId** es la clave principal para la tabla.|  
|**ColumnName**|**nvarchar(4000)**|Nombre de la columna.|  
|**IsNullable**|**bit**|Especifica si la columna puede contener valores null. Si el valor es 1, la columna puede contener valores null. Si el valor es 0, la columna no puede contener valores null. Tenga en cuenta que la regla de validación también puede usarse para evitar que los valores null.|  
|**DataType**|**nvarchar(4000)**|Tipo de datos acceso de la columna, como **texto** o **largo**.|  
|**Disautoincrement**|**bit**|Especifica si la columna incrementa automáticamente los valores enteros. Si el valor es 1, los enteros se incrementa automáticamente.|  
|**Ordinal**|**smallint**|El orden de la columna en la tabla, empezando desde cero.|  
|**DefaultValue**|**nvarchar(4000)**|El valor predeterminado de la columna.|  
|**ValidationRule**|**nvarchar(4000)**|La regla que se utiliza para validar los datos se agrega o se actualiza en la columna.|  
  
## <a name="indexes"></a>Índices  
Metadatos de índice se exportan a la **SSMA_Access_InventoryIndexes** tabla. Esta tabla contiene las columnas siguientes:  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|Identifica la base de datos que contiene este índice.|  
|**TableId**|**uniqueidentifier**|Identifica la tabla que contiene este índice.|  
|**IndexId**|**int**|Un entero incremental que identifica el índice. Esta columna es la clave principal de la tabla.|  
|**IndexName**|**nvarchar(4000)**|El nombre del índice.|  
|**ColumnsIncluded**|**nvarchar(4000)**|Enumera las columnas que se incluyen en el índice. Los nombres de columna están separados por punto y coma.|  
|**IsUnique**|**bit**|Especifica si cada elemento en el índice debe ser único. En un índice de varias columna, la combinación de valores debe ser única. Si el valor es 1, el índice exige valores únicos.|  
|**IsPK**|**bit**|Especifica si el índice se creó automáticamente como parte de la definición de la clave principal.|  
|**IsClustered**|**bit**|Especifica si el índice está agrupado. Un índice clúster reorganiza el almacenamiento físico de los datos. Una tabla puede tener sólo un índice agrupado.|  
  
## <a name="foreign-keys"></a>Claves externas  
Los metadatos de clave externo se exportan a la **SSMA_Access_InventoryForeignKeys** tabla. Esta tabla contiene las columnas siguientes:  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|Identifica la base de datos que contiene esta clave externa.|  
|**TableId**|**uniqueidentifier**|Identifica la tabla que contiene esta clave externa.|  
|**ForeignKeyId**|**int**|Un entero incremental que identifica la clave externa. Esta columna es la clave principal de la tabla.|  
|**ForeignKeyName**|**nvarchar(4000)**|El nombre del índice.|  
|**ReferencedTableId**|**uniqueidentifier**|Identifica la tabla que contiene las columnas de origen.|  
|**SourceColumns**|**nvarchar(4000)**|Muestra la columna de clave externa o columnas.|  
|**ReferencedColumns**|**nvarchar(4000)**|Muestra la columna de clave principal o las columnas que se hace referencia a la clave externa.|  
|**IsCascadeForUpdate**|**bit**|Especifica que si se actualiza el valor de clave principal, también se actualizan todas las filas que hacen referencia a ese valor de clave.|  
|**IsCascadeForDelete**|**bit**|Especifica que si se elimina el valor de clave principal, también se eliminan todas las filas que hacen referencia a ese valor de clave.|  
|**IsEnforced**|**bit**|Especifica que se aplica la restricción foreign key.|  
  
## <a name="queries"></a>Consultas  
Metadatos de la consulta se exportan a la **SSMA_Access_InventoryQueries** tabla. Esta tabla contiene las columnas siguientes:  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|Identifica la base de datos que contiene esta consulta.|  
|**QueryId**|**int**|Un entero incremental que identifica la consulta. Esta columna es la clave principal de la tabla.|  
|**QueryName**|**nvarchar(4000)**|El nombre de la consulta.|  
|**QueryText**|**nvarchar(4000)**|El código de consulta SQL, como una instrucción SELECT.|  
|**IsUpdateable**|**bit**|Especifica si la consulta es actualizable o de solo lectura.|  
|**QueryType**|**nvarchar(4000)**|Especifica el tipo de consulta, como **seleccione** o **SetOperation**.|  
|**ExternalSource**|**nvarchar(4000)**|Si la consulta hace referencia a un origen de datos externo, se trata la cadena de conexión utilizada por la consulta.|  
  
## <a name="forms"></a>Formularios  
Formulario metadatos se exportan a la **SSMA_Access_InventoryForms** tabla. Esta tabla contiene las columnas siguientes:  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|Identifica la base de datos que contiene este formulario.|  
|**Idform**|**int**|Un entero incremental que identifica el formulario. Esta columna es la clave principal de la tabla.|  
|**FormName**|**nvarchar(4000)**|El nombre del formulario.|  
  
## <a name="macros"></a>Macros  
Macro metadatos se exportan a la **SSMA_Access_InventoryMacros** tabla. Esta tabla contiene las columnas siguientes:  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|Identifica la base de datos que contiene la macro.|  
|**MacroId**|**int**|Un entero incremental que identifica la macro. Esta columna es la clave principal de la tabla.|  
|**Nombredemacro**|**nvarchar(4000)**|El nombre de la macro.|  
  
## <a name="reports"></a>Informes  
Los metadatos del informe se exportan a la **SSMA_Access_InventoryReports** tabla. Esta tabla contiene las columnas siguientes:  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|Identifica la base de datos que contiene el informe.|  
|**ReportId**|**int**|Un entero incremental que identifica el informe. Esta columna es la clave principal de la tabla.|  
|**ReportName**|**nvarchar(4000)**|Nombre del informe.|  
  
## <a name="modules"></a>Módulos  
Metadatos del módulo se exportan a la **SSMA_Access_InventoryModules** tabla. Esta tabla contiene las columnas siguientes:  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|Identifica la base de datos que contiene el módulo.|  
|**Identificador de módulo**|**int**|Un entero incremental que identifica el módulo. Esta columna es la clave principal de la tabla.|  
|**ModuleName**|**nvarchar(4000)**|El nombre del módulo.|  
  
## <a name="see-also"></a>Vea también  
[Exportación de un inventario de Access](exporting-an-access-inventory-accesstosql.md)  
  
