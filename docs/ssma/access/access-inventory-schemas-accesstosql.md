---
title: Obtener acceso a los esquemas de inventario (AccessToSQL) | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssma-access
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: "17"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8d3c34d87adbe5e854b9de2f49bda5492583298d
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="access-inventory-schemas-accesstosql"></a>Esquemas de inventario de acceso (AccessToSQL)
En las siguientes secciones se describen las tablas que se crean de SSMA al exportar esquemas de acceso a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
## <a name="databases"></a>Bases de datos  
Metadatos de la base de datos se exportan a la **SSMA_Access_InventoryDatabases** tabla. Esta tabla contiene las columnas siguientes:  
  
|Nombre de la columna|Tipo de datos|Description|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|Un GUID que identifica de forma única cada base de datos. Esta columna también es la clave principal de la tabla.|  
|**DatabaseName**|**nvarchar(4000)**|El nombre de la base de datos de Access.|  
|**ExportTime**|**datetime**|La fecha y hora de que creación de estos metadatos por SSMA.|  
|**FilePath**|**nvarchar(4000)**|El nombre completo de ruta de acceso y de la base de datos de Access.|  
|**Tamaño de archivo**|**bigint**|El tamaño de la base de datos de Access en KB.|  
|**FileOwner**|**nvarchar(4000)**|La cuenta de Windows que se especifica como el propietario de la base de datos de Access.|  
|**DateCreated**|**datetime**|La fecha y hora de que creación de la base de datos de Access.|  
|**DateModified**|**datetime**|La fecha y hora de que última modificación de la base de datos de Access.|  
|**TablesCount**|**int**|El número de tablas en la base de datos de Access.|  
|**QueriesCount**|**int**|El número de consultas en la base de datos de Access.|  
|**FormsCount**|**int**|La cantidad de formularios en la base de datos de Access.|  
|**ModulesCount**|**int**|El número de módulos en la base de datos de Access.|  
|**ReportsCount**|**int**|El número de informes en la base de datos de Access.|  
|**MacrosCount**|**int**|El número de macros en la base de datos de Access.|  
|**AccessVersion**|**nvarchar(4000)**|La versión de Access de la base de datos.|  
|**Intercalación**|**nvarchar(4000)**|La intercalación de la base de datos de Access. Las intercalaciones determinan cómo se ordena y compara cadenas de una base de datos.|  
|**JetVersion**|**nvarchar(4000)**|Versión del motor de base de datos de Jet. Bases de datos de Access utilizan el motor de base de datos de Jet subyacente.|  
|**IsUpdatable**|**bit**|Indica si se puede actualizar la base de datos. Si el valor es 1, la base de datos es actualizable. Si el valor es 0, la base de datos es de solo lectura.|  
|**QueryTimeout**|**int**|El ODBC consulta espera valor configurado para la base de datos, en segundos. El valor predeterminado es 60 segundos.|  
  
## <a name="tables"></a>Tablas  
Metadatos de las tablas se exportan a la **SSMA_Access_InventoryTables** tabla. Esta tabla contiene las columnas siguientes:  
  
|Nombre de la columna|Tipo de datos|Description|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|Identifica la base de datos que contiene esta tabla.|  
|**TableId**|**uniqueidentifier**|Un GUID que identifica de forma única la tabla. Esta columna también es la clave principal de la tabla.|  
|**Nombre de tabla**|**nvarchar(4000)**|Nombre de la tabla.|  
|**RowsCount**|**int**|Número de filas de la tabla.|  
|**ValidationRule**|**nvarchar(4000)**|La regla que define una entrada válida para la tabla. Si no existe ninguna regla de validación, el campo contendrá una cadena vacía.|  
|**LinkedTable**|**nvarchar(4000)**|Otra tabla, si hay alguno, que se vincula con la tabla. Vincular tablas permite las adiciones, eliminaciones y actualizaciones de la otra tabla mediante el uso de esta tabla.|  
|**ExternalSource**|**nvarchar(4000)**|El origen de datos, si hay alguno, que está asociado a la tabla. Si una tabla está vinculada, tiene un origen de datos externo especificado en este campo.|  
  
## <a name="columns"></a>Columnas  
Metadatos de columna se exportan a la **SSMA_Access_InventoryColumns** tabla. Esta tabla contiene las columnas siguientes:  
  
|Nombre de la columna|Tipo de datos|Description|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|Identifica la base de datos que contiene esta columna.|  
|**TableId**|**uniqueidentifier**|Identifica la tabla que contiene esta columna.|  
|**ColumnId**|**int**|Incremento entero que identifica la columna. **ColumnId** es la clave principal de la tabla.|  
|**ColumnName**|**nvarchar(4000)**|Nombre de la columna.|  
|**IsNullable**|**bit**|Especifica si la columna puede contener valores null. Si el valor es 1, la columna puede contener valores null. Si el valor es 0, la columna no puede contener valores null. Tenga en cuenta que la regla de validación puede utilizarse también para evitar que los valores null.|  
|**DataType**|**nvarchar(4000)**|Tipo de datos de acceso de la columna, como **texto** o **largo**.|  
|**Disautoincrement**|**bit**|Especifica si la columna incrementa automáticamente valores enteros. Si el valor es 1, los enteros se incrementa automáticamente.|  
|**Ordinal**|**smallint**|El orden de la columna en la tabla, comenzando por cero.|  
|**DefaultValue**|**nvarchar(4000)**|El valor predeterminado para la columna.|  
|**ValidationRule**|**nvarchar(4000)**|La regla que se utiliza para validar los datos se agreguen o se actualicen en la columna.|  
  
## <a name="indexes"></a>Índices  
Metadatos de índice se exportan a la **SSMA_Access_InventoryIndexes** tabla. Esta tabla contiene las columnas siguientes:  
  
|Nombre de la columna|Tipo de datos|Description|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|Identifica la base de datos que contiene este índice.|  
|**TableId**|**uniqueidentifier**|Identifica la tabla que contiene este índice.|  
|**IndexId**|**int**|Incremento entero que identifica el índice. Esta columna es la clave principal de la tabla.|  
|**IndexName**|**nvarchar(4000)**|El nombre del índice.|  
|**ColumnsIncluded**|**nvarchar(4000)**|Enumera las columnas que se incluyen en el índice. Los nombres de columna están separados por un punto y coma.|  
|**IsUnique**|**bit**|Especifica si cada elemento en el índice debe ser único. En un índice de varias columnas, la combinación de valores debe ser única. Si el valor es 1, el índice exige valores únicos.|  
|**IsPK**|**bit**|Especifica si el índice se creó automáticamente como parte de la definición de la clave principal.|  
|**IsClustered**|**bit**|Especifica si el índice está agrupado. Un índice clúster reorganiza el almacenamiento físico de los datos. Una tabla puede tener solo un índice clúster.|  
  
## <a name="foreign-keys"></a>Claves externas  
Los metadatos de clave externo se exportan a la **SSMA_Access_InventoryForeignKeys** tabla. Esta tabla contiene las columnas siguientes:  
  
|Nombre de la columna|Tipo de datos|Description|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|Identifica la base de datos que contiene esta clave externa.|  
|**TableId**|**uniqueidentifier**|Identifica la tabla que contiene esta clave externa.|  
|**ForeignKeyId**|**int**|Incremento entero que identifica la clave externa. Esta columna es la clave principal de la tabla.|  
|**ForeignKeyName**|**nvarchar(4000)**|El nombre del índice.|  
|**ReferencedTableId**|**uniqueidentifier**|Identifica la tabla que contiene las columnas de origen.|  
|**SourceColumns**|**nvarchar(4000)**|Muestra la columna de clave externa o las columnas.|  
|**ReferencedColumns**|**nvarchar(4000)**|Muestra la columna de clave principal o las columnas que se hace referencia a la clave externa.|  
|**IsCascadeForUpdate**|**bit**|Especifica que si se actualiza el valor de clave principal, también se actualizan todas las filas que hacen referencia a ese valor de clave.|  
|**IsCascadeForDelete**|**bit**|Especifica que si se elimina el valor de clave principal, también se eliminan todas las filas que hacen referencia a ese valor de clave.|  
|**IsEnforced**|**bit**|Especifica que se aplica la restricción foreign key.|  
  
## <a name="queries"></a>Consultas  
Metadatos de la consulta se exportan a la **SSMA_Access_InventoryQueries** tabla. Esta tabla contiene las columnas siguientes:  
  
|Nombre de la columna|Tipo de datos|Description|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|Identifica la base de datos que contiene esta consulta.|  
|**QueryId**|**int**|Incremento entero que identifica la consulta. Esta columna es la clave principal de la tabla.|  
|**Nombredeconsulta**|**nvarchar(4000)**|El nombre de la consulta.|  
|**QueryText**|**nvarchar(4000)**|El código de consulta SQL, como una instrucción SELECT.|  
|**IsUpdateable**|**bit**|Especifica si la consulta es actualizable o de solo lectura.|  
|**QueryType**|**nvarchar(4000)**|Especifica el tipo de consulta, como **seleccione** o **SetOperation**.|  
|**ExternalSource**|**nvarchar(4000)**|Si la consulta hace referencia a un origen de datos externo, ésta es la cadena de conexión usada por la consulta.|  
  
## <a name="forms"></a>formularios  
Metadatos de formulario se exportan a la **SSMA_Access_InventoryForms** tabla. Esta tabla contiene las columnas siguientes:  
  
|Nombre de la columna|Tipo de datos|Description|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|Identifica la base de datos que contiene este formulario.|  
|**Idform**|**int**|Incremento entero que identifica el formulario. Esta columna es la clave principal de la tabla.|  
|**FormName**|**nvarchar(4000)**|El nombre del formulario.|  
  
## <a name="macros"></a>Macros  
Macro metadatos se exportan a la **SSMA_Access_InventoryMacros** tabla. Esta tabla contiene las columnas siguientes:  
  
|Nombre de la columna|Tipo de datos|Description|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|Identifica la base de datos que contiene la macro.|  
|**MacroId**|**int**|Incremento entero que identifica la macro. Esta columna es la clave principal de la tabla.|  
|**Nombredemacro**|**nvarchar(4000)**|El nombre de la macro.|  
  
## <a name="reports"></a>Informes  
Metadatos del informe se exportan a la **SSMA_Access_InventoryReports** tabla. Esta tabla contiene las columnas siguientes:  
  
|Nombre de la columna|Tipo de datos|Description|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|Identifica la base de datos que contiene el informe.|  
|**Identificador informe que**|**int**|Incremento entero que identifica el informe. Esta columna es la clave principal de la tabla.|  
|**ReportName**|**nvarchar(4000)**|Nombre del informe.|  
  
## <a name="modules"></a>Módulos  
Los metadatos del módulo se exportan a la **SSMA_Access_InventoryModules** tabla. Esta tabla contiene las columnas siguientes:  
  
|Nombre de la columna|Tipo de datos|Description|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|Identifica la base de datos que contiene el módulo.|  
|**Identificador de módulo**|**int**|Incremento entero que identifica el módulo. Esta columna es la clave principal de la tabla.|  
|**ModuleName**|**nvarchar(4000)**|El nombre del módulo.|  
  
## <a name="see-also"></a>Vea también  
[Exportación de un inventario de Access](http://msdn.microsoft.com/en-us/7e1941fb-3d14-4265-aff6-c77a4026d0ed)  
  
