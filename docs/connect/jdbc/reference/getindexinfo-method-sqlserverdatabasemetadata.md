---
title: Método getIndexInfo (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getIndexInfo
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 8a677cc6-8e33-4e57-8678-0849345aa8d0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8dd512236aa3070ce299756d4e4294c79ac2e94a
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "67982792"
---
# <a name="getindexinfo-method-sqlserverdatabasemetadata"></a>Método getIndexInfo (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera una descripción de los índices y estadísticas de la tabla determinada.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.sql.ResultSet getIndexInfo(java.lang.String cat,  
                                       java.lang.String schema,  
                                       java.lang.String table,  
                                       boolean unique,  
                                       boolean approximate)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *cat*  
  
 Objeto **String** que contiene el nombre del catálogo.  
  
 *schema*  
  
 Objeto **String** que contiene el nombre del esquema.  
  
 *table*  
  
 Objeto **String** que contiene el nombre de la tabla.  
  
 *unique*  
  
 Es **true** si solo se devuelven índices para valores únicos. Es **false** si se devuelven todos los índices.  
  
 *approximate*  
  
 Es **true** si los resultados reflejan valores aproximados o no actualizados. Es **false** si los resultados son precisos.  
  
## <a name="return-value"></a>Valor devuelto  
 Objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método getIndexInfo especifica este método getIndexInfo en la interfaz java.sql.DatabaseMetaData.  
  
 El conjunto de resultados devuelto por el método getIndexInfo contendrá la siguiente información:  
  
|Nombre|Tipo|Descripción|  
|----------|----------|-----------------|  
|TABLE_CAT|**String**|Nombre de la base de datos en la que reside la tabla especificada.|  
|TABLE_SCHEM|**String**|El esquema para la tabla.|  
|TABLE_NAME|**String**|Nombre de la tabla.|  
|NON_UNIQUE|**boolean**|Indica si los valores de índice pueden ser no únicos.|  
|INDEX_QUALIFIER|**String**|Nombre del propietario del índice. Se devolverá un valor NULL cuando TYPE sea tableIndexStatistic.|  
|INDEX_NAME|**String**|El nombre del índice.|  
|TYPE|**short**|El tipo del índice. Puede ser uno de los siguientes valores:<br /><br /> tableIndexStatistic (0)<br /><br /> tableIndexClustered (1)<br /><br /> tableIndexHashed (2)<br /><br /> tableIndexOther (3)|  
|ORDINAL_POSITION|**short**|Posición ordinal de la columna en el índice. La primera columna del índice es 1.|  
|COLUMN_NAME|**String**|Nombre de la columna.|  
|ASC_OR_DESC|**String**|Orden utilizado en la intercalación del índice: Puede ser uno de los siguientes valores:<br /><br /> A (ascendente)<br /><br /> D (descendente)<br /><br /> NULL (no aplicable)<br /><br /> **Nota:** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] siempre devuelve "A".|  
|CARDINALITY|**int**|Número de filas de la tabla o de valores únicos del índice.|  
|PAGES|**int**|Número de páginas usadas para el almacenamiento del índice o la tabla.|  
|FILTER_CONDITION|**String**|Condición del filtro.<br /><br /> **Nota:** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] siempre devuelve NULL.|  
  
> [!NOTE]  
>  Para más información sobre los datos que devuelve el método getIndexInfo, vea "sp_indexes (Transact-SQL)" en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="example"></a>Ejemplo  
 En el siguiente ejemplo se muestra cómo utilizar el método getIndexInfo para devolver información sobre los índices y estadísticas de la tabla Person.Contact en la base de datos de ejemplo [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)].  
  
```  
public static void executeGetIndexInfo(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getIndexInfo("AdventureWorks", "Person", "Contact", false, true);  
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
  
  
