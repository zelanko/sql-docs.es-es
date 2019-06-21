---
title: Método getColumnPrivileges (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getColumnPrivileges
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4ab6a671-9573-4b95-8c23-364306c60d25
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 934a230e295532231f52ac3ed787b6a4de366d54
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66763377"
---
# <a name="getcolumnprivileges-method-sqlserverdatabasemetadata"></a>Método getColumnPrivileges (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera una descripción de los derechos de acceso para las columnas en una tabla.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.sql.ResultSet getColumnPrivileges(java.lang.String catalog,  
                                              java.lang.String schema,  
                                              java.lang.String table,  
                                              java.lang.String col)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *catalog*  
  
 Objeto **String** que contiene el nombre del catálogo.  
  
 *schema*  
  
 Objeto **String** que contiene el nombre del esquema.  
  
 *table*  
  
 Objeto **String** que contiene el nombre de la tabla.  
  
 *col*  
  
 Objeto **String** que contiene el patrón de nombre de columna.  
  
## <a name="return-value"></a>Valor devuelto  
 Objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 Este método getColumnPrivileges especificado por el método getColumnPrivileges en la interfaz java.sql.DatabaseMetaData.  
  
 El conjunto de resultados devuelto por el método getColumnPrivileges contendrá la siguiente información:  
  
|Nombre|Tipo|Descripción|  
|----------|----------|-----------------|  
|TABLE_CAT|**String**|Nombre del catálogo.|  
|TABLE_SCHEM|**String**|Esquema de la tabla.|  
|TABLE_NAME|**String**|El nombre de la tabla.|  
|COLUMN_NAME|**String**|Nombre de columna.|  
|GRANTOR|**String**|Objeto que concede el acceso.|  
|GRANTEE|**String**|Objeto que recibe el acceso.|  
|PRIVILEGE|**String**|Tipo de acceso concedido.|  
|IS_GRANTABLE|**String**|Indica si el receptor del acceso puede conceder acceso a otros usuarios.|  
  
> [!NOTE]  
>  Para obtener más información sobre los datos que devuelve el método getColumnPrivileges, vea "sp_column_privileges (Transact-SQL)" en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="example"></a>Ejemplo  
 En el siguiente ejemplo se muestra cómo utilizar el método getColumnPrivileges para devolver los derechos de acceso para la columna FirstName en la tabla Person.Contact en la base de datos de ejemplo [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)].  
  
```  
public static void executeGetColumnPrivileges(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getColumnPrivileges("AdventureWorks", "Person", "Contact", "FirstName");  
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
  
  
