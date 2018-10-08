---
title: Método getProcedures (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getProcedures
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 66c9a8b0-dc4c-4cbb-8004-c7157368cab4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f61427cdc3a71ebba5c6d511c3a5c8068b44c496
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47778753"
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
  
 Objeto **String** que contiene el nombre del catálogo. Si se proporciona un valor NULL en este parámetro, indicará que no es necesario utilizar el nombre de catálogo.  
  
 *SEL*  
  
 Objeto **String** que contiene el modelo de nombre del esquema. Si se proporciona un valor NULL en este parámetro, indicará que no es necesario utilizar el nombre de esquema.  
  
 *proc*  
  
 Objeto **String** que contiene el modelo de nombre del procedimiento.  
  
## <a name="return-value"></a>Valor devuelto  
 Objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 Este método getProcedures especificado por el método getProcedures en la interfaz java.sql.DatabaseMetaData.  
  
 El conjunto de resultados devuelto por el método getProcedures contendrá la siguiente información:  
  
|Nombre|Tipo|Descripción|  
|----------|----------|-----------------|  
|PROCEDURE_CAT|**String**|Nombre de la base de datos en la que reside el procedimiento almacenado.|  
|PROCEDURE_SCHEM|**String**|Esquema para el procedimiento almacenado.|  
|PROCEDURE_NAME|**String**|Nombre del procedimiento almacenado.|  
|NUM_INPUT_PARAMS|**int**|Se reserva para su uso futuro, actualmente devuelve un valor -1.|  
|NUM_OUTPUT_PARAMS|**int**|Se reserva para su uso futuro, actualmente devuelve un valor -1.|  
|NUM_RESULT_SETS|**int**|Se reserva para su uso futuro, actualmente devuelve un valor -1.|  
|REMARKS|**String**|Descripción de esta columna de procedimientos.<br /><br /> <br /><br /> **Nota:** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no devuelve ningún valor relativo a esta columna.|  
|PROCEDURE_TYPE|**smallint**|Nombre tipo del procedimiento almacenado. Puede ser uno de los siguientes valores:<br /><br /> SQL_PT_UNKNOWN (0)<br /><br /> SQL_PT_PROCEDURE (1)<br /><br /> SQL_PT_FUNCTION (2)|  
  
> [!NOTE]  
>  Para más información sobre los datos que devuelve el método getProcedures, vea "sp_stored_procedures (Transact-SQL)" en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="example"></a>Ejemplo  
 En el siguiente ejemplo se muestra cómo utilizar el método getProcedures para devolver información sobre el procedimiento almacenado uspGetBillOfMaterials en la base de datos de ejemplo [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)].  
  
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
  
## <a name="see-also"></a>Ver también  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Miembros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Clase SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
