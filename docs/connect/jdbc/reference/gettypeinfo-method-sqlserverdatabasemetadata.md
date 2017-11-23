---
title: "Método getTypeInfo (SQLServerDatabaseMetaData) | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLServerDatabaseMetaData.getTypeInfo
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: 23208f01-c1bf-4235-b29c-9051d3df59a3
caps.latest.revision: "21"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2424ec8f3b484272d2311ac7880cc8810561bd2e
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="gettypeinfo-method-sqlserverdatabasemetadata"></a>Método getTypeInfo (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera una descripción de todos los tipos SQL estándar que se admiten en la base de datos actual.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.sql.ResultSet getTypeInfo()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 A [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método getTypeInfo es especificado por el método getTypeInfo en la interfaz java.sql.DatabaseMetaData.  
  
 El conjunto de resultados devuelto por el método getTypeInfo contendrá la siguiente información:  
  
|Nombre|Tipo|Description|  
|----------|----------|-----------------|  
|TYPE_NAME|**String**|El nombre del tipo de datos.|  
|DATA_TYPE|**corto**|Tipo de datos SQL de java.sql.Types.|  
|PRECISION|**int**|Número total de dígitos significativos.|  
|LITERAL_PREFIX|**String**|El carácter o caracteres utilizados antes de una constante.|  
|LITERAL_SUFFIX|**String**|Carácter o caracteres utilizados para terminar una constante.|  
|CREATE_PARAMS|**String**|Descripción de los parámetros de creación para el tipo de datos.|  
|NULLABLE|**corto**|Indica si la columna puede contener un valor NULL. Puede ser uno de los siguientes valores:<br /><br /> typeNoNulls (0)<br /><br /> typeNullable (1)<br /><br /> typeNullableUnknown (2)|  
|CASE_SENSITIVE|**boolean**|Indica si el tipo de datos distingue mayúsculas de minúsculas. "**true**"si el tipo es entre mayúsculas y minúsculas; en caso contrario,"**false**".|  
|SEARCHABLE|**corto**|Indica si la columna se puede utilizar en una cláusula WHERE de SQL. Puede ser uno de los siguientes valores:<br /><br /> typePredNone (0)<br /><br /> typePredChar (1)<br /><br /> typePredBasic (2)<br /><br /> typeSeachable (3)|  
|UNSIGNED_ATTRIBUTE|**boolean**|Indica el signo del tipo de datos. "**true**"si el tipo es sin signo; de lo contrario,"**false**".|  
|FIXED_PREC_SCALE|**boolean**|Indica que el tipo de datos puede ser un valor de moneda. "**true**" si el tipo de datos es de tipo moneda; en caso contrario, "**false**".|  
|AUTO_INCREMENT|**boolean**|Indica que el tipo de datos se puede incrementarse automáticamente. "**true**"si el tipo puede incrementar automáticamente; en caso contrario,"**false**".|  
|LOCAL_TYPE_NAME|**String**|Nombre localizado del tipo de datos.|  
|MINIMUM_SCALE|**corto**|Número máximo de dígitos a la derecha del signo decimal.|  
|MAXIMUM_SCALE|**corto**|Número mínimo de dígitos a la derecha del signo decimal.|  
|SQL_DATA_TYPE|**int**|El controlador JDBC no lo admite.|  
|SQL_DATETIME_SUB|**int**|El controlador JDBC no lo admite.|  
|NUM_PREC_RADIX|**int**|El número de bits o dígitos para calcular el número máximo que puede tener una columna.|  
|INTERVAL_PRECISION|**smallint**|Valor de la precisión del principio del intervalo.|  
|USERTYPE|**smallint**|El **usertype** valor de la **systypes** tabla. Para obtener más información, vea los Libros en pantalla de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)].|  
  
> [!NOTE]  
>  Para obtener más información acerca de los datos devueltos por el método getTypeInfo, vea "sp_datatype_info (Transact-SQL)" en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] libros en pantalla.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se muestra cómo utilizar el método getTypeInfo para devolver información acerca de los tipos de datos utilizados en un [!INCLUDE[ssVersion2005](../../../includes/ssversion2005_md.md)] (o posterior) base de datos.  
  
```  
public static void executeGetTypeInfo(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getTypeInfo();  
      ResultSetMetaData rsmd = rs.getMetaData();  
  
      // Display the result set data.  
      int cols = rsmd.getColumnCount();  
      while(rs.next()) {  
         for (int i = 1; i <= cols; i++) {  
            System.out.println(rs.getString(i));  
         }  
      }  
      rs.close();  
   }   
  
   catch (Exception e) {  
      e.printStackTrace();  
   }  
}  
```  
  
## <a name="see-also"></a>Vea también  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Miembros de SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Clase SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
