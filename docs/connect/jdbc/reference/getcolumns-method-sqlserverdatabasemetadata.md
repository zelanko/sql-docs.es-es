---
title: Método getColumns (SQLServerDatabaseMetaData) | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
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
ms.workload: Inactive
ms.openlocfilehash: 7d6b0df43a82b288f475c1325c66670cf6290933
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
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
  
 A **cadena** que contiene el nombre del catálogo.  
  
 *schema*  
  
 A **cadena** que contiene el patrón de nombre de esquema.  
  
 *table*  
  
 A **cadena** que contiene el patrón de nombre de tabla.  
  
 *Col.*  
  
 A **cadena** que contiene el patrón de nombre de columna.  
  
## <a name="return-value"></a>Valor devuelto  
 A [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método getColumns es especificado por el método getColumns en la interfaz java.sql.DatabaseMetaData.  
  
 El conjunto de resultados devuelto por el método getColumns contendrá la siguiente información:  
  
|Nombre|Tipo|Description|  
|----------|----------|-----------------|  
|TABLE_CAT|**String**|Nombre del catálogo.|  
|TABLE_SCHEM|**String**|El nombre de esquema de la tabla.|  
|TABLE_NAME|**String**|El nombre de la tabla.|  
|COLUMN_NAME|**String**|Nombre de columna.|  
|DATA_TYPE|**smallint**|Tipo de datos SQL de java.sql.Types.|  
|TYPE_NAME|**String**|El nombre del tipo de datos.|  
|COLUMN_SIZE|**int**|La precisión de la columna.|  
|BUFFER_LENGTH|**smallint**|Tamaño de transferencia de los datos.|  
|DECIMAL_DIGITS|**smallint**|La escala de la columna.|  
|NUM_PREC_RADIX|**smallint**|Base de la columna.|  
|NULLABLE|**smallint**|Indica si la columna admite valores NULL. Puede ser uno de los siguientes valores:<br /><br /> columnNoNulls (0)<br /><br /> columnNullable (1)|  
|REMARKS|**String**|Comentarios asociados con la columna.<br /><br /> **Nota:** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] siempre devuelve null para esta columna.|  
|COLUMN_DEF|**String**|El valor predeterminado de la columna.|  
|SQL_DATA_TYPE|**smallint**|Valor del tipo de datos SQL tal como aparece en el campo TYPE del descriptor. Esta columna es igual que la columna DATA_TYPE, salvo por los tipos de datos datetime e interval de SQL-92. Esta columna siempre devuelve un valor.|  
|SQL_DATETIME_SUB|**smallint**|Código de subtipo para los tipos de datos interval de SQL-92 y datetime. Para otros tipos de datos, esta columna devuelve NULL.|  
|CHAR_OCTET_LENGTH|**int**|Número máximo de bytes en la columna.|  
|ORDINAL_POSITION|**int**|Índice de la columna en la tabla.|  
|IS_NULLABLE|**String**|Indica si la columna admite valores NULL.|  
|SS_IS_SPARSE|**smallint**|Si la columna es una columna dispersa, esto tiene el valor 1; en caso contrario, es 0. <sup>1</sup>|  
|SS_IS_COLUMN_SET|**smallint**|Si la columna es la columna column_set dispersa, esto tiene el valor 1; de lo contrario, 0. <sup>1</sup>|  
|SS_IS_COMPUTED|**smallint**|Indica si una columna en un TABLE_TYPE es una columna calculada. <sup>1</sup>|  
|IS_AUTOINCREMENT|**String**|Es "SÍ" si la columna se incrementa automáticamente. Es "NO" si la columna no se incrementa automáticamente. Es "" (cadena vacía) si el controlador no puede determinar si la columna se incrementa automáticamente. <sup>1</sup>|  
|SS_UDT_CATALOG_NAME|**String**|Nombre del catálogo que contiene el tipo definido por el usuario (UDT). <sup>1</sup>|  
|SS_UDT_SCHEMA_NAME|**String**|Nombre del esquema que contiene el tipo definido por el usuario (UDT). <sup>1</sup>|  
|SS_UDT_ASSEMBLY_TYPE_NAME|**String**|Tipo definido por el usuario (UDT) del nombre completo. <sup>1</sup>|  
|SS_XML_SCHEMACOLLECTION_CATALOG_NAME|**String**|Nombre del catálogo donde se define el nombre de una colección de esquemas XML. Si no se encuentra el nombre del catálogo, esta variable contiene una cadena vacía. <sup>1</sup>|  
|SS_XML_SCHEMACOLLECTION_SCHEMA_NAME|**String**|Nombre del esquema donde se define el nombre de una colección de esquemas XML. Si no se puede encontrar el nombre de esquema, esta cadena estará vacía. <sup>1</sup>|  
|SS_XML_SCHEMACOLLECTION_NAME|**String**|Nombre de una colección de esquemas XML. Si no se puede encontrar el nombre, esta cadena estará vacía. <sup>1</sup>|  
|SS_DATA_TYPE|**tinyint**|El [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] tipo de datos que utiliza los procedimientos almacenados extendidos.<br /><br /> **Tenga en cuenta** para obtener más información acerca de los tipos de datos devueltos por [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)], vea "Tipos de datos (Transact-SQL)" en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] libros en pantalla.|  
  
 (1) esta columna no estará disponible si se está conectando a [!INCLUDE[ssVersion2005](../../../includes/ssversion2005_md.md)].  
  
> [!NOTE]  
>  Para obtener más información acerca de los datos devueltos por el método getColumns, vea "sp_columns (Transact-SQL)" en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] libros en pantalla.  
  
 En el [!INCLUDE[msCoName](../../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] controlador JDBC 3.0, verá el siguiente comportamiento cambia respecto a versiones anteriores del controlador JDBC:  
  
 La columna DATA_TYPE tiene los cambios siguientes:  
  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Tipo de datos|Tipo devuelto en el controlador JDBC 2.0 (o si está conectado a [!INCLUDE[ssVersion2005](../../../includes/ssversion2005_md.md)]) y constante numérica asociada|Tipo de valor devuelto en el controlador JDBC 3.0 cuando se conecta a [!INCLUDE[ssKatmai](../../../includes/sskatmai_md.md)] o posterior|  
|-------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------|  
|tipo definido por el usuario mayor que 8 KB|LONGVARBINARY (-4)|VARBINARY (-3)|  
|geography|LONGVARBINARY (-4)|VARBINARY (-3)|  
|geometry|LONGVARBINARY (-4)|VARBINARY (-3)|  
|varbinary(max)|LONGVARBINARY (-4)|VARBINARY (-3)|  
|nvarchar(max)|LONGVARCHAR (-1) o LONGNVARCHAR (JDBC 4) (-16)|VARCHAR (12) o NVARCHAR (JDBC 4) (-9)|  
|ntext|LONGVARCHAR (-1)|VARCHAR (12)|  
|time|VARCHAR (12) o NVARCHAR (JDBC 4) (-9)|TIME (-154)|  
|date|VARCHAR (12) o NVARCHAR (JDBC 4) (-9)|DATE (91)|  
|datetime2|VARCHAR (12) o NVARCHAR (JDBC 4) (-9)|TIMESTAMP (93)|  
|datetimeoffset|VARCHAR (12) o NVARCHAR (JDBC 4) (-9)|microsoft.sql.Types.DATETIMEOFFSET  (-155)|  
  
 La columna COLUMN_SIZE tiene los siguientes cambios:  
  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Tipo de datos|Tipo devuelto en el controlador JDBC 2.0|Tipo devuelto en el controlador JDBC 3.0|  
|-------------------------------------------------------------------|------------------------------------|------------------------------------|  
|nvarchar(max)|1073741823|2147483647 (metadatos de base de datos)|  
|xml|1073741823|2147483647 (metadatos de base de datos)|  
|tipo definido por el usuario menor o igual que 8 KB|8 KB (conjunto de resultados y metadatos de parámetro)|Tamaño real que devuelve el procedimiento almacenado.|  
|time||La longitud en caracteres de la representación de cadena del tipo (suponiendo la precisión máxima permitida del componente de fracciones de segundo).|  
|date||igual que time|  
|datetime2||igual que time|  
|datetimeoffset||igual que time|  
  
 La columna BUFFER_LENGTH tiene el siguiente cambio:  
  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Tipo de datos|Tipo devuelto en el controlador JDBC 2.0|Tipo devuelto en el controlador JDBC 3.0|  
|-------------------------------------------------------------------|------------------------------------|------------------------------------|  
|tipo definido por el usuario mayor que 8 KB||2147483647|  
  
 La columna TYPE_NAME tiene los siguientes cambios:  
  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Tipo de datos|Tipo devuelto en el controlador JDBC 2.0|Tipo devuelto en el controlador JDBC 3.0|  
|-------------------------------------------------------------------|------------------------------------|------------------------------------|  
|ntext|texto|varchar|  
|varbinary(max)|imagen|varbinary|  
  
 La columna DECIMAL_DIGITS tiene los siguientes cambios:  
  
|Tipo de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]|Controlador JDBC 2.0|Controlador JDBC 3.0|  
|--------------------------------------------------------------|---------------------|---------------------|  
|time|null|7 (o menor si se especifica)|  
|date|null|null|  
|datetime2|null|7 (o menor si se especifica)|  
|datetimeoffset|null|7 (o menor si se especifica)|  
  
 La columna SQL_DATA_TYPE tiene los siguientes cambios:  
  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Tipo de datos|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Valor de datos de 2008 en el controlador JDBC 2.0|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Valor de datos de 2008 en el controlador JDBC 3.0|  
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
|date|-9|91|  
|datetime2|-9|93|  
|datetimeoffset|-9|-155|  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se muestra cómo utilizar el método getColumns para devolver información de la tabla Person.Contact en la [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] base de datos de ejemplo.  
  
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
  
## <a name="see-also"></a>Vea también  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Miembros de SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Clase SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
