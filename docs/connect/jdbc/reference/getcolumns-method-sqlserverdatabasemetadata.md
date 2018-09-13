---
title: Método getColumns (SQLServerDatabaseMetaData) | Microsoft Docs
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
- SQLServerDatabaseMetaData.getColumns
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f173fa5d-e114-4a37-a5c4-2baad9ff3af1
caps.latest.revision: 39
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d1a8d682e0bb099d082578b98e70dd6930033024
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 08/14/2018
ms.locfileid: "42785841"
---
# <a name="getcolumns-method-sqlserverdatabasemetadata"></a>Método getColumns (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera una descripción de las columnas de la tabla que están disponibles en el catálogo especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.sql.ResultSet getColumns(java.lang.String catalog,  
                                     java.lang.String schema,  
                                     java.lang.String table,  
                                     java.lang.String col)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *catalog*  
  
 Objeto **String** que contiene el nombre del catálogo.  
  
 *schema*  
  
 Objeto **String** que contiene el modelo de nombre del esquema.  
  
 *table*  
  
 Objeto **String** que contiene el patrón de nombre de tabla.  
  
 *col*  
  
 Objeto **String** que contiene el patrón de nombre de columna.  
  
## <a name="return-value"></a>Valor devuelto  
 Objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 Este método getColumns especificado por el método getColumns en la interfaz java.sql.DatabaseMetaData.  
  
 El conjunto de resultados devuelto por el método getColumns contendrá la siguiente información:  
  
|Nombre|Tipo|Descripción|  
|----------|----------|-----------------|  
|TABLE_CAT|**String**|Nombre del catálogo.|  
|TABLE_SCHEM|**String**|El nombre del esquema de tabla.|  
|TABLE_NAME|**String**|El nombre de la tabla.|  
|COLUMN_NAME|**String**|Nombre de columna.|  
|DATA_TYPE|**smallint**|Tipo de datos SQL de java.sql.Types.|  
|TYPE_NAME|**String**|El nombre del tipo de datos.|  
|COLUMN_SIZE|**int**|Precisión de la columna.|  
|BUFFER_LENGTH|**smallint**|Tamaño de transferencia de los datos.|  
|DECIMAL_DIGITS|**smallint**|Escala de la columna.|  
|NUM_PREC_RADIX|**smallint**|Base de la columna.|  
|NULLABLE|**smallint**|Indica si la columna admite valores NULL. Puede ser uno de los siguientes valores:<br /><br /> columnNoNulls (0)<br /><br /> columnNullable (1)|  
|REMARKS|**String**|Comentarios asociados con la columna.<br /><br /> **Nota:** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] siempre devuelve null para esta columna.  |  
|COLUMN_DEF|**String**|Valor predeterminado de la columna.|  
|SQL_DATA_TYPE|**smallint**|Valor del tipo de datos SQL tal como aparece en el campo TYPE del descriptor. Esta columna es igual que la columna DATA_TYPE, salvo por los tipos de datos datetime e interval de SQL-92. Esta columna siempre devuelve un valor.|  
|SQL_DATETIME_SUB|**smallint**|Código de subtipo para los tipos de datos interval de SQL-92 y datetime. Para otros tipos de datos, esta columna devuelve NULL.|  
|CHAR_OCTET_LENGTH|**int**|Número máximo de bytes en la columna.|  
|ORDINAL_POSITION|**int**|Índice de la columna en la tabla.|  
|IS_NULLABLE|**String**|Indica si la columna admite valores NULL.|  
|SS_IS_SPARSE|**smallint**|Si la columna es una columna dispersa, esto tiene el valor 1; de lo contrario, 0.<sup>1</sup>.|  
|SS_IS_COLUMN_SET|**smallint**|Si la columna es la columna column_set dispersa, esto tiene el valor 1; de lo contrario, 0. <sup>1</sup>|  
|SS_IS_COMPUTED|**smallint**|Indica si una columna en un TABLE_TYPE es una columna calculada. <sup>1</sup>|  
|IS_AUTOINCREMENT|**String**|Es "SÍ" si la columna se incrementa automáticamente. Es "NO" si la columna no se incrementa automáticamente. Es "" (cadena vacía) si el controlador no puede determinar si la columna se incrementa automáticamente. <sup>1</sup>|  
|SS_UDT_CATALOG_NAME|**String**|Nombre del catálogo que contiene el tipo definido por el usuario (UDT). <sup>1</sup>|  
|SS_UDT_SCHEMA_NAME|**String**|Nombre del esquema que contiene el tipo definido por el usuario (UDT). <sup>1</sup>|  
|SS_UDT_ASSEMBLY_TYPE_NAME|**String**|Tipo definido por el usuario (UDT) del nombre completo. <sup>1</sup>|  
|SS_XML_SCHEMACOLLECTION_CATALOG_NAME|**String**|Nombre del catálogo donde se define el nombre de una colección de esquemas XML. Si no se encuentra el nombre de catálogo, esta variable contiene una cadena vacía. <sup>1</sup>|  
|SS_XML_SCHEMACOLLECTION_SCHEMA_NAME|**String**|Nombre del esquema donde se define el nombre de una colección de esquemas XML. Si no se puede encontrar el nombre de esquema, esta cadena estará vacía. <sup>1</sup>|  
|SS_XML_SCHEMACOLLECTION_NAME|**String**|Nombre de una colección de esquemas XML. Si no se puede encontrar el nombre, esta cadena estará vacía. <sup>1</sup>|  
|SS_DATA_TYPE|**tinyint**|Tipo de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que utilizan los procedimientos almacenados extendidos.<br /><br /> **Nota:** Para más información sobre los tipos de datos que devuelve [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], vea "Tipos de datos (Transact-SQL)" en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
  
 (1) Esta columna no estará presente si se está conectando con [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].  
  
> [!NOTE]  
>  Para más información sobre los datos que devuelve el método getColumns, vea "sp_columns (Transact-SQL)" en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 En el controlador JDBC 3.0 de [!INCLUDE[msCoName](../../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], observará que existen los siguientes cambios de comportamiento con respecto a las versiones anteriores del controlador JDBC:  
  
 La columna DATA_TYPE tiene los cambios siguientes:  
  
|Tipo de datos [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]|Tipo devuelto en el controlador JDBC 2.0 (o si está conectado con [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]) y constante numérica asociada|Tipo devuelto en el controlador JDBC 3.0 cuando se conecta con [!INCLUDE[ssKatmai](../../../includes/sskatmai_md.md)] o una versión posterior|  
|-------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------|  
|tipo definido por el usuario mayor que 8 KB|LONGVARBINARY (-4)|VARBINARY (-3)|  
|geography|LONGVARBINARY (-4)|VARBINARY (-3)|  
|geometry|LONGVARBINARY (-4)|VARBINARY (-3)|  
|varbinary(max)|LONGVARBINARY (-4)|VARBINARY (-3)|  
|nvarchar(max)|LONGVARCHAR (-1) o LONGNVARCHAR (JDBC 4) (-16)|VARCHAR (12) o NVARCHAR (JDBC 4) (-9)|  
|ntext|LONGVARCHAR (-1)|VARCHAR (12)|  
|time|VARCHAR (12) o NVARCHAR (JDBC 4) (-9)|TIME (-154)|  
|Date|VARCHAR (12) o NVARCHAR (JDBC 4) (-9)|DATE (91)|  
|datetime2|VARCHAR (12) o NVARCHAR (JDBC 4) (-9)|TIMESTAMP (93)|  
|datetimeoffset|VARCHAR (12) o NVARCHAR (JDBC 4) (-9)|microsoft.sql.Types.DATETIMEOFFSET  (-155)|  
  
 La columna COLUMN_SIZE tiene los siguientes cambios:  
  
|Tipo de datos [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]|Tipo devuelto en el controlador JDBC 2.0|Tipo devuelto en el controlador JDBC 3.0|  
|-------------------------------------------------------------------|------------------------------------|------------------------------------|  
|nvarchar(max)|1073741823|2147483647 (metadatos de base de datos)|  
|xml|1073741823|2147483647 (metadatos de base de datos)|  
|tipo definido por el usuario menor o igual que 8 KB|8 KB (conjunto de resultados y metadatos de parámetro)|Tamaño real que devuelve el procedimiento almacenado.|  
|time||La longitud en caracteres de la representación de cadena del tipo (suponiendo la precisión máxima permitida del componente de fracciones de segundo).|  
|Date||igual que time|  
|datetime2||igual que time|  
|datetimeoffset||igual que time|  
  
 La columna BUFFER_LENGTH tiene el siguiente cambio:  
  
|Tipo de datos [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]|Tipo devuelto en el controlador JDBC 2.0|Tipo devuelto en el controlador JDBC 3.0|  
|-------------------------------------------------------------------|------------------------------------|------------------------------------|  
|tipo definido por el usuario mayor que 8 KB||2147483647|  
  
 La columna TYPE_NAME tiene los siguientes cambios:  
  
|Tipo de datos [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]|Tipo devuelto en el controlador JDBC 2.0|Tipo devuelto en el controlador JDBC 3.0|  
|-------------------------------------------------------------------|------------------------------------|------------------------------------|  
|ntext|texto|varchar|  
|varbinary(max)|imagen|varbinary|  
  
 La columna DECIMAL_DIGITS tiene los siguientes cambios:  
  
|Tipo de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]|Controlador JDBC 2.0|Controlador JDBC 3.0|  
|--------------------------------------------------------------|---------------------|---------------------|  
|time|null|7 (o menor si se especifica)|  
|Date|null|null|  
|datetime2|null|7 (o menor si se especifica)|  
|datetimeoffset|null|7 (o menor si se especifica)|  
  
 La columna SQL_DATA_TYPE tiene los siguientes cambios:  
  
|Tipo de datos [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]|Valor de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 2008 en el controlador JDBC 2.0|Valor de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 2008 en el controlador JDBC 3.0|  
|-------------------------------------------------------------------|--------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------|  
|ntext|-10|-9|  
|nvarchar(max)|-1|-9|  
|xml|-10|-152|  
|tipo definido por el usuario menor o igual que 8 KB|-3|-151|  
|tipo definido por el usuario mayor que 8 KB|No está disponible en el controlador JDBC 2.0|-151|  
|geography|-4|-151|  
|geometry|-4|-151|  
|hierarchyid|-4|-151|  
|time|-9|92|  
|Date|-9|91|  
|datetime2|-9|93|  
|datetimeoffset|-9|-155|  
  
## <a name="example"></a>Ejemplo  
 En el siguiente ejemplo se muestra cómo usar el método getColumns para devolver información para la tabla Person.Contact en la base de datos de ejemplo [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)].  
  
```  
import java.sql.*;  
public class c1 {  
   public static void main(String[] args) {  
      String connectionUrl = "jdbc:sqlserver://localhost:1433;databaseName=AdventureWorks;integratedsecurity=true";  
  
      Connection con = null;  
      Statement stmt = null;  
      ResultSet rs = null;  
  
      try {  
         Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");  
         con = DriverManager.getConnection(connectionUrl);  
         DatabaseMetaData dbmd = con.getMetaData();  
         rs = dbmd.getColumns("AdventureWorks", "Person", "Contact", "FirstName");  
  
         ResultSet r = dbmd.getColumns(null, null, "Contact", null);  
         ResultSetMetaData rm = r.getMetaData();   
         int noofcols = rm.getColumnCount();  
  
         if (r.next())  
            for (int i = 0 ; i < noofcols ; i++ )  
            System.out.println(rm.getColumnName( i + 1 ) + ": \t\t" + r.getString( i + 1 ));  
      }  
  
      catch (Exception e) {}  
      finally {}  
   }  
}  
```  
  
## <a name="see-also"></a>Ver también  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Miembros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Clase SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
