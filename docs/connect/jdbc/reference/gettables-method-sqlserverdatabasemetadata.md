---
title: "Método getTables (SQLServerDatabaseMetaData) | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerDatabaseMetaData.getTables
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: a7514673-3457-4541-9560-28a8284ad9e3
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9bbf35aeec7b5626b380fc654995d181fe124811
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="gettables-method-sqlserverdatabasemetadata"></a>Método getTables (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera una descripción de las tablas que están disponibles en el patrón de nombre determinado de catálogo, esquema o tabla.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.sql.ResultSet getTables(java.lang.String catalog,  
                                    java.lang.String schema,  
                                    java.lang.String table,  
                                    java.lang.String[] types)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *catálogo*  
  
 A **cadena** que contiene el nombre del catálogo. Si se proporciona un valor NULL en este parámetro, indicará que no es necesario utilizar el nombre de catálogo.  
  
 *esquema*  
  
 A **cadena** que contiene el patrón de nombre de esquema. Si se proporciona un valor NULL en este parámetro, indicará que no es necesario utilizar el nombre de esquema.  
  
 *nombre de tabla*  
  
 A **cadena** que contiene el patrón de nombre de tabla.  
  
 *tipos de*  
  
 Una matriz de cadenas que contiene los tipos de tablas que se van a incluir. El valor NULL indica que todos los tipos de tablas deberían estar incluidos.  
  
## <a name="return-value"></a>Valor devuelto  
 A [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método getTables es especificado por el método getTables en la interfaz java.sql.DatabaseMetaData.  
  
 El conjunto de resultados devuelto por el método getTables contendrá la siguiente información:  
  
|Nombre|Tipo|Description|  
|----------|----------|-----------------|  
|TABLE_CAT|**String**|El nombre de la base de datos en el que reside la tabla especificada.|  
|TABLE_SCHEM|**String**|El nombre de esquema de la tabla.|  
|TABLE_NAME|**String**|El nombre de la tabla.|  
|TABLE_TYPE|**String**|Tipo de la tabla.|  
|REMARKS|**String**|La descripción de la tabla.<br /><br /> **Nota:** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] no devuelve un valor para esta columna.  |  
|TYPE_CAT|**String**|El controlador JDBC no lo admite.|  
|TYPE_SCHEM|**String**|El controlador JDBC no lo admite.|  
|TYPE_NAME|**String**|El controlador JDBC no lo admite.|  
|SELF_REFERENCING_COL_NAME|**String**|El controlador JDBC no lo admite.|  
|REF_GENERATION|**String**|El controlador JDBC no lo admite.|  
  
> [!NOTE]  
>  Para obtener más información acerca de los datos devueltos por el método getTables, vea "sp_tables (Transact-SQL)" en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] libros en pantalla.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se muestra cómo utilizar el método getTables para devolver la información de descripción de la tabla para la tabla Person.Contact en la [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] base de datos de ejemplo.  
  
```  
public static void executeGetTables(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getTables("AdventureWorks", "Person", "Contact", null);  
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
  
  

