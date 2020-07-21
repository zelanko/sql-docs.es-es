---
title: Método getProcedureColumns (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getProcedureColumns
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4f0df8fe-3cd6-46e4-ae3c-dc23c35676b2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1767519cc2f36bac4a70da84efeb8da9e2a1ec3c
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "67980751"
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
  
 Objeto **String** que contiene el nombre del catálogo. Si se proporciona un valor NULL en este parámetro, indicará que no es necesario utilizar el nombre de catálogo.  
  
 *sSchema*  
  
 Objeto **String** que contiene el modelo de nombre del esquema. Si se proporciona un valor NULL en este parámetro, indicará que no es necesario utilizar el nombre de esquema.  
  
 *proc*  
  
 Objeto **String** que contiene el modelo de nombre del procedimiento.  
  
 *col*  
  
 Objeto **String** que contiene el patrón de nombre de columna. Si se proporciona un valor NULL en este parámetro, devolverá una fila para cada columna.  
  
## <a name="return-value"></a>Valor devuelto  
 Objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método getProcedureColumns especifica este método getProcedureColumns en la interfaz java.sql.DatabaseMetaData.  
  
 El conjunto de resultados devuelto por el método getProcedureColumns contendrá la siguiente información:  
  
|Nombre|Tipo|Descripción|  
|----------|----------|-----------------|  
|PROCEDURE_CAT|**String**|Nombre de la base de datos en la que reside el procedimiento almacenado.|  
|PROCEDURE_SCHEM|**String**|Esquema para el procedimiento almacenado.|  
|PROCEDURE_NAME|**String**|Nombre del procedimiento almacenado.|  
|COLUMN_NAME|**String**|Nombre de la columna.|  
|COLUMN_TYPE|**short**|El tipo de la columna. Puede ser uno de los siguientes valores:<br /><br /> procedureColumnUnknown (0)<br /><br /> procedureColumnIn (1)<br /><br /> procedureColumnInOut (2)<br /><br /> procedureColumnOut (4)<br /><br /> procedureColumnReturn (5)<br /><br /> procedureColumnResult (3)|  
|DATA_TYPE|**smallint**|Tipo de datos SQL de java.sql.Types.|  
|TYPE_NAME|**String**|El nombre del tipo de datos.|  
|PRECISION|**int**|Número total de dígitos significativos.|  
|LENGTH|**int**|La longitud de los datos, en bytes.|  
|SCALE|**short**|Número de dígitos que se encuentran a la derecha del separador decimal.|  
|RADIX|**short**|Base de tipos numéricos.|  
|NULLABLE|**short**|Indica si la columna puede contener un valor NULL. Puede ser uno de los siguientes valores:<br /><br /> procedureNoNulls (0)<br /><br /> procedureNullable (1)<br /><br /> procedureNullableUnknown (2)|  
|COMENTARIOS|**String**|Descripción de esta columna de procedimientos.<br /><br /> <br /><br /> **Nota:** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no devuelve ningún valor relativo a esta columna.|  
|COLUMN_DEF|**String**|Valor predeterminado de la columna.|  
|SQL_DATA_TYPE|**smallint**|Esta columna es igual que la columna **DATA_TYPE**, salvo por los tipos de datos **datetime** e **interval** de ISO.|  
|SQL_DATETIME_SUB|**smallint**|El subcódigo **datetime** ISO **interval** si el valor de **SQL_DATA_TYPE** es **SQL_DATETIME** o **SQL_INTERVAL**. Para tipos de datos distintos de **datetime** e **interval** de ISO, esta columna es NULL.|  
|CHAR_OCTET_LENGTH|**int**|Número máximo de bytes en la columna.|  
|ORDINAL_POSITION|**int**|Índice de la columna en la tabla.|  
|IS_NULLABLE|**String**|Indica si la columna admite valores NULL.|  
|SS_TYPE_CATALOG_NAME|**String**|Nombre del catálogo que contiene el tipo definido por el usuario (UDT).|  
|SS_TYPE_SCHEMA_NAME|**String**|Nombre del esquema que contiene el tipo definido por el usuario (UDT).|  
|SS_UDT_CATALOG_NAME|**String**|Tipo definido por el usuario (UDT) del nombre completo.|  
|SS_UDT_SCHEMA_NAME|**String**|Nombre del catálogo donde se define el nombre de una colección de esquemas XML. Si no se encuentra el nombre de catálogo, esta variable contiene una cadena vacía.|  
|SS_UDT_ASSEMBLY_TYPE_NAME|**String**|Nombre del esquema donde se define el nombre de una colección de esquemas XML. Si no se puede encontrar el nombre de esquema, esta cadena estará vacía.|  
|SS_XML_SCHEMACOLLECTION_CATALOG_NAME|**String**|Nombre de una colección de esquemas XML. Si no se puede encontrar el nombre, esta cadena estará vacía.|  
|SS_XML_SCHEMACOLLECTION_SCHEMA_NAME|**String**|Nombre del catálogo que contiene el tipo definido por el usuario (UDT).|  
|SS_XML_SCHEMACOLLECTION_NAME|**String**|Nombre del esquema que contiene el tipo definido por el usuario (UDT).|  
|SS_DATA_TYPE|**tinyint**|Tipo de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que utilizan los procedimientos almacenados extendidos.<br /><br /> <br /><br /> **Nota:** Para más información sobre los tipos de datos que [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] devuelve, vea "Tipos de datos (Transact-SQL)" en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
  
> [!NOTE]  
>  Para más información sobre los datos que devuelve el método getProcedureColumns, vea "sp_sproc_columns (Transact-SQL)" en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="example"></a>Ejemplo  
 En el siguiente ejemplo se muestra cómo utilizar el método getProcedureColumns para devolver información sobre el procedimiento almacenado uspGetBillOfMaterials en la base de datos de ejemplo [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)].  
  
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
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Clase SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
