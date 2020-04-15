---
title: SQLColumns ? Microsoft Docs
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
ms.openlocfilehash: abce98b64da8de6039f81025201cce25269763a6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302614"
---
# <a name="sqlcolumns"></a>SQLColumns
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  **SQLColumns** devuelve SQL_SUCCESS si existen o no valores para los parámetros *CatalogName*, *TableName*o *ColumnName* . **SQLFetch** devuelve SQL_NO_DATA si se usan valores no válidos en estos parámetros.  
  
> [!NOTE]  
>  Para los tipos de valores grandes, todos los parámetros de longitud se devolverán con un valor de SQL_SS_LENGTH_UNLIMITED.  
  
 **SQLColumns** se puede ejecutar en un cursor de servidor estático. Un intento de ejecutar **SQLColumns** en un cursor actualizable (dinámico o conjunto de claves) devolverá SQL_SUCCESS_WITH_INFO que indica que se ha cambiado el tipo de cursor.  
  
 El controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client permite notificar información de tablas en servidores vinculados aceptando un nombre de dos partes para el parámetro *CatalogName* : *Linked_Server_Name.Catalog_Name*.  
  
 Para ODBC 2. *x* aplicaciones que no utilizan comodines en *TableName*, **SQLColumns** devuelve información sobre las tablas cuyos nombres coinciden con *TableName* y son propiedad del usuario actual. Si el usuario actual no posee ninguna tabla cuyo nombre coincida con el parámetro *TableName,* **SQLColumns** devuelve información sobre las tablas propiedad de otros usuarios donde el nombre de tabla coincide con el parámetro *TableName.* Para ODBC 2. *x* aplicaciones que utilizan comodines, **SQLColumns** devuelve todas las tablas cuyos nombres coinciden con *TableName*. Para ODBC 3. *x* aplicaciones **SQLColumns** devuelve todas las tablas cuyos nombres coinciden con *TableName* independientemente del propietario o si se utilizan comodines.  
  
 La tabla siguiente muestra las columnas devueltas por el conjunto de resultados:  
  
|Nombre de la columna|Descripción|  
|-----------------|-----------------|  
|DATA_TYPE|Devuelve SQL_VARCHAR, SQL_VARBINARY o SQL_WVARCHAR para los tipos de datos **varchar(max).**|  
|TYPE_NAME|Devuelve "varchar", "varbinary" o "nvarchar" para los tipos de datos **varchar(max)**, **varbinary(max)** y **nvarchar(max).**|  
|COLUMN_SIZE|Devuelve SQL_SS_LENGTH_UNLIMITED para los tipos de datos **varchar(max)** que indican que el tamaño de la columna es ilimitado.|  
|BUFFER_LENGTH|Devuelve SQL_SS_LENGTH_UNLIMITED para los tipos de datos **varchar(max)** que indican que el tamaño del búfer es ilimitado.|  
|SQL_DATA_TYPE|Devuelve SQL_VARCHAR, SQL_VARBINARY o SQL_WVARCHAR para los tipos de datos **varchar(max).**|  
|CHAR_OCTET_LENGTH|Devuelve la longitud máxima de una columna de caracteres o binaria. Devuelve 0 para indicar que el tamaño es ilimitado.|  
|SS_XML_SCHEMACOLLECTION_CATALOG_NAME|Devuelve el nombre del catálogo donde se define un nombre de colección de esquemas XML. Si no se encuentra el nombre de catálogo, esta variable contiene una cadena vacía.|  
|SS_XML_SCHEMACOLLECTION_SCHEMA_NAME|Devuelve el nombre del esquema donde se define un nombre de colección de esquemas XML. Si no se encuentra el nombre de esquema, esta variable contiene una cadena vacía.|  
|SS_XML_SCHEMACOLLECTION_NAME|Devuelve el nombre de una colección de esquemas XML. Si no se encuentra el nombre, esta variable contiene una cadena vacía.|  
|SS_UDT_CATALOG_NAME|Nombre del catálogo que contiene el UDT (tipo definido por el usuario).|  
|SS_UDT_SCHEMA_NAME|Nombre del esquema que contiene el UDT.|  
|SS_UDT_ASSEMBLY_TYPE_NAME|Nombre completo de ensamblado del UDT.|  
  
 Para los UDT, la columna TYPE_NAME existente se utiliza para indicar el nombre del UDT; por lo tanto, no se debe agregar ninguna columna adicional para él al conjunto de resultados de **SQLColumns** o [SQLProcedureColumns](../../relational-databases/native-client-odbc-api/sqlprocedurecolumns.md). El DATA_TYPE de una columna o parámetro de UDT es SQL_SS_UDT.  
  
 Para el UDT de los parámetros, puede utilizar los nuevos descriptores específicos del controlador definidos anteriormente para obtener o establecer las propiedades de metadatos adicionales de un UDT, en caso de que el servidor devuelva o requiera esta información.  
  
 Cuando un cliente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se conecta a sqlColumns y llama a ellos, el uso de valores NULL o comodín para el parámetro de entrada de catálogo no devolverá información de otros catálogos. En su lugar, solo se devolverá información sobre el catálogo actual. El cliente puede llamar primero a SQLTables para determinar en qué catálogo se encuentra la tabla deseada. A continuación, el cliente puede usar ese valor de catálogo para el parámetro de entrada de catálogo en su llamada a SQLColumns para recuperar información sobre las columnas de esa tabla.  
  
## <a name="sqlcolumns-and-table-valued-parameters"></a>Parámetros de SQLColumns y con valores de tabla  
 El conjunto de resultados devuelto por SQLColumns depende de la configuración de SQL_SOPT_SS_NAME_SCOPE. Para obtener más información, vea [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md). Se han agregado las columnas siguientes para los parámetros con valores de tabla:  
  
|Nombre de la columna|Tipo de datos|Contenido|  
|-----------------|---------------|--------------|  
|SS_IS_COMPUTED|Smallint|Para una columna de TABLE_TYPE, este es SQL_TRUE si se trata de una columna calculada; de lo contrario, SQL_FALSE.|  
|SS_IS_IDENTITY|Smallint|SQL_TRUE si se trata de una columna de identidad; de lo contrario, SQL_FALSE.|  
  
 Para obtener más información acerca de los parámetros con valores de tabla, vea [Parámetros con valores ](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)de tabla &#40;&#41;ODBC .  
  
## <a name="sqlcolumns-support-for-enhanced-date-and-time-features"></a>Compatibilidad de SQLColumns con las características mejoradas de fecha y hora  
 Para obtener información sobre los valores devueltos para los tipos de fecha y hora, vea Metadatos de [catálogo](../../relational-databases/native-client-odbc-date-time/metadata-catalog.md).  
  
 Para obtener más información, vea Mejoras de [fecha y hora &#40;&#41;ODBC ](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqlcolumns-support-for-large-clr-udts"></a>Compatibilidad de SQLColumns con UDT CLR grandes  
 **SQLColumns** admite tipos definidos por el usuario (UDT) CLR grandes. Para obtener más información, vea [Tipos definidos por el usuario de CLR grandes &#40;&#41;ODBC ](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="sqlcolumns-support-for-sparse-columns"></a>Compatibilidad de SQLColumns con columnas dispersas  
 Se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] han agregado dos columnas específicas al conjunto de resultados para SQLColumns:  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|SS_IS_SPARSE|**Smallint**|Si la columna es una columna dispersa, tiene el valor SQL_TRUE; de lo contrario, SQL_FALSE.|  
|SS_IS_COLUMN_SET|**Smallint**|Si la columna es la columna **column_set,** se SQL_TRUE; de lo contrario, SQL_FALSE.|  
  
 De conformidad con la especificación ODBC, SS_IS_SPARSE y SS_IS_COLUMN_SET aparecen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] antes de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]todas las columnas específicas del controlador que se agregaron a versiones anteriores a , y después de todas las columnas exigidas por ODBC.  
  
 El conjunto de resultados devuelto por SQLColumns depende de la configuración de SQL_SOPT_SS_NAME_SCOPE. Para obtener más información, vea [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md).  
  
 Para obtener más información acerca de las columnas dispersas en ODBC, vea [Compatibilidad con columnas dispersas &#40;&#41;ODBC ](../../relational-databases/native-client/odbc/sparse-columns-support-odbc.md).  
  
## <a name="see-also"></a>Consulte también  
 [Función SQLColumns](https://go.microsoft.com/fwlink/?LinkId=59336)   
 [ODBC API Implementation Details](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
