---
title: SQLProcedureColumns | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLProcedureColumns function
ms.assetid: 6671e180-0072-4de5-90f5-314306d2ba9c
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 96c68eac12677109975fce5beea04eec071e70b1
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85787981"
---
# <a name="sqlprocedurecolumns"></a>SQLProcedureColumns
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asdw-pdw.md)]

  **SQLProcedureColumns** devuelve una fila que notifica los atributos del valor devuelto de todos los procedimientos almacenados de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **SQLProcedureColumns** devuelve SQL_SUCCESS tanto si existen valores o no de los parámetros *CatalogName*, *SchemaName*, *ColumnName*o *ProcName* . **SQLFetch** devuelve SQL_NO_DATA si se usan valores no válidos en estos parámetros.  
  
 **SQLProcedureColumns** se puede ejecutar en un cursor de servidor estático. Un intento de ejecutar **SQLProcedureColumns** en un cursor actualizable (dinámico o controlado por conjunto de claves) devolverá SQL_SUCCESS_WITH_INFO, lo que indica que se ha cambiado el tipo de cursor.  
  
 En la tabla siguiente se muestran las columnas devueltas por el conjunto de resultados y cómo se han extendido para administrar los tipos de datos **xml** y **udt** a través del controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client:  
  
|Nombre de columna|Descripción|  
|-----------------|-----------------|  
|SS_UDT_CATALOG_NAME|Devuelve el nombre del catálogo que contiene el UDT (tipo definido por el usuario).|  
|SS_UDT_SCHEMA_NAME|Devuelve el nombre del esquema que contiene el UDT.|  
|SS_UDT_ASSEMBLY_TYPE_NAME|Devuelve el nombre completo de ensamblado del UDT.|  
|SS_XML_SCHEMACOLLECTION_CATALOG_NAME|Devuelve el nombre del catálogo donde se define un nombre de colección de esquemas XML. Si no se encuentra el nombre de catálogo, esta variable contiene una cadena vacía.|  
|SS_XML_SCHEMACOLLECTION_SCHEMA_NAME|Devuelve el nombre del esquema donde se define un nombre de colección de esquemas XML. Si no se encuentra el nombre de esquema, esta variable contiene una cadena vacía.|  
|SS_XML_SCHEMACOLLECTION_NAME|Devuelve el nombre de una colección de esquemas XML. Si no se encuentra el nombre, esta variable contiene una cadena vacía.|  
  
## <a name="sqlprocedurecolumns-and-table-valued-parameters"></a>SQLProcedureColumns y los parámetros con valores de tabla  
 SQLProcedureColumns controla los parámetros con valores de tabla de manera similar a los tipos definidos por el usuario CLR. En las filas devueltas para los parámetros con valores de tabla, las columnas tienen los valores siguientes:  
  
|Nombre de columna|Descripción/valor|  
|-----------------|------------------------|  
|DATA_TYPE|SQL_SS_TABLE|  
|TYPE_NAME|El nombre del tipo de tabla para el parámetro con valores de tabla.|  
|COLUMN_SIZE|NULL|  
|BUFFER_LENGTH|0|  
|DECIMAL_DIGITS|El número de columnas del parámetro con valores de tabla.|  
|NUM_PREC_RADIX|NULL|  
|NULLABLE|SQL_NULLABLE|  
|COMENTARIOS|NULL|  
|COLUMN_DEF|NULL. Los tipos de tabla puede que no tengan valores predeterminados.|  
|SQL_DATA_TYPE|SQL_SS_TABLE|  
|SQL_DATEIME_SUB|NULL|  
|CHAR_OCTET_LENGTH|NULL|  
|IS_NULLABLE|"YES"|  
|SS_TYPE_CATALOG_NAME|Devuelve el nombre del catálogo que contiene la tabla o el tipo definido por el usuario CLR.|  
|SS_TYPE_SCHEMA_NAME|Devuelve el nombre del esquema que contiene la tabla o el tipo definido por el usuario CLR.|  
  
 Las columnas SS_TYPE_CATALOG_NAME y SS_TYPE_SCHEMA_NAME están disponibles en [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] y versiones posteriores para devolver el catálogo y el esquema, respectivamente, de los parámetros con valores de tabla. Estas columnas se rellenan para los parámetros con valores de tabla y también para los parámetros de tipos definidos por el usuario CLR. (Esta función adicional no afecta al esquema ni a las columnas de catálogo existentes para los parámetros de tipos definidos por el usuario CLR. También se rellenan para mantener la compatibilidad con versiones anteriores).  
  
 De acuerdo con la especificación de ODBC, SS_TYPE_CATALOG_NAME y SS_TYPE_SCHEMA_NAME aparecen antes de todas las columnas específicas del controlador agregadas en versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]y después de todas las columnas asignadas por el propio ODBC.  
  
 Para obtener más información sobre los parámetros con valores de tabla, vea [parámetros con valores de tabla &#40;ODBC&#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="sqlprocedurecolumns-support-for-enhanced-date-and-time-features"></a>SQLProcedureColumns admite las características mejoradas de fecha y hora  
 Para obtener los valores devueltos para los tipos de fecha y hora, vea [Catalog Metadata](../../relational-databases/native-client-odbc-date-time/metadata-catalog.md).  
  
 Para obtener más información general, consulte [mejoras de fecha y hora &#40;ODBC&#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqlprocedurecolumns-support-for-large-clr-udts"></a>SQLProcedureColumns admite UDT CLR grandes  
 **SQLProcedureColumns** admite tipos definidos por el usuario (UDT) CLR grandes. Para obtener más información, vea [tipos CLR grandes definidos por el usuario &#40;ODBC&#41;](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="see-also"></a>Consulte también  
 [SQLProcedureColumns función)](https://go.microsoft.com/fwlink/?LinkId=59363)   
 [ODBC API Implementation Details](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
