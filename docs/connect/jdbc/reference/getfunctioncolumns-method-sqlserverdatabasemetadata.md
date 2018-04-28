---
title: Método getFunctionColumns (SQLServerDatabaseMetaData) | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: e2b0e0f7-717c-48e6-bcd2-a325d938a833
caps.latest.revision: 27
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8e9e3d78c17b4c2fe44ce80b6baf0eb8e4294339
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="getfunctioncolumns-method-sqlserverdatabasemetadata"></a>Método getFunctionColumns (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera una descripción de los parámetros de las funciones del sistema o de usuario del catálogo y del tipo de devolución.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public ResultSet getFunctionColumns(java.lang.String catalog,  
                       java.lang.String schemaPattern,  
                       java.lang.String functionNamePattern  
                       java.lang.String columnNamePattern)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *catalog*  
  
 A **cadena** que contiene el nombre del catálogo. Si es una cadena vacía "", el resultado incluye las funciones sin un catálogo. Si es **null**, el nombre del catálogo no se utiliza para la búsqueda.  
  
 *schemaPattern*  
  
 A **cadena** que contiene el patrón de nombre de esquema. Si es una cadena vacía "", el resultado incluye las funciones sin un esquema. Si es **null**, el nombre del esquema no se utiliza para la búsqueda.  
  
 *functionNamePattern*  
  
 A **cadena** que contiene el nombre de una función.  
  
 *columnNamePattern*  
  
 A **cadena** que contiene el nombre de un parámetro.  
  
## <a name="return-value"></a>Valor devuelto  
 A [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método getFunctionColumns especificado por el método getFunctionColumns en la interfaz java.sql.DatabaseMetaData.  
  
 Este método devuelve solamente las funciones y parámetros que coinciden con el esquema, nombre de función y nombre de parámetro especificados dentro del catálogo indicado.  
  
 Cada fila en el conjunto de resultados incluye las siguientes columnas para una descripción del parámetro, una descripción de la columna o un tipo de devolución:  
  
|Nombre|Tipo|Description|  
|----------|----------|-----------------|  
|FUNCTION_CAT|**String**|Nombre de la base de datos en que reside la función.|  
|FUNCTION_SCHEM|**String**|Esquema para la función.|  
|FUNCTION_NAME|**String**|Nombre de la función.|  
|COLUMN_NAME|**String**|Nombre de un parámetro o columna.|  
|COLUMN_TYPE|**Corto**|**El tipo de la columna. Puede ser uno de los siguientes valores:**<br /><br /> functionColumnUnknown (0): tipo desconocido.<br /><br /> functionColumnIn (1): parámetro de entrada.<br /><br /> functionColumnInOut (2): parámetro de entrada y salida.<br /><br /> functionColumnOut (3): parámetro de salida.<br /><br /> functionReturn (4): valor devuelto de una función.<br /><br /> functionColumnResult (5): un parámetro o columna es una columna en el conjunto de resultados.|  
|DATA_TYPE|**smallint**|Valor de Java.sql.Types del tipo de datos SQL.|  
|TYPE_NAME|**String**|El nombre del tipo de datos.|  
|PRECISION|**int**|Número total de dígitos significativos.|  
|LENGTH|**int**|La longitud de los datos en bytes.|  
|SCALE|**Corto**|El número de dígitos a la derecha del separador decimal.|  
|RADIX|**Corto**|Base de tipos numéricos.|  
|NULLABLE|**Corto**|Indica si el valor devuelto o parámetro puede contener una **null** valor.<br /><br /> **Puede ser uno de los siguientes valores:**<br /><br /> functionNoNulls (0): no se permite un valor NULL.<br /><br /> functionNullable (1): se permite un valor NULL.<br /><br /> functionNullableUnknown (2): desconocido.|  
|REMARKS|**String**|Comentarios sobre una columna o un parámetro.|  
|COLUMN_DEF|**String**|El valor predeterminado de la columna.<br /><br /> **Nota:** esta información está disponible con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] y es específica del controlador JDBC.|  
|SQL_DATA_TYPE|**smallint**|Esta columna es el mismo que el **DATA_TYPE** columna, excepto para la **datetime** e ISO **intervalo** tipos de datos.<br /><br /> **Nota:** esta información está disponible con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] y es específica del controlador JDBC.|  
|SQL_DATETIME_SUB|**smallint**|El **datetime** ISO **intervalo** subcódigo si el valor de **SQL_DATA_TYPE** es **SQL_DATETIME** o **SQL_INTERVAL**. Para tipos de datos distinto de **datetime** e ISO **intervalo**, esta columna es NULL.<br /><br /> **Nota:** esta información está disponible con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] y es específica del controlador JDBC.|  
|CHAR_OCTET_LENGTH|**int**|Longitud máxima de los parámetros o columnas basados en valores binarios o caracteres. Para los demás tipos de datos, es NULL.|  
|ORDINAL_POSITION|**int**|Para los parámetros de entrada y salida, representa la posición a partir de 1.<br /><br /> Para las columnas de conjunto de resultados, es la posición de la columna en el conjunto de resultados a partir de 1.<br /><br /> Para el valor devuelto, es 0.|  
|IS_NULLABLE|**String**|Determina la nulabilidad de un parámetro o columna.<br /><br /> Puede ser uno de los siguientes valores:<br /><br /> **Sí**: el parámetro o una columna puede incluir valores NULL.<br /><br /> **Ya NO**: el parámetro o una columna no puede incluir los valores NULL.<br /><br /> Cadena vacía (""): desconocido.|  
|SS_TYPE_CATALOG_NAME|**String**|Nombre del catálogo que contiene el tipo definido por el usuario (UDT).|  
|SS_TYPE_SCHEMA_NAME|**String**|Nombre del esquema que contiene el tipo definido por el usuario (UDT).|  
|SS_UDT_CATALOG_NAME|**String**|Tipo definido por el usuario (UDT) del nombre completo.|  
|SS_UDT_SCHEMA_NAME|**String**|Nombre del catálogo donde se define el nombre de una colección de esquemas XML. Si no se encuentra el nombre del catálogo, esta variable contiene una cadena vacía.|  
|SS_UDT_ASSEMBLY_TYPE_NAME|**String**|Nombre del esquema donde se define el nombre de una colección de esquemas XML. Si no se puede encontrar el nombre de esquema, esta cadena estará vacía.|  
|SS_XML_SCHEMACOLLECTION_CATALOG_NAME|**String**|Nombre de una colección de esquemas XML. Si no se puede encontrar el nombre, esta cadena estará vacía.|  
|SS_XML_SCHEMACOLLECTION_SCHEMA_NAME|**String**|Nombre del catálogo que contiene el tipo definido por el usuario (UDT).|  
|SS_XML_SCHEMACOLLECTION_NAME|**String**|Nombre del esquema que contiene el tipo definido por el usuario (UDT).|  
|SS_DATA_TYPE|**tinyint**|El [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] tipo de datos que utiliza los procedimientos almacenados extendidos.<br /><br /> **Tenga en cuenta** para obtener más información acerca de los tipos de datos devueltos por [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)], vea "Tipos de datos (Transact-SQL)" en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] libros en pantalla.|  
  
## <a name="see-also"></a>Vea también  
 [Miembros de SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Clase SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
