---
title: "Campos de descriptor para columnas constituyentes del parámetro con valores de tabla | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-table-valued-parameters
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords: table-valued parameters (ODBC), descriptor fields for constituent columns
ms.assetid: 944b3968-fd47-4847-98d6-b87e8ef2acdc
caps.latest.revision: "24"
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e0001cdd0d2295196aa565876f8a380142ad2552
ms.sourcegitcommit: a0aa5e611a0e6ebb74ac1e2f613e8916dc7a7617
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/24/2018
---
# <a name="descriptor-fields-for-table-valued-parameter-constituent-columns"></a>Campos de descriptor para columnas de parámetros con valores de tabla
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Los campos de descriptor de parámetro con valores de tabla se describe en esta sección se manipulan mediante [SQLSetDescField](../../relational-databases/native-client-odbc-api/sqlsetdescfield.md) y [SQLSetDescField](../../relational-databases/native-client-odbc-api/sqlsetdescfield.md) con el identificador para el descriptor de parámetro de implementación () IPD).  
  
## <a name="remarks"></a>Comentarios  
 SQL_DESC_AUTO_UNIQUE_VALUE se usa para los parámetros con valores de tabla así como otras características.  
  
|Nombre del atributo|Tipo|Description|  
|--------------------|----------|-----------------|  
|SQL_DESC_AUTO_UNIQUE_VALUE|SQLINTEGER|SQL_TRUE indica que esta columna es una columna de identidad.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Puede utilizar esta información para optimizar el rendimiento, pero no se requiere que las aplicaciones lo establezcan para las columnas de identidad.|  
  
 Los atributos siguientes se agregan a todos los tipos de parámetro en los campos descriptor de parámetros de la aplicación (APD) y descriptor de parámetro de implementación (IPD):  
  
|Nombre del atributo|Tipo|Description|  
|--------------------|----------|-----------------|  
|SQL_CA_SS_COLUMN_COMPUTED|SQLSMALLINT|SQL_TRUE indica que esta columna está calculada.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Puede utilizar esta información para optimizar el rendimiento, pero no se requiere que las aplicaciones lo establezcan para las columnas calculadas.<br /><br /> Este atributo se pasa por alto en los enlaces que no son columnas de parámetro con valores de tabla.|  
|SQL_CA_SS_COLUMN_IN_UNIQUE_KEY|SQLSMALLINT|SQL_TRUE indica que una columna de parámetro con valores de tabla participa en una clave única. Esto puede dar lugar a un mejor rendimiento de la consulta. Este atributo se pasa por alto en los enlaces que no son columnas de parámetro con valores de tabla.|  
|SQL_CA_SS_COLUMN_SORT_ORDER|SQLSMALLINT|Indica el criterio de ordenación de una columna de parámetro con valores de tabla. Esto puede dar lugar a un mejor rendimiento de la consulta. Este atributo se pasa por alto en los enlaces que no son columnas de parámetro con valores de tabla. Los valores posibles son los siguientes: <br />**SQL_SS_ASCENDING_ORDER**<br />**SQL_SS_DESCENDING_ORDER**<br />**SQL_SS_ORDER_UNSPECIFIED**<br /><br /> Valores distintos de **SQL_SS_ASCENDING_ORDER** y **SQL_SS_DESCENDING_ORDER** generará un error con **SQLSTATE HY024** y el mensaje 'valor de atributo no válido' y son tratar como **SQL_SS_ORDER_UNSPECIFIED**, que es el valor predeterminado para este atributo.|  
|SQL_CA_SS_COLUMN_SORT_ORDINAL|SQLSMALLINT|Indica el ordinal de una columna de parámetro con valores de tabla en el conjunto de columnas que definen la clasificación total para un parámetro con valores de tabla. Esto puede dar lugar a un mejor rendimiento de la consulta. Este atributo se pasa por alto en los enlaces que no son columnas de parámetro con valores de tabla. La ordenación de los ordinales se inicia en 1. Un valor de 0, el valor predeterminado, indica que una columna de parámetro con valores de tabla no tiene ordenación de columnas.|  
|SQL_CA_SS_COLUMN_HAS_DEFAULT_VALUE|SQLSMALLINT|Indica si todas las filas en el parámetro con valores de tabla tendrán el valor predeterminado para esta columna. Para los parámetros con valores de tabla, no es posible seleccionar el valor predeterminado fila a fila. Un valor de SQL_FALSE indica que las filas tendrán valores no predeterminados. Ésta es la opción predeterminada. Un valor de SQL_TRUE indica que esta columna tendrá los valores predeterminados para todas las filas.<br /><br /> Si está establecido en SQL_TRUE, no se enviará al servidor ningún dato.<br /><br /> Este campo también se puede usar con columnas de identidad o calculadas si los valores de columna no son necesarios en el procesamiento del servidor.|  
  
 Estos atributos únicamente son válidos en columnas de parámetro con valores de tabla. Se pasan por alto para otros parámetros.  
  
 Si SQL_CA_SS_COL_HAS_DEFAULT_VALUE está establecido para una columna de parámetro con valores de tabla, SQL_DESC_DATA_PTR para esa columna debe ser un puntero NULL. En caso contrario, SQLExecute o SQLExecDirect devolverá SQL_ERROR. Se generará un registro de diagnóstico con SQLSTATE = 07S01 y el mensaje "uso no válido de parámetro predeterminado para el parámetro \<p >, columna \<c >", donde \<p > es el parámetro ordinal y \<c > es el ordinal de columna.  
  
## <a name="see-also"></a>Vea también  
 [Con valores de tabla parámetros &#40; ODBC &#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
  
