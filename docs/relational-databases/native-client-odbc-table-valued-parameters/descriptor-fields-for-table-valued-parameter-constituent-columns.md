---
title: Campos de descriptor para columnas de parámetros con valores de tabla | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC), descriptor fields for constituent columns
ms.assetid: 944b3968-fd47-4847-98d6-b87e8ef2acdc
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: b6be7a245b15061b5186f15ad070d0fc91924383
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37429554"
---
# <a name="descriptor-fields-for-table-valued-parameter-constituent-columns"></a>Campos de descriptor para columnas de parámetros con valores de tabla
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Los campos de descriptor de parámetro con valores de tabla se describe en esta sección se manipulan mediante [SQLSetDescField](../../relational-databases/native-client-odbc-api/sqlsetdescfield.md) y [SQLSetDescField](../../relational-databases/native-client-odbc-api/sqlsetdescfield.md) con el identificador para el descriptor de parámetro de implementación () IPD).  
  
## <a name="remarks"></a>Notas  
 SQL_DESC_AUTO_UNIQUE_VALUE se usa para los parámetros con valores de tabla así como otras características.  
  
|Nombre del atributo|Tipo|Descripción|  
|--------------------|----------|-----------------|  
|SQL_DESC_AUTO_UNIQUE_VALUE|SQLINTEGER|SQL_TRUE indica que esta columna es una columna de identidad.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Puede usar esta información para optimizar el rendimiento, pero no tienen las aplicaciones lo establezcan para las columnas de identidad.|  
  
 Los atributos siguientes se agregan a todos los tipos de parámetro en los campos descriptor de parámetros de la aplicación (APD) y descriptor de parámetro de implementación (IPD):  
  
|Nombre del atributo|Tipo|Descripción|  
|--------------------|----------|-----------------|  
|SQL_CA_SS_COLUMN_COMPUTED|SQLSMALLINT|SQL_TRUE indica que esta columna está calculada.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Puede usar esta información para optimizar el rendimiento, pero no tienen las aplicaciones lo establezcan para las columnas calculadas.<br /><br /> Este atributo se pasa por alto en los enlaces que no son columnas de parámetro con valores de tabla.|  
|SQL_CA_SS_COLUMN_IN_UNIQUE_KEY|SQLSMALLINT|SQL_TRUE indica que una columna de parámetro con valores de tabla participa en una clave única. Esto puede dar lugar a un mejor rendimiento de la consulta. Este atributo se pasa por alto en los enlaces que no son columnas de parámetro con valores de tabla.|  
|SQL_CA_SS_COLUMN_SORT_ORDER|SQLSMALLINT|Indica el criterio de ordenación de una columna de parámetro con valores de tabla. Esto puede dar lugar a un mejor rendimiento de la consulta. Este atributo se pasa por alto en los enlaces que no son columnas de parámetro con valores de tabla. Los valores posibles son los siguientes: <br />**SQL_SS_ASCENDING_ORDER**<br />**SQL_SS_DESCENDING_ORDER**<br />**SQL_SS_ORDER_UNSPECIFIED**<br /><br /> Los valores distintos de **SQL_SS_ASCENDING_ORDER** y **SQL_SS_DESCENDING_ORDER** generan un error con **SQLSTATE HY024** y mensaje 'valor de atributo no válido' y tratar como **SQL_SS_ORDER_UNSPECIFIED**, que es el valor predeterminado para este atributo.|  
|SQL_CA_SS_COLUMN_SORT_ORDINAL|SQLSMALLINT|Indica el ordinal de una columna de parámetro con valores de tabla en el conjunto de columnas que definen la clasificación total para un parámetro con valores de tabla. Esto puede dar lugar a un mejor rendimiento de la consulta. Este atributo se pasa por alto en los enlaces que no son columnas de parámetro con valores de tabla. La ordenación de los ordinales se inicia en 1. Un valor de 0, el valor predeterminado, indica que una columna de parámetro con valores de tabla no tiene ordenación de columnas.|  
|SQL_CA_SS_COLUMN_HAS_DEFAULT_VALUE|SQLSMALLINT|Indica si todas las filas en el parámetro con valores de tabla tendrán el valor predeterminado para esta columna. Para los parámetros con valores de tabla, no es posible seleccionar el valor predeterminado fila a fila. Un valor de SQL_FALSE indica que las filas tendrán valores no predeterminados. Ésta es la opción predeterminada. Un valor de SQL_TRUE indica que esta columna tendrá los valores predeterminados para todas las filas.<br /><br /> Si está establecido en SQL_TRUE, no se enviará al servidor ningún dato.<br /><br /> Este campo también se puede usar con columnas de identidad o calculadas si los valores de columna no son necesarios en el procesamiento del servidor.|  
  
 Estos atributos únicamente son válidos en columnas de parámetro con valores de tabla. Se pasan por alto para otros parámetros.  
  
 Si SQL_CA_SS_COL_HAS_DEFAULT_VALUE está establecido para una columna de parámetro con valores de tabla, SQL_DESC_DATA_PTR para esa columna debe ser un puntero NULL. En caso contrario, SQLExecute o SQLExecDirect devolverá SQL_ERROR. Se generará un registro de diagnóstico con SQLSTATE = 07S01 y el mensaje "uso no válido de parámetro predeterminado para el parámetro \<p >, columna \<c >", donde \<p > es el parámetro ordinal y \<c > es el ordinal de columna.  
  
## <a name="see-also"></a>Vea también  
 [Parámetros con valores de tabla &#40;ODBC&#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
  
