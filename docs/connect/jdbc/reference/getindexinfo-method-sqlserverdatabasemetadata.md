---
title: Método getIndexInfo (SQLServerDatabaseMetaData) | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getIndexInfo
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 8a677cc6-8e33-4e57-8678-0849345aa8d0
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cef7b37818e5bc7bf46c7181a3816edd5bbad860
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="getindexinfo-method-sqlserverdatabasemetadata"></a>Método getIndexInfo (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera una descripción de los índices y estadísticas para la tabla dada.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.sql.ResultSet getIndexInfo(java.lang.String cat,  
                                       java.lang.String schema,  
                                       java.lang.String table,  
                                       boolean unique,  
                                       boolean approximate)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *CAT*  
  
 A **cadena** que contiene el nombre del catálogo.  
  
 *schema*  
  
 A **cadena** que contiene el nombre del esquema.  
  
 *table*  
  
 A **cadena** que contiene el nombre de tabla.  
  
 *Único*  
  
 **True** si solo se devuelven índices para valores únicos. **false** si se devuelven todos los índices.  
  
 *aproximado*  
  
 **True** si los resultados reflejan valores aproximados o no actualizados. **false** si los resultados son precisos.  
  
## <a name="return-value"></a>Valor devuelto  
 A [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método getIndexInfo especificado por el método getIndexInfo en la interfaz java.sql.DatabaseMetaData.  
  
 El conjunto de resultados devuelto por el método getIndexInfo contendrá la siguiente información:  
  
|Nombre|Tipo|Description|  
|----------|----------|-----------------|  
|TABLE_CAT|**String**|El nombre de la base de datos en el que reside la tabla especificada.|  
|TABLE_SCHEM|**String**|El esquema para la tabla.|  
|TABLE_NAME|**String**|Nombre de la tabla.|  
|NON_UNIQUE|**boolean**|Indica si los valores de índice pueden ser no únicos.|  
|INDEX_QUALIFIER|**String**|El nombre del propietario del índice. Se devolverá un valor NULL cuando TYPE sea tableIndexStatistic.|  
|INDEX_NAME|**String**|El nombre del índice.|  
|TYPE|**Corto**|El tipo del índice. Puede ser uno de los siguientes valores:<br /><br /> tableIndexStatistic (0)<br /><br /> tableIndexClustered (1)<br /><br /> tableIndexHashed (2)<br /><br /> tableIndexOther (3)|  
|ORDINAL_POSITION|**Corto**|Posición ordinal de la columna en el índice. La primera columna del índice es 1.|  
|COLUMN_NAME|**String**|Nombre de la columna.|  
|ASC_OR_DESC|**String**|Orden utilizado en la intercalación del índice: Puede ser uno de los siguientes valores:<br /><br /> A (ascendente)<br /><br /> D (descendente)<br /><br /> NULL (no aplicable)<br /><br /> **Nota:** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] siempre devuelve "A".  |  
|CARDINALITY|**int**|Número de filas de la tabla o de valores únicos del índice.|  
|PAGES|**int**|El número de páginas utilizadas para almacenar el índice o tabla.|  
|FILTER_CONDITION|**String**|Condición del filtro.<br /><br /> **Nota:** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] siempre devuelve null.  |  
  
> [!NOTE]  
>  Para obtener más información acerca de los datos devueltos por el método getIndexInfo, vea "sp_indexes (Transact-SQL)" en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] libros en pantalla.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se muestra cómo utilizar el método getIndexInfo para devolver información acerca de los índices y estadísticas de la tabla Person.Contact en la [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] base de datos de ejemplo.  
  
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
  
## <a name="see-also"></a>Vea también  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Miembros de SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Clase SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
