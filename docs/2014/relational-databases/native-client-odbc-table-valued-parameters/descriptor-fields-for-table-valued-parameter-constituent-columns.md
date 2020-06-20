---
title: Campos de descriptor para columnas de componentes de parámetros con valores de tabla | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC), descriptor fields for constituent columns
ms.assetid: 944b3968-fd47-4847-98d6-b87e8ef2acdc
author: rothja
ms.author: jroth
ms.openlocfilehash: 3e4c45cf608c78715abd7c5075d4cd7fb2e162a5
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85018385"
---
# <a name="descriptor-fields-for-table-valued-parameter-constituent-columns"></a>Campos de descriptor para columnas de parámetros con valores de tabla
  Los campos de descriptor de parámetros con valores de tabla descritos en esta sección se manipulan mediante [SQLSetDescField](../native-client-odbc-api/sqlsetdescfield.md) y [SQLSetDescField](../native-client-odbc-api/sqlsetdescfield.md) con el identificador del descriptor de parámetros de implementación (IPD).  
  
## <a name="remarks"></a>Comentarios  
 SQL_DESC_AUTO_UNIQUE_VALUE se usa para los parámetros con valores de tabla así como otras características.  
  
|Nombre del atributo|Tipo|Description|  
|--------------------|----------|-----------------|  
|SQL_DESC_AUTO_UNIQUE_VALUE|SQLINTEGER|SQL_TRUE indica que esta columna es una columna de identidad.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]puede usar esta información para optimizar el rendimiento, pero no es necesario que las aplicaciones lo establezcan para las columnas de identidad.|  
  
 Los atributos siguientes se agregan a todos los tipos de parámetro en los campos descriptor de parámetros de la aplicación (APD) y descriptor de parámetro de implementación (IPD):  
  
|Nombre del atributo|Tipo|Description|  
|--------------------|----------|-----------------|  
|SQL_CA_SS_COLUMN_COMPUTED|SQLSMALLINT|SQL_TRUE indica que esta columna está calculada.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]puede usar esta información para optimizar el rendimiento, pero no es necesario que las aplicaciones lo establezcan para las columnas calculadas.<br /><br /> Este atributo se pasa por alto en los enlaces que no son columnas de parámetro con valores de tabla.|  
|SQL_CA_SS_COLUMN_IN_UNIQUE_KEY|SQLSMALLINT|SQL_TRUE indica que una columna de parámetro con valores de tabla participa en una clave única. Esto puede dar lugar a un mejor rendimiento de la consulta. Este atributo se pasa por alto en los enlaces que no son columnas de parámetro con valores de tabla.|  
|SQL_CA_SS_COLUMN_SORT_ORDER|SQLSMALLINT|Indica el criterio de ordenación de una columna de parámetro con valores de tabla. Esto puede dar lugar a un mejor rendimiento de la consulta. Este atributo se pasa por alto en los enlaces que no son columnas de parámetro con valores de tabla. Los valores posibles son los siguientes:<br /><br /> -SQL_SS_ASCENDING_ORDER<br />-SQL_SS_DESCENDING_ORDER<br />-SQL_SS_ORDER_UNSPECIFIED<br /><br /> Los valores distintos de SQL_SS_ASCENDING_ORDER y SQL_SS_DESCENDING_ORDER generan un error con SQLSTATE HY024 y el mensaje 'Valor de atributo no válido', y se tratan como SQL_SS_ORDER_UNSPECIFIED, que es el valor predeterminado para este atributo.|  
|SQL_CA_SS_COLUMN_SORT_ORDINAL|SQLSMALLINT|Indica el ordinal de una columna de parámetro con valores de tabla en el conjunto de columnas que definen la clasificación total para un parámetro con valores de tabla. Esto puede dar lugar a un mejor rendimiento de la consulta. Este atributo se pasa por alto en los enlaces que no son columnas de parámetro con valores de tabla. La ordenación de los ordinales se inicia en 1. Un valor de 0, el valor predeterminado, indica que una columna de parámetro con valores de tabla no tiene ordenación de columnas.|  
|SQL_CA_SS_COLUMN_HAS_DEFAULT_VALUE|SQLSMALLINT|Indica si todas las filas en el parámetro con valores de tabla tendrán el valor predeterminado para esta columna. Para los parámetros con valores de tabla, no es posible seleccionar el valor predeterminado fila a fila. Un valor de SQL_FALSE indica que las filas tendrán valores no predeterminados. Este es el valor predeterminado. Un valor de SQL_TRUE indica que esta columna tendrá los valores predeterminados para todas las filas.<br /><br /> Si está establecido en SQL_TRUE, no se enviará al servidor ningún dato.<br /><br /> Este campo también se puede usar con columnas de identidad o calculadas si los valores de columna no son necesarios en el procesamiento del servidor.|  
  
 Estos atributos únicamente son válidos en columnas de parámetro con valores de tabla. Se pasan por alto para otros parámetros.  
  
 Si SQL_CA_SS_COL_HAS_DEFAULT_VALUE está establecido para una columna de parámetro con valores de tabla, SQL_DESC_DATA_PTR para esa columna debe ser un puntero NULL. De lo contrario, SQLExecute o SQLExecDirect devolverán SQL_ERROR. Se generará un registro de diagnóstico con SQLSTATE = 07S01 y el mensaje "uso no válido de parámetro predeterminado para \<p> el parámetro, columna \<c> ", donde \<p> es el ordinal del parámetro y \<c> es el ordinal de la columna.  
  
## <a name="see-also"></a>Consulte también  
 [Parámetros con valores de tabla &#40;ODBC&#41;](table-valued-parameters-odbc.md)  
  
  
