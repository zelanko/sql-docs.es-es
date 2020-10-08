---
description: SQLColumns
title: SQLColumns | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLColumns function
ms.assetid: 69d3af44-8196-43ab-8037-cdd06207b171
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f44f2e1c9754096ae08bc64298815a8849f92478
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/07/2020
ms.locfileid: "91810601"
---
# <a name="sqlcolumns"></a>SQLColumns
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  **SQLColumns** devuelve SQL_SUCCESS si existen o no valores para los parámetros *nombrecatálogo*, *TableName*o *columnName* . **SQLFetch** devuelve SQL_NO_DATA si se usan valores no válidos en estos parámetros.  
  
> [!NOTE]  
>  Para los tipos de valores grandes, todos los parámetros de longitud se devolverán con un valor de SQL_SS_LENGTH_UNLIMITED.  
  
 **SQLColumns** se puede ejecutar en un cursor de servidor estático. Un intento de ejecutar **SQLColumns** en un cursor actualizable (dinámico o conjunto de claves) devolverá SQL_SUCCESS_WITH_INFO que indica que se ha cambiado el tipo de cursor.  
  
 El controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client permite notificar información de tablas en servidores vinculados aceptando un nombre de dos partes para el parámetro *CatalogName* : *Linked_Server_Name.Catalog_Name*.  
  
 Para ODBC 2. las aplicaciones *x* que no usan caracteres comodín en *TableName*, **SQLColumns** devuelven información sobre las tablas cuyos nombres coinciden con *TableName* y son propiedad del usuario actual. Si el usuario actual no posee ninguna tabla cuyo nombre coincida con el parámetro *TableName* , **SQLColumns** devuelve información sobre las tablas que pertenecen a otros usuarios, donde el nombre de tabla coincide con el parámetro *TableName* . Para ODBC 2. las aplicaciones *x* que usan caracteres comodín, **SQLColumns** devuelve todas las tablas cuyos nombres coinciden con *TableName*. Para ODBC 3. la *x* aplicaciones **SQLColumns** devuelve todas las tablas cuyos nombres coinciden con *TableName* independientemente del propietario o de si se utilizan caracteres comodín.  
  
 La tabla siguiente muestra las columnas devueltas por el conjunto de resultados:  
  
|Nombre de la columna|Descripción|  
|-----------------|-----------------|  
|DATA_TYPE|Devuelve SQL_VARCHAR, SQL_VARBINARY o SQL_WVARCHAR para los tipos de datos **VARCHAR (Max)** .|  
|TYPE_NAME|Devuelve "VARCHAR", "varbinary" o "nvarchar" para los tipos de datos **VARCHAR (Max)**, **varbinary (Max)** y **nvarchar (Max)** .|  
|COLUMN_SIZE|Devuelve SQL_SS_LENGTH_UNLIMITED para los tipos de datos **VARCHAR (Max)** que indican que el tamaño de la columna es ilimitado.|  
|BUFFER_LENGTH|Devuelve SQL_SS_LENGTH_UNLIMITED para los tipos de datos **VARCHAR (Max)** que indican que el tamaño del búfer es ilimitado.|  
|SQL_DATA_TYPE|Devuelve SQL_VARCHAR, SQL_VARBINARY o SQL_WVARCHAR para los tipos de datos **VARCHAR (Max)** .|  
|CHAR_OCTET_LENGTH|Devuelve la longitud máxima de una columna de caracteres o binaria. Devuelve 0 para indicar que el tamaño es ilimitado.|  
|SS_XML_SCHEMACOLLECTION_CATALOG_NAME|Devuelve el nombre del catálogo donde se define un nombre de colección de esquemas XML. Si no se encuentra el nombre de catálogo, esta variable contiene una cadena vacía.|  
|SS_XML_SCHEMACOLLECTION_SCHEMA_NAME|Devuelve el nombre del esquema donde se define un nombre de colección de esquemas XML. Si no se encuentra el nombre de esquema, esta variable contiene una cadena vacía.|  
|SS_XML_SCHEMACOLLECTION_NAME|Devuelve el nombre de una colección de esquemas XML. Si no se encuentra el nombre, esta variable contiene una cadena vacía.|  
|SS_UDT_CATALOG_NAME|Nombre del catálogo que contiene el UDT (tipo definido por el usuario).|  
|SS_UDT_SCHEMA_NAME|Nombre del esquema que contiene el UDT.|  
|SS_UDT_ASSEMBLY_TYPE_NAME|Nombre completo de ensamblado del UDT.|  
  
 En los UDT, la columna de TYPE_NAME existente se usa para indicar el nombre del UDT; por lo tanto, no se debe agregar ninguna columna adicional al conjunto de resultados de **SQLColumns** o [SQLProcedureColumns](../../relational-databases/native-client-odbc-api/sqlprocedurecolumns.md). El DATA_TYPE de una columna o parámetro de UDT es SQL_SS_UDT.  
  
 Para el UDT de los parámetros, puede utilizar los nuevos descriptores específicos del controlador definidos anteriormente para obtener o establecer las propiedades de metadatos adicionales de un UDT, en caso de que el servidor devuelva o requiera esta información.  
  
 Cuando un cliente se conecta a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y llama a SQLColumns, el uso de valores NULL o comodín para el parámetro de entrada del catálogo no devolverá información de otros catálogos. En su lugar, solo se devolverá información sobre el catálogo actual. El cliente puede llamar primero a SQLTables para determinar en qué catálogo se encuentra la tabla deseada. A continuación, el cliente puede usar ese valor de catálogo para el parámetro de entrada de catálogo en su llamada a SQLColumns para recuperar información acerca de las columnas de esa tabla.  
  
## <a name="sqlcolumns-and-table-valued-parameters"></a>Parámetros de SQLColumns y con valores de tabla  
 El conjunto de resultados devuelto por SQLColumns depende de la configuración de SQL_SOPT_SS_NAME_SCOPE. Para obtener más información, vea [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md). Se han agregado las columnas siguientes para los parámetros con valores de tabla:  
  
|Nombre de la columna|Tipo de datos|Contenido|  
|-----------------|---------------|--------------|  
|SS_IS_COMPUTED|Smallint|Para una columna de TABLE_TYPE, este es SQL_TRUE si se trata de una columna calculada; de lo contrario, SQL_FALSE.|  
|SS_IS_IDENTITY|Smallint|SQL_TRUE si se trata de una columna de identidad; de lo contrario, SQL_FALSE.|  
  
 Para obtener más información sobre los parámetros con valores de tabla, vea [parámetros con valores de tabla &#40;ODBC&#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="sqlcolumns-support-for-enhanced-date-and-time-features"></a>Compatibilidad de SQLColumns con las características mejoradas de fecha y hora  
 Para obtener información sobre los valores devueltos para los tipos de fecha y hora, vea [metadatos de catálogo](../../relational-databases/native-client-odbc-date-time/metadata-catalog.md).  
  
 Para obtener más información, vea [mejoras de fecha y hora &#40;ODBC&#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqlcolumns-support-for-large-clr-udts"></a>Compatibilidad de SQLColumns con UDT CLR grandes  
 **SQLColumns** admite tipos definidos por el usuario (UDT) CLR grandes. Para obtener más información, vea [tipos CLR grandes definidos por el usuario &#40;ODBC&#41;](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="sqlcolumns-support-for-sparse-columns"></a>Compatibilidad de SQLColumns con columnas dispersas  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Se han agregado dos columnas específicas al conjunto de resultados para SQLColumns:  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|SS_IS_SPARSE|**Smallint**|Si la columna es una columna dispersa, tiene el valor SQL_TRUE; de lo contrario, SQL_FALSE.|  
|SS_IS_COLUMN_SET|**Smallint**|Si la columna es la **COLUMN_SET** columna, se SQL_TRUE; de lo contrario, SQL_FALSE.|  
  
 De acuerdo con la especificación de ODBC, SS_IS_SPARSE y SS_IS_COLUMN_SET aparecen antes de todas las columnas específicas del controlador que se agregaron a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] las versiones anteriores a [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] y después de todas las columnas asignadas por el propio ODBC.  
  
 El conjunto de resultados devuelto por SQLColumns depende de la configuración de SQL_SOPT_SS_NAME_SCOPE. Para obtener más información, vea [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md).  
  
 Para obtener más información sobre las columnas dispersas en ODBC, vea [compatibilidad con columnas Dispersas &#40;odbc&#41;](../../relational-databases/native-client/odbc/sparse-columns-support-odbc.md).  
  
## <a name="see-also"></a>Consulte también  
 [SQLColumns (función)](../../odbc/reference/syntax/sqlcolumns-function.md)   
 [ODBC API Implementation Details](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
