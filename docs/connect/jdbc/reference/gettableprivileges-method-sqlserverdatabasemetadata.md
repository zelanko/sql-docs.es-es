---
title: Método getTablePrivileges (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getTablePrivileges
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 0610d667-a16d-4201-a14b-0a40048911e1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d0fe3b01fd02bf48fb5f38707530e3b3344133e6
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "67979223"
---
# <a name="gettableprivileges-method-sqlserverdatabasemetadata"></a>Método getTablePrivileges (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera una descripción de los derechos de acceso para cada tabla que está disponible en el modelo del nombre determinado de catálogo, esquema o tabla.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.sql.ResultSet getTablePrivileges(java.lang.String catalog,  
                                             java.lang.String schema,  
                                             java.lang.String table)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *catalog*  
  
 Objeto **String** que contiene el nombre del catálogo. Si se proporciona un valor NULL en este parámetro, indicará que no es necesario utilizar el nombre de catálogo.  
  
 *schema*  
  
 Objeto **String** que contiene el modelo de nombre del esquema. Si se proporciona un valor NULL en este parámetro, indicará que no es necesario utilizar el nombre de esquema.  
  
 *table*  
  
 Objeto **String** que contiene el patrón de nombre de tabla.  
  
## <a name="return-value"></a>Valor devuelto  
 Objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método getTablePrivileges especifica este método getTablePrivileges en la interfaz java.sql.DatabaseMetaData.  
  
 El conjunto de resultados devuelto por el método getTablePrivileges contendrá la siguiente información:  
  
|Nombre|Tipo|Descripción|  
|----------|----------|-----------------|  
|TABLE_CAT|**String**|Nombre del catálogo.|  
|TABLE_SCHEM|**String**|Esquema de la tabla.|  
|TABLE_NAME|**String**|El nombre de la tabla.|  
|GRANTOR|**String**|Objeto que concede el acceso.|  
|GRANTEE|**String**|Objeto que recibe el acceso.|  
|PRIVILEGE|**String**|Tipo de acceso concedido.|  
|IS_GRANTABLE|**String**|Indica si el receptor del acceso puede conceder acceso a otros usuarios.|  
  
> [!NOTE]  
>  Para más información sobre los datos que devuelve el método getTablePrivileges, vea "sp_table_privileges (Transact-SQL)" en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="example"></a>Ejemplo  
 En el siguiente ejemplo se muestra cómo utilizar el método getTablePrivileges para devolver los derechos de acceso correspondientes a la tabla Person.Contact en la base de datos de ejemplo [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)].  
  
```  
public static void executeGetTablePrivileges(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getTablePrivileges("AdventureWorks", "Person", "Contact");  
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
  
  
