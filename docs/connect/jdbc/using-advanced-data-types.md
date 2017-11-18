---
title: Uso de tipos de datos avanzados | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b39461d3-48d6-4048-8300-1a886c00756d
caps.latest.revision: 58
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b74ed587d91e351f91db2e3ef2a45c41edf37918
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="using-advanced-data-types"></a>Usar tipos de datos avanzados
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  El [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] usa los tipos de datos avanzados de JDBC para convertir el [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tipos de datos a un formato que pueda entender el Java de lenguaje de programación.  
  
## <a name="remarks"></a>Comentarios  
 En la tabla siguiente se enumera las asignaciones predeterminadas entre los avanzados [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], JDBC y los tipos de datos de lenguaje de programación Java.  
  
|Tipos de SQL Server|Tipos de JDBC (Tipos de java.sql.)|Tipos del lenguaje Java|  
|----------------------|-----------------------------------|-------------------------|  
|varbinary(max)<br /><br /> imagen|LONGVARBINARY|Byte [] \(predeterminado), Blob, InputStream, cadena|  
|texto<br /><br /> varchar(max)|LONGVARCHAR|String (default), Clob, InputStream|  
|ntext<br /><br /> nvarchar(max)|LONGVARCHAR<br /><br /> LONGNVARCHAR (Java SE 6.0)|String (default), Clob, NClob (Java SE 6.0)|  
|xml|LONGVARCHAR<br /><br /> SQLXML (Java SE 6.0)|String (default), InputStream, Clob, byte[],Blob, SQLXML (Java SE 6.0)|  
|UDT<sup>1</sup>|VARBINARY|String (default), byte[], InputStream|  
  
 <sup>1</sup> la [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] admite el envío y recuperación de UDT de CLR como datos binarios, pero no se admite la manipulación de metadatos CLR.  
  
 Las siguientes secciones proporcionan ejemplos de cómo puede usar el controlador JDBC y los tipos de datos avanzados.  
  
## <a name="blob-and-clob-and-nclob-data-types"></a>Tipos de datos BLOB, CLOB y NCLOB  
 El controlador JDBC implementa todos los métodos de las interfaces java.sql.Blob, java.sql.Clob y java.sql.NClob.  
  
> [!NOTE]  
>  Valores CLOB se pueden usar con [!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)] (o posterior) tipos de datos de valor grande. En concreto, los tipos CLOB se pueden usar con la **varchar (max)** y **nvarchar (max)** tipos de datos, tipos BLOB pueden usarse con **varbinary (max)** y **imagen**  tipos de datos y los tipos NCLOB pueden utilizarse con **ntext** y **nvarchar (max)**.  
  
## <a name="large-value-data-types"></a>Tipos de datos de valores grandes  
 En versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], trabajar con datos de valores grandes tipos requería un tratamiento especial. Los tipos de datos de gran tamaño son aquellos que superan el tamaño de fila máximo de 8 KB. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]Introduce un especificador de máximo para **varchar**, **nvarchar**, y **varbinary** tipos de datos para permitir el almacenamiento de valores tan grandes como 2 ^ 31 bytes. Columnas de la tabla y [!INCLUDE[tsql](../../includes/tsql_md.md)] pueden especificar variables **varchar (max)**, **nvarchar (max)**, o **varbinary (max)** tipos de datos.  
  
 Los escenarios principales en los que se trabaja con tipos de valores grandes implican su recuperación de una base de datos o agregarlos a una base de datos. Las siguientes secciones describen diferentes enfoques para realizar estas tareas.  
  
### <a name="retrieving-large-value-types-from-a-database"></a>Recuperar tipos de valores grandes de una base de datos  
 Cuando se recupera un tipo de datos de valores grandes no binarios, como el **varchar (max)** tipo de datos, desde una base de datos, un enfoque consiste en leer esos datos como una secuencia de caracteres. En el ejemplo siguiente, la [executeQuery](../../connect/jdbc/reference/executequery-method-sqlserverstatement.md) método de la [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) clase se utiliza para recuperar datos de la base de datos y devolverlos como un conjunto de resultados. La [getCharacterStream](../../connect/jdbc/reference/getcharacterstream-method-sqlserverresultset.md) método de la [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) clase se utiliza para leer los datos de valores grandes desde el conjunto de resultados.  
  
```  
ResultSet rs = stmt.executeQuery("SELECT TOP 1 * FROM Test1");  
rs.next();  
Reader reader = rs.getCharacterStream(2);  
```  
  
> [!NOTE]  
>  Este mismo enfoque también se puede utilizar para la **texto**, **ntext**, y **nvarchar (max)** tipos de datos.  
  
 Cuando se recupera un tipo de datos binarios de gran valor, como el **varbinary (max)** tipo de datos, desde una base de datos, hay varios enfoques que puede realizar. El enfoque más eficaz es leer los datos como un flujo binario, como en el siguiente ejemplo:  
  
```  
ResultSet rs = stmt.executeQuery("SELECT photo FROM mypics");  
rs.next();  
InputStream is = rs.getBinaryStream(2);  
```  
  
 También puede usar el [getBytes](../../connect/jdbc/reference/getbytes-method-sqlserverresultset.md) método para leer los datos como una matriz de bytes, como en el siguiente ejemplo:  
  
```  
ResultSet rs = stmt.executeQuery("SELECT photo FROM mypics");  
rs.next();  
byte [] b = rs.getBytes(2);  
```  
  
> [!NOTE]  
>  También puede leer los datos como un BLOB. No obstante, este es el método menos eficaz de los dos que se han mostrado anteriormente.  
  
### <a name="adding-large-value-types-to-a-database"></a>Agregar tipos de valores grandes a una base de datos  
 La carga de datos grandes con el controlador JDBC funciona bien para los casos en que tienen el tamaño de la memoria y, en los casos en los que son más grandes que la memoria, la transmisión de datos es la opción principal. No obstante, la manera más eficaz de cargar datos grandes es mediante interfaces de transmisión de datos.  
  
 Otra opción es usar un String o bytes, como se puede ver en el siguiente ejemplo:  
  
```  
PreparedStatement pstmt = con.prepareStatement("INSERT INTO test1 (c1_id, c2_vcmax) VALUES (?, ?)");  
pstmt.setInt(1, 1);  
pstmt.setString(2, htmlStr);  
pstmt.executeUpdate();  
```  
  
> [!NOTE]  
>  Este enfoque también puede utilizarse para los valores que se almacenan en **texto**, **ntext**, y **nvarchar (max)** columnas.  
  
 Si tiene una biblioteca de imágenes en el servidor y debe cargar archivos binarios completos para una **varbinary (max)** columna, el método más eficaz con el controlador JDBC es usar directamente secuencias, como en el siguiente ejemplo:  
  
```  
PreparedStatement pstmt = con.prepareStatement("INSERT INTO test1 (Col1, Col2) VALUES(?,?)");  
File inputFile = new File("CLOBFile20mb.jpg");  
FileInputStream inStream = new FileInputStream(inputFile);  
int id = 1;  
pstmt.setInt(1,id);  
pstmt.setBinaryStream(2, inStream);  
pstmt.executeUpdate();  
inStream.close();  
```  
  
> [!NOTE]  
>  El método CLOB o BLOB no es una forma eficaz de cargar grandes volúmenes de datos.  
  
### <a name="modifying-large-value-types-in-a-database"></a>Modificación de tipos de valores grandes en una base de datos  
 En la mayoría de los casos, el método recomendado para actualizar o modificar valores grandes en la base de datos consiste en pasar parámetros a través de la [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) y [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) clases mediante el uso de [!INCLUDE[tsql](../../includes/tsql_md.md)] comandos como UPDATE, WRITE y SUBSTRING.  
  
 Si tiene que reemplazar la instancia de una palabra en un archivo de texto grande, como un archivo de almacenamiento HTML, puede usar un objeto Clob, como en el siguiente ejemplo:  
  
```  
String SQL = "SELECT * FROM test1;";  
Statement stmt = con.createStatement(ResultSet.TYPE_SCROLL_SENSITIVE, ResultSet.CONCUR_UPDATABLE);  
ResultSet rs = stmt.executeQuery(SQL);  
rs.next();  
  
Clob clob = rs.getClob(2);  
long pos = clob.position("dog", 1);  
clob.setString(pos, "cat");  
rs.updateClob(2, clob);  
rs.updateRow();  
```  
  
 Además, podría hacer el trabajo en el servidor y pasar los parámetros a una instrucción UPDATE preparada.  
  
 Para obtener más información sobre tipos de valores grandes, consulte "Uso de tipos de valores grandes" en los Libros en pantalla de SQL Server.  
  
## <a name="xml-data-type"></a>Tipos de datos XML  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]Proporciona un **xml** tipo de datos que le permite almacenar documentos XML y fragmentos en un [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] base de datos. El **xml** tipo de datos es un tipo de datos integrado en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]y es en cierta forma es similar a otros tipos integrados, como **int** y **varchar**. Como con otros tipos integrados, puede usar el **xml** tipo de datos como un tipo de columna cuando crea una tabla, como un tipo de variable, un tipo de parámetro o un tipo de valor devuelto de función; o en [!INCLUDE[tsql](../../includes/tsql_md.md)] funciones CAST y CONVERT.  
  
 En el controlador JDBC, el **xml** se puede asignar el tipo de datos como una cadena, matriz de bytes, secuencia, objeto CLOB, BLOB o SQLXML. Cadena es el valor predeterminado. Desde la versión 2.0 del controlador JDBC, este controlador proporciona compatibilidad con la API de JDBC 4.0, que presenta la interfaz SQLXML. La interfaz SQLXML define métodos para interactuar y manipular datos XML. El **SQLXML** tipo de datos se asigna a la [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **xml** tipo de datos. Para obtener más información acerca de cómo leer y escribir datos XML desde y hacia la base de datos relacional con el **SQLXML** tipo de datos de Java, consulte [compatibilidad con datos XML](../../connect/jdbc/supporting-xml-data.md).  
  
 La implementación de la **xml** tipo de datos en el controlador JDBC proporciona compatibilidad para lo siguiente:  
  
-   Acceso a XML como una cadena UTF-16 estándar de Java para la mayoría de las situaciones comunes de programación.  
  
-   Compatibilidad con la escritura de UTF-8 y otros XML codificados de 8 bits.  
  
-   Acceso a XML como una matriz de bytes con un BOM inicial, cuando está codificado en UTF-16 para el intercambio con otros procesadores de XML y archivos en discos.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]requiere un BOM inicial para XML codificado en UTF-16. La aplicación debe proporcionarlo cuando los valores de parámetro XML se proporcionen como matrices de bytes. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]siempre produce valores XML como UTF-16 cadenas sin BOM o declaración de codificación incrustada. Cuando se recuperan valores XML como byte[], BinaryStream o Blob, se agrega al principio del valor un BOM de UTF-16.  
  
 Para obtener más información sobre la **xml** tipo de datos, vea "tipos de datos xml" en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] libros en pantalla.  
  
## <a name="user-defined-data-type"></a>Tipo de datos definido por el usuario  
 La introducción de tipos definidos por el usuario (UDT) en [!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)] amplía el sistema de tipos SQL al permitirle almacenar objetos y estructuras de datos personalizadas en un [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] base de datos. Los UDT pueden contener varios tipos de datos y pueden presentar distintos comportamientos, lo que los diferencia de los tipos de datos de alias tradicionales que constan de un único tipo de datos del sistema de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Los UDT se definen con cualquiera de los lenguajes compatibles con Microsoft .NET Common Language Runtime (CLR) que producen código comprobable. Esto incluye Microsoft Visual C# y Visual Basic .NET. Los datos se exponen como campos y propiedades de una clase o una estructura basada en .NET Framework, y los comportamientos se definen con métodos de la clase o la estructura.  
  
 En [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], un UDT puede utilizarse como definición de columna de una tabla, como una variable en un [!INCLUDE[tsql](../../includes/tsql_md.md)] lote, o como un argumento de un [!INCLUDE[tsql](../../includes/tsql_md.md)] función o procedimiento almacenado.  
  
 Para obtener más información acerca de los tipos de datos definidos por el usuario, consulte "Usar y modificar instancias de tipos definidos por el usuario" en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] libros en pantalla.  
  
## <a name="see-also"></a>Vea también  
 [Descripción de los tipos de datos del controlador JDBC](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
  
  

