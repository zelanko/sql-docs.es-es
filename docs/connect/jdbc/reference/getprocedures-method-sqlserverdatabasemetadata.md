---
title: "Método getProcedures (SQLServerDatabaseMetaData) | Documentos de Microsoft"
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
- SQLServerDatabaseMetaData.getProcedures
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 66c9a8b0-dc4c-4cbb-8004-c7157368cab4
caps.latest.revision: 24
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 3b1fb6671ac6f223b4e3dcc620f5f7144432abe8
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="getprocedures-method-sqlserverdatabasemetadata"></a>Método getProcedures (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera una descripción de los procedimientos almacenados que están disponibles en un modelo de nombre determinado de catálogo, esquema o procedimiento.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.sql.ResultSet getProcedures(java.lang.String sCatalog,  
                                        java.lang.String sSchema,  
                                        java.lang.String proc)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *sCatalog*  
  
 A **cadena** que contiene el nombre del catálogo. Si se proporciona un valor NULL en este parámetro, indicará que no es necesario utilizar el nombre de catálogo.  
  
 *SEL*  
  
 A **cadena** que contiene el patrón de nombre de esquema. Si se proporciona un valor NULL en este parámetro, indicará que no es necesario utilizar el nombre de esquema.  
  
 *proc*  
  
 A **cadena** que contiene el patrón de nombre de procedimiento.  
  
## <a name="return-value"></a>Valor devuelto  
 A [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método getProcedures es especificado por el método getProcedures en la interfaz java.sql.DatabaseMetaData.  
  
 El conjunto de resultados devuelto por el método getProcedures contendrá la siguiente información:  
  
|Nombre|Tipo|Description|  
|----------|----------|-----------------|  
|PROCEDURE_CAT|**String**|Nombre de la base de datos en la que reside el procedimiento almacenado.|  
|PROCEDURE_SCHEM|**String**|Esquema para el procedimiento almacenado.|  
|PROCEDURE_NAME|**String**|El nombre del procedimiento almacenado.|  
|NUM_INPUT_PARAMS|**int**|Se reserva para su uso futuro, actualmente devuelve un valor -1.|  
|NUM_OUTPUT_PARAMS|**int**|Se reserva para su uso futuro, actualmente devuelve un valor -1.|  
|NUM_RESULT_SETS|**int**|Se reserva para su uso futuro, actualmente devuelve un valor -1.|  
|REMARKS|**String**|Descripción de esta columna de procedimientos.<br /><br /> <br /><br /> **Nota:** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] no devuelve un valor para esta columna.|  
|PROCEDURE_TYPE|**smallint**|Nombre tipo del procedimiento almacenado. Puede ser uno de los siguientes valores:<br /><br /> SQL_PT_UNKNOWN (0)<br /><br /> SQL_PT_PROCEDURE (1)<br /><br /> SQL_PT_FUNCTION (2)|  
  
> [!NOTE]  
>  Para obtener más información acerca de los datos devueltos por el método getProcedures, vea "sp_stored_procedures (Transact-SQL)" en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] libros en pantalla.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se muestra cómo utilizar el método getProcedures para devolver información sobre el procedimiento almacenado uspGetBillOfMaterials en la [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] base de datos de ejemplo.  
  
```  
public static void executeGetProcedures(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getProcedures(null, null, "uspGetBillOfMaterials");  
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
  
  
