---
title: "Método getProcedureColumns (SQLServerDatabaseMetaData) | Documentos de Microsoft"
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
- SQLServerDatabaseMetaData.getProcedureColumns
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4f0df8fe-3cd6-46e4-ae3c-dc23c35676b2
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 847a037a1721e6ecd517d78f99d96b0ef2754aba
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="getprocedurecolumns-method-sqlserverdatabasemetadata"></a>Método getProcedureColumns (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera una descripción de los parámetros de procedimiento almacenado y de las columnas de resultados.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.sql.ResultSet getProcedureColumns(java.lang.String sCatalog,  
                                              java.lang.String sSchema,  
                                              java.lang.String proc,  
                                              java.lang.String col)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *sCatalog*  
  
 A **cadena** que contiene el nombre del catálogo. Si se proporciona un valor NULL en este parámetro, indicará que no es necesario utilizar el nombre de catálogo.  
  
 *SEL*  
  
 A **cadena** que contiene el patrón de nombre de esquema. Si se proporciona un valor NULL en este parámetro, indicará que no es necesario utilizar el nombre de esquema.  
  
 *proc*  
  
 A **cadena** que contiene el patrón de nombre de procedimiento.  
  
 *Col.*  
  
 A **cadena** que contiene el patrón de nombre de columna. Si se proporciona un valor NULL en este parámetro, devolverá una fila para cada columna.  
  
## <a name="return-value"></a>Valor devuelto  
 A [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método getProcedureColumns especificado por el método getProcedureColumns en la interfaz java.sql.DatabaseMetaData.  
  
 El conjunto de resultados devuelto por el método getProcedureColumns contendrá la siguiente información:  
  
|Nombre|Tipo|Description|  
|----------|----------|-----------------|  
|PROCEDURE_CAT|**String**|Nombre de la base de datos en la que reside el procedimiento almacenado.|  
|PROCEDURE_SCHEM|**String**|Esquema para el procedimiento almacenado.|  
|PROCEDURE_NAME|**String**|El nombre del procedimiento almacenado.|  
|COLUMN_NAME|**String**|Nombre de la columna.|  
|COLUMN_TYPE|**corto**|El tipo de la columna. Puede ser uno de los siguientes valores:<br /><br /> procedureColumnUnknown (0)<br /><br /> procedureColumnIn (1)<br /><br /> procedureColumnInOut (2)<br /><br /> procedureColumnOut (4)<br /><br /> procedureColumnReturn (5)<br /><br /> procedureColumnResult (3)|  
|DATA_TYPE|**smallint**|Tipo de datos SQL de java.sql.Types.|  
|TYPE_NAME|**String**|El nombre del tipo de datos.|  
|PRECISION|**int**|Número total de dígitos significativos.|  
|LENGTH|**int**|La longitud de los datos en bytes.|  
|SCALE|**corto**|El número de dígitos a la derecha del separador decimal.|  
|RADIX|**corto**|Base de tipos numéricos.|  
|NULLABLE|**corto**|Indica si la columna puede contener un valor NULL. Puede ser uno de los siguientes valores:<br /><br /> procedureNoNulls (0)<br /><br /> procedureNullable (1)<br /><br /> procedureNullableUnknown (2)|  
|REMARKS|**String**|Descripción de esta columna de procedimientos.<br /><br /> <br /><br /> **Nota:** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] no devuelve un valor para esta columna.|  
|COLUMN_DEF|**String**|El valor predeterminado de la columna.|  
|SQL_DATA_TYPE|**smallint**|Esta columna es el mismo que el **DATA_TYPE** columna, excepto para la **datetime** e ISO **intervalo** tipos de datos.|  
|SQL_DATETIME_SUB|**smallint**|El **datetime** ISO **intervalo** subcódigo si el valor de **SQL_DATA_TYPE** es **SQL_DATETIME** o **SQL_INTERVAL**. Para tipos de datos distinto de **datetime** e ISO **intervalo**, esta columna es NULL.|  
|CHAR_OCTET_LENGTH|**int**|Número máximo de bytes en la columna.|  
|ORDINAL_POSITION|**int**|Índice de la columna en la tabla.|  
|IS_NULLABLE|**String**|Indica si la columna admite valores NULL.|  
|SS_TYPE_CATALOG_NAME|**String**|Nombre del catálogo que contiene el tipo definido por el usuario (UDT).|  
|SS_TYPE_SCHEMA_NAME|**String**|Nombre del esquema que contiene el tipo definido por el usuario (UDT).|  
|SS_UDT_CATALOG_NAME|**String**|Tipo definido por el usuario (UDT) del nombre completo.|  
|SS_UDT_SCHEMA_NAME|**String**|Nombre del catálogo donde se define el nombre de una colección de esquemas XML. Si no se encuentra el nombre del catálogo, esta variable contiene una cadena vacía.|  
|SS_UDT_ASSEMBLY_TYPE_NAME|**String**|Nombre del esquema donde se define el nombre de una colección de esquemas XML. Si no se puede encontrar el nombre de esquema, esta cadena estará vacía.|  
|SS_XML_SCHEMACOLLECTION_CATALOG_NAME|**String**|Nombre de una colección de esquemas XML. Si no se puede encontrar el nombre, esta cadena estará vacía.|  
|SS_XML_SCHEMACOLLECTION_SCHEMA_NAME|**String**|Nombre del catálogo que contiene el tipo definido por el usuario (UDT).|  
|SS_XML_SCHEMACOLLECTION_NAME|**String**|Nombre del esquema que contiene el tipo definido por el usuario (UDT).|  
|SS_DATA_TYPE|**tinyint**|El [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] tipo de datos que utiliza los procedimientos almacenados extendidos.<br /><br /> <br /><br /> **Nota:** para obtener más información acerca de los tipos de datos devueltos por [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)], vea "Tipos de datos (Transact-SQL)" en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] libros en pantalla.|  
  
> [!NOTE]  
>  Para obtener más información acerca de los datos devueltos por el método getProcedureColumns, vea "sp_sproc_columns (Transact-SQL)" en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] libros en pantalla.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se muestra cómo utilizar el método getProcedureColumns para devolver información sobre el procedimiento almacenado uspGetBillOfMaterials en la [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] base de datos de ejemplo.  
  
```  
public static void executeGetProcedureColumns(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getProcedureColumns(null, null, "uspGetBillOfMaterials", null);  
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
 [Miembros de SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Clase SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  

