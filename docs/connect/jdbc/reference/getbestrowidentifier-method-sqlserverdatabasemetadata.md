---
title: Método getBestRowIdentifier (SQLServerDatabaseMetaData) | Documentos de Microsoft
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
- SQLServerDatabaseMetaData.getBestRowIdentifier
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: c19e9ca6-2a53-4a0c-91ab-80090c3f7229
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c36b69543f5253a4d62c1d4b149933febcf0b4b4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32832980"
---
# <a name="getbestrowidentifier-method-sqlserverdatabasemetadata"></a>Método getBestRowIdentifier (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera una descripción del conjunto óptimo de columnas de una tabla que identifique una fila de forma única.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.sql.ResultSet getBestRowIdentifier(java.lang.String catalog,  
                                               java.lang.String schema,  
                                               java.lang.String table,  
                                               int scope,  
                                               boolean nullable)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *catalog*  
  
 A **cadena** que contiene el nombre del catálogo.  
  
 *schema*  
  
 A **cadena** que contiene el nombre del esquema.  
  
 *table*  
  
 A **cadena** que contiene el nombre de tabla.  
  
 *ámbito*  
  
 Un **int** que indica el ámbito de interés. Los valores pueden incluir lo siguiente:  
  
 bestRowTemporary (0)  
  
 bestRowTransaction (1)  
  
 bestRowSession (2)  
  
 *Que aceptan valores null*  
  
 **True** para incluir columnas que aceptan valores NULL. De lo contrario, se devuelve el valor **False**.  
  
## <a name="return-value"></a>Valor devuelto  
 A [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método getBestRowIdentifier especificado por el método getBestRowIdentifier en la interfaz java.sql.DatabaseMetaData.  
  
 El conjunto de resultados devuelto por el método getBestRowIdentifier contendrá la siguiente información:  
  
|Nombre|Tipo|Description|  
|----------|----------|-----------------|  
|SCOPE|short|Ámbito de los resultados devueltos. Puede ser uno de los siguientes valores:<br /><br /> bestRowTemporary (0)<br /><br /> bestRowTransaction (1)<br /><br /> bestRowSession (2)|  
|COLUMN_NAME|String|Nombre de la columna.|  
|DATA_TYPE|short|Tipo de datos SQL de java.sql.Types.|  
|TYPE_NAME|String|El nombre del tipo de datos.|  
|COLUMN_SIZE|int|La precisión de la columna.|  
|BUFFER_LENGTH|int|Longitud del búfer.|  
|DECIMAL_DIGITS|short|La escala de la columna.|  
|PSEUDO_COLUMN|short|Indica si la columna es una pseudocolumna. Puede ser uno de los siguientes valores:<br /><br /> bestRowUnknown (0)<br /><br /> bestRowNotPseudo (1)<br /><br /> bestRowPseudo (2)|  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se muestra cómo utilizar el método getBestRowIdentifier para devolver información sobre el identificador de fila recomendado para la tabla Person.Contact en la [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] base de datos de ejemplo.  
  
```  
public static void executeGetBestRowIdentifier(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getBestRowIdentifier(null, "Person", "Contact", 0, true);  
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
  
  
