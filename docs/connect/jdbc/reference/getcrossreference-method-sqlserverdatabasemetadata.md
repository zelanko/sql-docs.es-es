---
title: Método getCrossReference (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getCrossReference
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 099dd0bf-b017-479d-9696-f5b06f4c6bf9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f23da4d83217fbed39e6dddacfe92541eae0db23
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "67984218"
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
  
 Objeto **String** que contiene el nombre del catálogo de la tabla que incluye la clave principal.  
  
 *schem1*  
  
 Objeto **String** que contiene el nombre del esquema de la tabla que incluye la clave principal.  
  
 *tab1*  
  
 Objeto **String** que contiene el nombre de tabla de la tabla que incluye la clave principal.  
  
 *cat2*  
  
 Objeto **String** que contiene el nombre del catálogo de la tabla que incluye la clave externa.  
  
 *schem2*  
  
 Objeto **String** que contiene el nombre del esquema de la tabla que incluye la clave externa.  
  
 *tab2*  
  
 Objeto **String** que contiene el nombre de tabla de la tabla que incluye la clave externa.  
  
## <a name="return-value"></a>Valor devuelto  
 Objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método getCrossReference especifica este método getCrossReference en la interfaz java.sql.ParameterMetaData.  
  
 El conjunto de resultados devuelto por el método getCrossReference contendrá la siguiente información:  
  
|Nombre|Tipo|Descripción|  
|----------|----------|-----------------|  
|PKTABLE_CAT|**String**|Nombre del catálogo que contiene la tabla de la clave principal.|  
|PKTABLE_SCHEM|**String**|Nombre del esquema de la tabla de la clave principal.|  
|PKTABLE_NAME|**String**|Nombre de la tabla de la clave principal.|  
|PKCOLUMN_NAME|**String**|Nombre de la columna de la clave principal.|  
|FKTABLE_CAT|**String**|Nombre del catálogo que contiene la tabla de la clave externa.|  
|FKTABLE_SCHEM|**String**|Nombre del esquema de la tabla de la clave externa.|  
|FKTABLE_NAME|**String**|Nombre de la tabla de la clave externa.|  
|FKCOLUMN_NAME|**String**|Nombre de la columna de la clave externa.|  
|KEY_SEQ|**short**|Número de secuencia de la columna en una clave principal en varias columnas.|  
|UPDATE_RULE|**short**|Acción aplicada a la clave externa cuando la operación de SQL sea una actualización. Puede ser uno de los siguientes valores:<br /><br /> importedKeyNoAction (3)<br /><br /> importedKeyCascade (0)<br /><br /> importedKeySetNull (2)<br /><br /> importedKeySetDefault (4)<br /><br /> importedKeyRestrict (1)|  
|DELETE_RULE|**short**|Acción aplicada a la clave externa cuando la operación de SQL sea una eliminación. Puede ser uno de los siguientes valores:<br /><br /> importedKeyNoAction (3)<br /><br /> importedKeyCascade (0)<br /><br /> importedKeySetNull (2)<br /><br /> importedKeySetDefault (4)<br /><br /> importedKeyRestrict (1)|  
|FK_NAME|**String**|El nombre de la clave externa.|  
|PK_NAME|**String**|Nombre de la clave principal.|  
|DEFERRABILITY|**short**|Indica si la evaluación de la restricción de la clave externa se puede diferir hasta que se efectúe una confirmación. Puede ser uno de los siguientes valores:<br /><br /> importedKeyInitiallyDeferred (5)<br /><br /> importedKeyInitiallyImmediate (6)<br /><br /> importedKeyNotDeferrable (7)|  
  
> [!NOTE]  
>  Para más información sobre los datos que devuelve el método getCrossReference, vea "sp_fkeys (Transact-SQL)" en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="example"></a>Ejemplo  
 En el siguiente ejemplo se muestra cómo utilizar el método getCrossReference para devolver información sobre la relación de las claves principal y externa con las tablas Person.Contact y HumanResources.Employee en la base de datos de ejemplo [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)].  
  
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
  
## <a name="see-also"></a>Consulte también  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Miembros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Clase SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
