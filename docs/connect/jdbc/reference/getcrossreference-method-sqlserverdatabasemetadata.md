---
title: Método getCrossReference (SQLServerDatabaseMetaData) | Documentos de Microsoft
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
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getCrossReference
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 099dd0bf-b017-479d-9696-f5b06f4c6bf9
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 81764e3e8b049207913020a2ee75528945b39419
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="getcrossreference-method-sqlserverdatabasemetadata"></a>Método getCrossReference (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera una descripción de las columnas de clave externa en la tabla de clave externa determinada que hace referencia a las columnas de clave principal de la tabla de claves principales determinada.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.sql.ResultSet getCrossReference(java.lang.String cat1,  
                                            java.lang.String schem1,  
                                            java.lang.String tab1,  
                                            java.lang.String cat2,  
                                            java.lang.String schem2,  
                                            java.lang.String tab2)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *cat1*  
  
 A **cadena** que contiene el nombre del catálogo de la tabla que contiene la clave principal.  
  
 *schem1*  
  
 A **cadena** que contiene el nombre del esquema de la tabla que contiene la clave principal.  
  
 *Tab1*  
  
 A **cadena** que contiene el nombre de tabla de la tabla que contiene la clave principal.  
  
 *Cat2*  
  
 A **cadena** que contiene el nombre del catálogo de la tabla que contiene la clave externa.  
  
 *schem2*  
  
 A **cadena** que contiene el nombre del esquema de la tabla que contiene la clave externa.  
  
 *Tab2*  
  
 A **cadena** que contiene el nombre de tabla de la tabla que contiene la clave externa.  
  
## <a name="return-value"></a>Valor devuelto  
 A [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método getCrossReference especificado por el método getCrossReference en la interfaz java.sql.DatabaseMetaData.  
  
 El conjunto de resultados devuelto por el método getCrossReference contendrá la siguiente información:  
  
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
|KEY_SEQ|**Corto**|Número de secuencia de la columna en una clave principal en varias columnas.|  
|UPDATE_RULE|**Corto**|Acción aplicada a la clave externa cuando la operación de SQL sea una actualización. Puede ser uno de los siguientes valores:<br /><br /> importedKeyNoAction (3)<br /><br /> importedKeyCascade (0)<br /><br /> importedKeySetNull (2)<br /><br /> importedKeySetDefault (4)<br /><br /> importedKeyRestrict (1)|  
|DELETE_RULE|**Corto**|Acción aplicada a la clave externa cuando la operación de SQL sea una eliminación. Puede ser uno de los siguientes valores:<br /><br /> importedKeyNoAction (3)<br /><br /> importedKeyCascade (0)<br /><br /> importedKeySetNull (2)<br /><br /> importedKeySetDefault (4)<br /><br /> importedKeyRestrict (1)|  
|FK_NAME|**String**|El nombre de la clave externa.|  
|PK_NAME|**String**|Nombre de la clave principal.|  
|DEFERRABILITY|**Corto**|Indica si la evaluación de la restricción de la clave externa se puede diferir hasta que se efectúe una confirmación. Puede ser uno de los siguientes valores:<br /><br /> importedKeyInitiallyDeferred (5)<br /><br /> importedKeyInitiallyImmediate (6)<br /><br /> importedKeyNotDeferrable (7)|  
  
> [!NOTE]  
>  Para obtener más información acerca de los datos devueltos por el método getCrossReference, vea "sp_fkeys (Transact-SQL)" en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] libros en pantalla.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se muestra cómo utilizar el método getCrossReference para devolver información sobre la relación de clave principal y externa entre las tablas Person.Contact y HumanResources.Employee en la [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] base de datos de ejemplo.  
  
```  
public static void executeGetCrossReference(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getCrossReference("AdventureWorks", "Person", "Contact", null, "HumanResources", "Employee");  
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
  
  
