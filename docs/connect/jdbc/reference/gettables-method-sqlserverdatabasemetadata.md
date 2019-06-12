---
title: Método getTables (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getTables
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: a7514673-3457-4541-9560-28a8284ad9e3
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 81cb6429cbf1c3f1dd1d97a0aee9458fff637f15
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66779067"
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
 *catalog*  
  
 Objeto **String** que contiene el nombre del catálogo. Si se proporciona un valor NULL en este parámetro, indicará que no es necesario utilizar el nombre de catálogo.  
  
 *schema*  
  
 Objeto **String** que contiene el modelo de nombre del esquema. Si se proporciona un valor NULL en este parámetro, indicará que no es necesario utilizar el nombre de esquema.  
  
 *tableName*  
  
 Objeto **String** que contiene el patrón de nombre de tabla.  
  
 *types*  
  
 Una matriz de cadenas que contiene los tipos de tablas que se van a incluir. El valor NULL indica que todos los tipos de tablas deberían estar incluidos.  
  
## <a name="return-value"></a>Valor devuelto  
 Objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 El método getTables especifica este método getTables en la interfaz java.sql.DatabaseMetaData.  
  
 El conjunto de resultados devuelto por el método getTables contendrá la siguiente información:  
  
|Nombre|Tipo|Descripción|  
|----------|----------|-----------------|  
|TABLE_CAT|**String**|Nombre de la base de datos en la que reside la tabla especificada.|  
|TABLE_SCHEM|**String**|Es el esquema de la tabla.|  
|TABLE_NAME|**String**|El nombre de la tabla.|  
|TABLE_TYPE|**String**|Tipo de la tabla.|  
|REMARKS|**String**|Descripción de la tabla.<br /><br /> **Nota:** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no devuelve ningún valor relativo a esta columna.|  
|TYPE_CAT|**String**|El controlador JDBC no lo admite.|  
|TYPE_SCHEM|**String**|El controlador JDBC no lo admite.|  
|TYPE_NAME|**String**|El controlador JDBC no lo admite.|  
|SELF_REFERENCING_COL_NAME|**String**|El controlador JDBC no lo admite.|  
|REF_GENERATION|**String**|El controlador JDBC no lo admite.|  
  
> [!NOTE]  
>  Para más información sobre los datos que devuelve el método getTables, vea "sp_tables (Transact-SQL)" en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="example"></a>Ejemplo  
 En el siguiente ejemplo se muestra cómo utilizar el método getTables para devolver información sobre la descripción en la tabla para la tabla Person.Contact en la base de datos de ejemplo [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)].  
  
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
  
## <a name="see-also"></a>Consulte también  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Miembros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Clase SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
