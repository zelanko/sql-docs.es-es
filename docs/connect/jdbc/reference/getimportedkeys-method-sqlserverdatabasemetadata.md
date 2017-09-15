---
title: "Método getImportedKeys (SQLServerDatabaseMetaData) | Documentos de Microsoft"
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
- SQLServerDatabaseMetaData.getImportedKeys
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: dc8c1a5e-700e-4059-a5ed-5013bbb87fb6
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f6639abb34a7d81e7e99f8cb0856ab7ab1f6e046
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="getimportedkeys-method-sqlserverdatabasemetadata"></a>Método getImportedKeys (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera una descripción de las columnas de clave principal que hacen referencia las columnas de clave externa de una tabla.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.sql.ResultSet getImportedKeys(java.lang.String cat,  
                                          java.lang.String schema,  
                                          java.lang.String table)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *CAT*  
  
 A **cadena** que contiene el nombre del catálogo.  
  
 *esquema*  
  
 A **cadena** que contiene el nombre del esquema.  
  
 *table*  
  
 A **cadena** que contiene el nombre de tabla.  
  
## <a name="return-value"></a>Valor devuelto  
 A [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método getImportedKeys especificado por el método getImportedKeys en la interfaz java.sql.DatabaseMetaData.  
  
 El conjunto de resultados devuelto por el método getImportedKeys contendrá la siguiente información:  
  
|Nombre|Tipo|Description|  
|----------|----------|-----------------|  
|PKTABLE_CAT|**String**|Nombre del catálogo que contiene la tabla de la clave principal.|  
|PKTABLE_SCHEM|**String**|Nombre del esquema de la tabla de la clave principal.|  
|PKTABLE_NAME|**String**|Nombre de la tabla de la clave principal.|  
|PKCOLUMN_NAME|**String**|Nombre de la columna de la clave principal.|  
|FKTABLE_CAT|**String**|Nombre del catálogo que contiene la tabla de la clave externa.|  
|FKTABLE_SCHEM|**String**|Nombre del esquema de la tabla de la clave externa.|  
|FKTABLE_NAME|**String**|Nombre de la tabla de la clave externa.|  
|FKCOLUMN_NAME|**String**|Nombre de la columna de la clave externa.|  
|KEY_SEQ|**corto**|Número de secuencia de la columna en una clave principal en varias columnas.|  
|UPDATE_RULE|**corto**|Acción aplicada a la clave externa cuando la operación de SQL sea una actualización. Puede ser uno de los siguientes valores:<br /><br /> importedKeyNoAction (3)<br /><br /> importedKeyCascade (0)<br /><br /> importedKeySetNull (2)<br /><br /> importedKeySetDefault (4)<br /><br /> importedKeyRestrict (1)|  
|DELETE_RULE|**corto**|Acción aplicada a la clave externa cuando la operación de SQL sea una eliminación. Puede ser uno de los siguientes valores:<br /><br /> importedKeyNoAction (3)<br /><br /> importedKeyCascade (0)<br /><br /> importedKeySetNull (2)<br /><br /> importedKeySetDefault (4)<br /><br /> importedKeyRestrict (1)|  
|FK_NAME|**String**|El nombre de la clave externa.|  
|PK_NAME|**String**|Nombre de la clave principal.|  
|DEFERRABILITY|**corto**|Indica si la evaluación de la restricción de la clave externa se puede diferir hasta que se efectúe una confirmación. Puede ser uno de los siguientes valores:<br /><br /> importedKeyInitiallyDeferred (5)<br /><br /> importedKeyInitiallyImmediate (6)<br /><br /> importedKeyNotDeferrable (7)|  
  
> [!NOTE]  
>  Para obtener más información acerca de los datos devueltos por el método getImportedKeys, vea "sp_fkeys (Transact-SQL)" en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] libros en pantalla.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se muestra cómo utilizar el método getImportedKeys para devolver información sobre todas las claves principales que hacen referencia las claves externas de la tabla Person.Address de la [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] base de datos de ejemplo.  
  
```  
public static void executeGetImportedKeys(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getImportedKeys("AdventureWorks", "Person", "Address");  
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
  
  
