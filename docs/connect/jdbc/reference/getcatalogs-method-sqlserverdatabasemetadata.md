---
title: "Método getCatalogs (SQLServerDatabaseMetaData) | Documentos de Microsoft"
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
- SQLServerDatabaseMetaData.getCatalogs
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7f8bd0f1-f340-4bb9-b559-0a6176124033
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6f78577e4f2698966afccba5f1f97855076434e9
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="getcatalogs-method-sqlserverdatabasemetadata"></a>Método getCatalogs (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera los nombres del catálogo que están disponibles en el servidor conectado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.sql.ResultSet getCatalogs()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 A [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método getCatalogs especificado por el método getCatalogs en la interfaz java.sql.DatabaseMetaData.  
  
> [!NOTE]  
>  En SQL Azure, debe conectarse a la base de datos maestra para llamar a **SQLServerDatabaseMetaData.getCatalogs**. SQL Azure no admite devolver todo el conjunto de catálogos de una base de datos de usuario. **SQLServerDatabaseMetaData.getCatalogs** usa la vista sys.databases para obtener los catálogos. Consulte la discusión de permisos en [sys.databases (base de datos de SQL Azure)](http://go.microsoft.com/fwlink/?LinkId=217396) comprender **SQLServerDatabaseMetaData.getCatalogs** comportamiento en SQL Azure.  
  
 El conjunto de resultados devuelto por el método getCatalogs contendrá la siguiente información:  
  
|Nombre|Tipo|Description|  
|----------|----------|-----------------|  
|TABLE_CAT|**String**|El nombre del catálogo, incluidas bases de datos del sistema en [!INCLUDE[msCoName](../../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)].|  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se muestra cómo utilizar el método getCatalogs para devolver los nombres de todas las bases de datos que se encuentran en [!INCLUDE[msCoName](../../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)], incluidas las bases de datos del sistema.  
  
```  
public static void executeGetCatalogs(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getCatalogs();  
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
  
  

