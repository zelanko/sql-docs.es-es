---
title: Método getPrimaryKeys (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getPrimaryKeys
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ebfe236a-dc02-493e-a3ab-5353d3769e36
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: bd6249f11c9026c1ec036d3ccf11b010dafda2e9
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66771214"
---
# <a name="getprimarykeys-method-sqlserverdatabasemetadata"></a>Método getPrimaryKeys (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera una descripción de las columnas de clave principal de la tabla determinada.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.sql.ResultSet getPrimaryKeys(java.lang.String cat,  
                                         java.lang.String schema,  
                                         java.lang.String table)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *cat*  
  
 Objeto **String** que contiene el nombre del catálogo.  
  
 *schema*  
  
 Objeto **String** que contiene el nombre del esquema.  
  
 *table*  
  
 Objeto **String** que contiene el nombre de la tabla.  
  
## <a name="return-value"></a>Valor devuelto  
 Objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 Este método getPrimaryKeys especificado por el método getPrimaryKeys en la interfaz java.sql.DatabaseMetaData.  
  
 El conjunto de resultados devuelto por el método getPrimaryKeys contendrá la siguiente información:  
  
|Nombre|Tipo|Descripción|  
|----------|----------|-----------------|  
|TABLE_CAT|String|Nombre de la base de datos en la que reside la tabla especificada.|  
|TABLE_SCHEM|String|El esquema para la tabla.|  
|TABLE_NAME|String|Nombre de la tabla.|  
|COLUMN_NAME|String|Nombre de la columna.|  
|KEY_SEQ|short|Número de secuencia de la columna en una clave principal en varias columnas.|  
|PK_NAME|String|Nombre de la clave principal.|  
  
> [!NOTE]  
>  Para más información sobre los datos que devuelve el método getPrimaryKeys, vea "sp_pkeys (Transact-SQL)" en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="example"></a>Ejemplo  
 En el siguiente ejemplo se muestra cómo utilizar el método getPrimaryKeys para devolver información sobre todas las claves principales tabla Person.Contact en la base de datos de ejemplo [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)].  
  
```  
public static void executeGetPrimaryKeys(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getPrimaryKeys("AdventureWorks", "Person", "Contact");  
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
  
  
