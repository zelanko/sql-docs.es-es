---
title: Empleo de tipos de datos avanzados | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b39461d3-48d6-4048-8300-1a886c00756d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a50bc3e4fae8fe45004374d3dd019a0f65fe544f
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "69027008"
---
# <a name="using-advanced-data-types"></a>Empleo de tipos de datos avanzados

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] usa los tipos de datos avanzados de JDBC para convertir los tipos de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a un formato que el lenguaje de programación Java pueda entender.  
  
## <a name="remarks"></a>Observaciones

En la siguiente tabla se muestran las asignaciones predeterminadas entre los tipos de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] avanzados, JDBC y del lenguaje de programación Java.  
  
|Tipos de SQL Server|Tipos de JDBC (Tipos de java.sql.)|Tipos del lenguaje Java|  
|----------------------|-----------------------------------|-------------------------|  
|varbinary(max)<br /><br /> imagen|LONGVARBINARY|byte[] \(default), Blob, InputStream, String|  
|text<br /><br /> ntext|LONGVARCHAR|String (default), Clob, InputStream|  
|ntext<br /><br /> nvarchar(max)|LONGVARCHAR<br /><br /> LONGNVARCHAR (Java SE 6.0)|String (default), Clob, NClob|  
|Xml|LONGVARCHAR<br /><br /> SQLXML|String (default), InputStream, Clob, byte[], Blob, SQLXML|  
|Udt<sup>1</sup>|VARBINARY|String (default), byte[], InputStream|  
|sqlvariant|SQLVARIANT|Object|  
|geometry<br /><br /> geography|VARBINARY|byte[]|  


<sup>1</sup>[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] admite el envío y recuperación de UDT de CLR como datos binarios, pero no admite la manipulación de metadatos CLR.  
  
Las siguientes secciones proporcionan ejemplos de cómo puede usar el controlador JDBC y los tipos de datos avanzados.  
  
## <a name="blob-and-clob-and-nclob-data-types"></a>Tipos de datos BLOB, CLOB y NCLOB

El controlador JDBC implementa todos los métodos de las interfaces java.sql.Blob, java.sql.Clob y java.sql.NClob.  
  
> [!NOTE]  
> Los valores CLOB se pueden usar con tipos de datos de valores grandes de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] (o versiones posteriores). En concreto, los tipos CLOB se pueden usar con los tipos de datos **varchar(max)** y **nvarchar(max)** , los tipos BLOB se pueden usar con los tipos de datos **varbinary(max)** y los tipos de datos **image** y los tipos NCLOB se pueden usar con **ntext** y **nvarchar(max)** .  

## <a name="large-value-data-types"></a>Tipos de datos de valores grandes

En versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el trabajo con tipos de datos de valores grandes requería un tratamiento especial. Los tipos de datos de gran tamaño son aquellos que superan el tamaño de fila máximo de 8 KB. En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se ha introducido un especificador máximo para los tipos de datos **varchar**, **nvarchar** y **varbinary** a fin de permitir el almacenamiento de valores de hasta 2^31 bytes. Las columnas de tabla y las variables [!INCLUDE[tsql](../../includes/tsql-md.md)] pueden especificar los tipos de datos **varchar(max)** , **nvarchar(max)** o **varbinary(max)** .  

Los escenarios principales en los que se trabaja con tipos de valores grandes implican su recuperación de una base de datos o agregarlos a una base de datos. Las siguientes secciones describen diferentes enfoques para realizar estas tareas.  

### <a name="retrieving-large-value-types-from-a-database"></a>Recuperar tipos de valores grandes de una base de datos

Al recuperar un tipo de datos de valores grandes, que no sean binarios, de una base de datos, como el tipo de datos **varchar(max)** , un planteamiento es leer esos datos como un flujo de caracteres. En el siguiente ejemplo, se usa el método [executeQuery](../../connect/jdbc/reference/executequery-method-sqlserverstatement.md) de la clase [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) para recuperar datos de la base de datos y devolverlos como un conjunto de resultados. Después, se usa el método [getCharacterStream](../../connect/jdbc/reference/getcharacterstream-method-sqlserverresultset.md) de la clase [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) para leer los datos de valores grandes del conjunto de resultados.  

```java
ResultSet rs = stmt.executeQuery("SELECT TOP 1 * FROM Test1");  
rs.next();  
Reader reader = rs.getCharacterStream(2);  
```

> [!NOTE]
> Este mismo enfoque también se puede usar para los tipos de datos **text**, **ntext** y **nvarchar(max)** .  

Al recuperar tipos de datos binarios de valores grandes, de una base de datos, como el tipo de datos **varbinary(max)** , hay varios enfoques que se pueden aplicar. El enfoque más eficaz es leer los datos como un flujo binario, como en el siguiente ejemplo:  

```java
ResultSet rs = stmt.executeQuery("SELECT photo FROM mypics");  
rs.next();  
InputStream is = rs.getBinaryStream(2);  
```

También se puede usar el método [getBytes](../../connect/jdbc/reference/getbytes-method-sqlserverresultset.md) para leer los datos como una matriz de bytes, como en el siguiente ejemplo:  

```java
ResultSet rs = stmt.executeQuery("SELECT photo FROM mypics");  
rs.next();  
byte [] b = rs.getBytes(2);  
```

> [!NOTE]  
> También puede leer los datos como un BLOB. No obstante, este es el método menos eficaz de los dos que se han mostrado anteriormente.  

### <a name="adding-large-value-types-to-a-database"></a>Agregar tipos de valores grandes a una base de datos

La carga de datos grandes con el controlador JDBC funciona bien para los casos en que tienen el tamaño de la memoria y, en los casos en los que son más grandes que la memoria, la transmisión de datos es la opción principal. No obstante, la manera más eficaz de cargar datos grandes es mediante interfaces de transmisión de datos.  

Otra opción es usar un String o bytes, como se puede ver en el siguiente ejemplo:  

```java
PreparedStatement pstmt = con.prepareStatement("INSERT INTO test1 (c1_id, c2_vcmax) VALUES (?, ?)");  
pstmt.setInt(1, 1);  
pstmt.setString(2, htmlStr);  
pstmt.executeUpdate();  
```

> [!NOTE]  
> Este enfoque también se puede utilizar para los valores que están almacenados en columnas **text**, **ntext** y **nvarchar(max)** .  

Si tiene en el servidor una biblioteca de imágenes y debe cargar archivos de imagen binarios completos en una columna **varbinary(max)** , el método más eficaz con JDBC Driver es usar directamente secuencias, como en el siguiente ejemplo:  

```java
try (PreparedStatement pstmt = con.prepareStatement("INSERT INTO test1 (Col1, Col2) VALUES(?,?)")) { 
  File inputFile = new File("CLOBFile20mb.jpg");  
  try (FileInputStream inStream = new FileInputStream(inputFile)) {
    int id = 1;  
    pstmt.setInt(1,id);  
    pstmt.setBinaryStream(2, inStream);  
    pstmt.executeUpdate();
  }
}
```

> [!NOTE]  
> El método CLOB o BLOB no es una forma eficaz de cargar grandes volúmenes de datos.  

### <a name="modifying-large-value-types-in-a-database"></a>Modificar tipos de valores grandes en una base de datos

En la mayoría de los casos, el método recomendado para actualizar o modificar valores grandes de una base de datos consiste en pasar parámetros a través de las clases [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) y [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) mediante comandos de [!INCLUDE[tsql](../../includes/tsql-md.md)] del tipo `UPDATE`, `WRITE` y `SUBSTRING`.  

Si tiene que reemplazar la instancia de una palabra en un archivo grande de texto, como un archivo de almacenamiento HTML, puede usar un objeto Clob, como en el siguiente ejemplo:  

```java
String SQL = "SELECT * FROM test1;";  
try (Statement stmt = con.createStatement(ResultSet.TYPE_SCROLL_SENSITIVE, ResultSet.CONCUR_UPDATABLE)
     ResultSet rs = stmt.executeQuery(SQL)) {
  rs.next();

  Clob clob = rs.getClob(2);  
  long pos = clob.position("dog", 1);  
  clob.setString(pos, "cat");  
  rs.updateClob(2, clob);  
  rs.updateRow();  
}
```

Además, podría hacer el trabajo en el servidor y pasar los parámetros a una instrucción UPDATE preparada.  

Para obtener más información sobre tipos de valores grandes, consulte "Uso de tipos de valores grandes" en los Libros en pantalla de SQL Server.  

## <a name="xml-data-type"></a>Tipo de datos de XML

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proporciona un tipo de datos **xml** que permite almacenar documentos y fragmentos XML en una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El tipo de datos **xml** es un tipo de datos integrado en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y es de algún modo similar a otros tipos integrados, como **int** y **varchar**. Como sucede con otros tipos integrados, puede usar el tipo de datos **xml** como un tipo de columna cuando crea una tabla; como un tipo de variable, de parámetro o de devolución de función; o en funciones CAST y CONVERT de [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
En el controlador JDBC, el tipo de datos **xml** se puede asignar como una cadena, una matriz de bytes, un flujo o un objeto CLOB, BLOB o SQLXML. Cadena es el valor predeterminado. Desde la versión 2.0 del controlador JDBC, este controlador proporciona compatibilidad con la API de JDBC 4.0, que presenta la interfaz SQLXML. La interfaz SQLXML define métodos para interactuar con datos XML y manipularlos. El tipo de datos **SQLXML** se asigna al tipo de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]xml**de**. Para obtener más información sobre cómo leer y escribir datos XML desde y en la base de datos relacional con el tipo de datos de Java **SQLXML**, vea [Compatibilidad con datos XML](../../connect/jdbc/supporting-xml-data.md).  
  
La implementación de los tipos de datos **xml** de JDBC Driver proporciona compatibilidad con lo siguiente:  
  
- Acceso a XML como una cadena UTF-16 estándar de Java para la mayoría de las situaciones comunes de programación.  
  
- Compatibilidad con la escritura de UTF-8 y otros XML codificados de 8 bits.  
  
- Acceso a XML como una matriz de bytes con un BOM inicial, cuando está codificado en UTF-16 para el intercambio con otros procesadores de XML y archivos en discos.  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] requiere un BOM inicial para XML codificado en UTF-16. La aplicación debe proporcionarlo cuando los valores de parámetro XML se proporcionen como matrices de bytes. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] siempre genera los valores XML como cadenas UTF-16 sin BOM ni declaración de codificación incrustada. Cuando se recuperan valores XML como byte[], BinaryStream o Blob, se agrega al principio del valor un BOM de UTF-16.  
  
Para más información sobre los tipos de datos **xml**, vea "Tipos de datos XML" en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="user-defined-data-type"></a>Tipos de datos definidos por el usuario  

La introducción de tipos definidos por el usuario (UDT) en [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] amplía el sistema de tipos de SQL al permitirle almacenar estructuras de datos personalizados y objetos en una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Los UDT pueden contener varios tipos de datos y pueden presentar distintos comportamientos, lo que los diferencia de los tipos de datos de alias tradicionales que constan de un único tipo de datos del sistema de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Los UDT se definen con cualquiera de los lenguajes compatibles con Microsoft .NET Common Language Runtime (CLR) que producen código comprobable. Esto incluye Microsoft Visual C# y Visual Basic .NET. Los datos se exponen como campos y propiedades de una clase o una estructura basada en .NET Framework, y los comportamientos se definen con métodos de la clase o la estructura.  
  
En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se pueden usar los UDT como definiciones de columnas de una tabla, como una variable de un lote de [!INCLUDE[tsql](../../includes/tsql-md.md)] o como un argumento de una función o un procedimiento almacenado de [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
Para más información sobre los tipos de datos definidos por el usuario, vea "Usar y modificar instancias de tipos definidos por el usuario" en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="sql_variant-data-type"></a>Tipo de datos Sql_variant

Para obtener información sobre el tipo de datos sql_variant, consulte [Uso del tipo de datos Sql_variant](../../connect/jdbc/using-sql-variant-datatype.md).  

## <a name="spatial-data-types"></a>Tipos de datos espaciales

Para obtener información sobre los tipos de datos espaciales, consulte [Empleo de tipos de datos espaciales](../../connect/jdbc/use-spatial-datatypes.md).  

## <a name="see-also"></a>Consulte también

[Descripción de los tipos de datos del controlador JDBC](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
