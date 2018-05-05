---
title: Los miembros de SQLServerResultSetMetaData | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 37587981-2979-49a3-a6ab-df4bfb9b8748
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 03374d523c0dda429b7193404cefddbb9b5711ca
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sqlserverresultsetmetadata-members"></a>Miembros SQLServerResultSetMetaData
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Las siguientes tablas enumeran los miembros expuestos por el [SQLServerResultSetMetaData](../../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md) clase.  
  
## <a name="constructors"></a>Constructores  
 Ninguno.  
  
## <a name="fields"></a>Campos  
 Ninguno.  
  
## <a name="inherited-fields"></a>Campos heredados  
  
|Nombre|Description|  
|----------|-----------------|  
|java.sql.ResultSetMetaData|columnNoNulls, columnNullable, columnNullableUnknown|  
  
## <a name="methods"></a>Métodos  
  
|Nombre|Description|  
|----------|-----------------|  
|[getCatalogName](../../../connect/jdbc/reference/getcatalogname-method-sqlserverresultsetmetadata.md)|Obtiene el nombre de catálogo para la tabla que incluye la columna designada.|  
|[getColumnClassName](../../../connect/jdbc/reference/getcolumnclassname-method-sqlserverresultsetmetadata.md)|Devuelve el nombre completo de la clase Java cuyas instancias se generan si la [getObject](../../../connect/jdbc/reference/getobject-method-sqlserverresultset.md) método de la [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) clase se llama para recuperar un valor de la columna.|  
|[getColumnCount](../../../connect/jdbc/reference/getcolumncount-method-sqlserverresultsetmetadata.md)|Devuelve el número de columnas del conjunto de resultados.|  
|[getColumnDisplaySize](../../../connect/jdbc/reference/getcolumndisplaysize-method-sqlserverresultsetmetadata.md)|Devuelve el ancho máximo normal, en caracteres, de la columna designada.|  
|[getColumnLabel](../../../connect/jdbc/reference/getcolumnlabel-method-sqlserverresultsetmetadata.md)|Obtiene el título que se sugiere para su uso en las copias impresas y presentaciones de la columna designada.|  
|[getColumnName](../../../connect/jdbc/reference/getcolumnname-method-sqlserverresultsetmetadata.md)|Obtener el nombre de la columna designada.|  
|[getColumnType](../../../connect/jdbc/reference/getcolumntype-method-sqlserverresultsetmetadata.md)|Recupera el tipo SQL de la columna designada.|  
|[getColumnTypeName](../../../connect/jdbc/reference/getcolumntypename-method-sqlserverresultsetmetadata.md)|Recupera el nombre del tipo específico de base de datos de la columna designada.|  
|[getPrecision](../../../connect/jdbc/reference/getprecision-method-sqlserverresultsetmetadata.md)|Obtiene el número de dígitos decimales para la columna designada.|  
|[getScale](../../../connect/jdbc/reference/getscale-method-sqlserverresultsetmetadata.md)|Obtiene el número de dígitos que se encuentran a la derecha del separador decimal para la columna designada.|  
|[getSchemaName](../../../connect/jdbc/reference/getschemaname-method-sqlserverresultsetmetadata.md)|Obtiene el nombre del esquema de tabla para la columna designada.|  
|[getTableName](../../../connect/jdbc/reference/gettablename-method-sqlserverresultsetmetadata.md)|Obtiene el nombre de la tabla de la columna designada.|  
|[Disautoincrement](../../../connect/jdbc/reference/isautoincrement-method-sqlserverresultsetmetadata.md)|Indica si se asigna automáticamente un número a la columna designada, lo cual la convierte en de solo lectura.|  
|[IsCaseSensitive](../../../connect/jdbc/reference/iscasesensitive-method-sqlserverresultsetmetadata.md)|Indica si la columna distinguen mayúsculas de minúsculas.|  
|[isCurrency](../../../connect/jdbc/reference/iscurrency-method-sqlserverresultsetmetadata.md)|Indica si la columna designada es un valor de efectivo.|  
|[isDefinitelyWritable](../../../connect/jdbc/reference/isdefinitelywritable-method-sqlserverresultsetmetadata.md)|Indica si se realizará correctamente la operación de escritura en una columna designada.|  
|[IsNullable](../../../connect/jdbc/reference/isnullable-method-sqlserverresultsetmetadata.md)|Indica la nulabilidad de los valores en la columna designada.|  
|[IsReadOnly](../../../connect/jdbc/reference/isreadonly-method-sqlserverresultsetmetadata.md)|Indica si definitivamente no se puede escribir en la columna.|  
|[isSearchable](../../../connect/jdbc/reference/issearchable-method-sqlserverresultsetmetadata.md)|Indica si la columna designada se puede utilizar en una cláusula WHERE de SQL.|  
|[isSigned](../../../connect/jdbc/reference/issigned-method-sqlserverresultsetmetadata.md)|Indica si los valores en la columna designada son números con signo.|  
|[isSparseColumnSet](../../../connect/jdbc/reference/issparsecolumnset-method-sqlserverresultsetmetadata.md)|Indica si una columna de un conjunto de resultados es un conjunto de columnas dispersas.|  
|[isWritable](../../../connect/jdbc/reference/iswritable-method-sqlserverresultsetmetadata.md)|Indica si es posible que se realice correctamente una operación de escritura en la columna designada.|  
  
## <a name="inherited-methods"></a>Métodos heredados  
  
|Clase heredada de:|Métodos|  
|---------------------------|-------------|  
|java.lang.Object|clone, equals, finalize, getClass, hashCode, notify, notifyAll, toString, wait|  
|java.sql.Wrapper|isWrapperFor, unwrap|  
  
## <a name="see-also"></a>Vea también  
 [Clase SQLServerResultSetMetaData](../../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md)  
  
  
