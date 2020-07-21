---
title: Creación de instancias de datos XML | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- type casting string instances [XML in SQL Server]
- XML [SQL Server], typed
- xml data type [SQL Server], generating instances
- casting string instances [XML in SQL Server]
- typed XML
- generating XML instances [SQL Server]
- XML [SQL Server], generating instances
- white space [XML in SQL Server]
ms.assetid: dbd6c06f-db6e-44a7-855a-6a55bf374907
author: rothja
ms.author: jroth
ms.openlocfilehash: c857b9ebbe559de34fdac925642f9270d9cbf936
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85059512"
---
# <a name="create-instances-of-xml-data"></a>Crear instancias de datos XML
  En este tema se describe cómo generar las instancias XML.  
  
 En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], podrá generar instancias XML de las formas siguientes:  
  
-   Instancias de cadenas de conversión de tipo.  
  
-   Usar la instrucción SELECT con la cláusula FOR XML.  
  
-   Usar asignaciones de constantes.  
  
-   Usar la carga masiva.  
  
## <a name="type-casting-string-and-binary-instances"></a>Instancias de cadenas de conversión de tipo e instancias binarias  
 Puede analizar cualquiera de los [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de datos de cadena, como [**n**] [**var**]**Char**, **[n] Text**, **varbinary**e **Image**, en el `xml` tipo de datos mediante la conversión (conversión) o la conversión (conversión) de la cadena en el `xml` tipo de datos. Se comprueba el XML sin tipo para confirmar que su formato es correcto. Si hay un esquema asociado al `xml` tipo, también se realiza la validación. Para obtener más información, vea [Comparar XML con tipo y XML sin tipo](compare-typed-xml-to-untyped-xml.md).  
  
 Los documentos XML pueden codificarse con distintas codificaciones (por ejemplo, UTF-8, UTF-16, windows-1252). A continuación se describen de forma resumida las reglas que establecen el modo en que los tipos de origen de cadena y binarios interactúan con la codificación del documento XML y cómo se comporta el analizador.  
  
 Puesto que **nvarchar** asume una codificación Unicode de dos bytes como UTF-16 o UCS-2, el analizador de XML tratará el valor de cadena como un documento o fragmento XML codificado con Unicode de dos bytes. Esto significa que el documento XML también debe codificarse con codificación Unicode de dos bytes para que sea compatible con el tipo de datos de origen. Un documento XML con codificación UTF-16 puede tener una marca de orden de bytes (BOM) UTF-16, pero no es necesario que la tenga ya que el contexto del tipo de origen indica claramente que solo puede tratarse de un documento con codificación Unicode de dos bytes.  
  
 El analizador de XML trata el contenido de una cadena **varchar** como un documento o fragmento XML con codificación de un byte. Puesto que la cadena de origen **varchar** tiene una página de códigos asociada, el analizador utilizará dicha página de códigos para la codificación si no se especifica ninguna codificación explícita en el XML. Si una instancia de XML tiene una marca BOM o una declaración de codificación, éstas deben ser coherentes con la página de códigos, de lo contrario el analizador notificará un error.  
  
 El contenido de **varbinary** se trata como un flujo de puntos de código que se pasa directamente al analizador de XML. Por consiguiente, el documento o fragmento XML debe proporcionar la marca BOM u otro tipo de información de codificación insertada. Para determinar la codificación, el analizador solo consultará el flujo. Esto significa que el XML con codificación UTF-16 debe proporcionar la marca BOM UTF-16 y que una instancia sin marca BOM y sin una codificación de declaración se interpretará como UTF-8.  
  
 Si la codificación del documento XML no se conoce de antemano y los datos se pasan como datos de cadena o datos binarios en lugar de pasarse como datos XML antes de realizar su conversión a XML, es recomendable tratar los datos como **varbinary**. Por ejemplo, si se leen datos de un archivo XML usando OpenRowset(), es necesario especificar los datos que deben leerse como un valor **varbinary(max)** :  
  
```  
select CAST(x as XML)   
from OpenRowset(BULK 'filename.xml', SINGLE_BLOB) R(x)  
```  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] representa internamente XML en una representación binaria eficaz que usa la codificación UTF-16. La codificación proporcionada por el usuario no se mantiene, pero se tiene en cuenta durante el proceso de análisis.  
  
### <a name="type-casting-clr-user-defined-types"></a>Conversión de tipos definidos por el usuario CLR  
 Si un tipo definido por el usuario CLR tiene una serialización XML, las instancias de dicho tipo pueden convertirse explícitamente a un tipo de datos XML. Para obtener más información sobre la serialización XML de un tipo de datos definido por el usuario CLR, vea [Serialización XML de objetos de base de datos de CLR](../../database-engine/dev-guide/xml-serialization-from-clr-database-objects.md).  
  
### <a name="white-space-handling-in-typed-xml"></a>Control de los espacios en blanco en XML con tipo  
 En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], los espacios en blanco en el contenido de los elementos se consideran no significativos si aparecen en una secuencia de datos de caracteres únicamente de espacios en blanco delimitados por caracteres de marcado, como etiquetas iniciales o finales, y no se crea una entidad para los mismos. Las secciones CDATA se omiten. Este control de los espacios en blanco es distinto de lo que se describe en la especificación XML 1.0 publicada por el World Wide Web Consortium (W3C). Esto se debe a que el analizador de XML de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] solo reconoce un número limitado de subconjuntos de DTD, tal como se define en XML 1.0. Para obtener más información sobre los subconjuntos de DTD limitados que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite, vea [CAST y CONVERT &#40;Transact-SQL&#41;](/sql/t-sql/functions/cast-and-convert-transact-sql).  
  
 De forma predeterminada, el analizador de XML descarta los espacios en blanco insignificantes cuando convierte datos de cadena a XML si se da alguna de las condiciones siguientes:  
  
-   `The xml:space` en un elemento o en sus elementos antecesores.  
  
-   El atributo `xml:space` activo en un elemento, o uno de sus elementos antecesores, tiene el valor predeterminado.  
  
 Por ejemplo:  
  
```  
declare @x xml  
set @x = '<root>      <child/>     </root>'  
select @x   
```  
  
 El resultado es el siguiente:  
  
```  
<root><child/></root>  
```  
  
 No obstante, puede cambiar este comportamiento. Para mantener los espacios en blanco de una instancia DT xml, utilice el operador CONVERT y su parámetro *style* opcional establecido en el valor 1. Por ejemplo:  
  
```  
SELECT CONVERT(xml, N'<root>      <child/>     </root>', 1)  
```  
  
 Si no se utiliza el parámetro *style* o su valor es 0, no se mantendrán los espacios en blanco insignificantes para la conversión de la instancia DT xml. Para obtener más información sobre cómo usar el operador CONVERT y su parámetro *style* al convertir datos de cadena a instancias DT xml, vea [CAST y CONVERT &#40;Transact-SQL&#41;](/sql/t-sql/functions/cast-and-convert-transact-sql).  
  
### <a name="example-cast-a-string-value-to-typed-xml-and-assign-it-to-a-column"></a>Ejemplo: convertir un valor de cadena a xml con tipo y asignarlo a una columna  
 En el ejemplo siguiente se convierte una variable de cadena que contiene un fragmento XML en el `xml` tipo de datos y, a continuación, se almacena en la `xml` columna de tipo:  
  
```  
CREATE TABLE T(c1 int primary key, c2 xml)  
go  
DECLARE  @s varchar(100)  
SET @s = '<Cust><Fname>Andrew</Fname><Lname>Fuller</Lname></Cust>'   
```  
  
 La siguiente operación de inserción convierte implícitamente de una cadena al `xml` tipo:  
  
```  
INSERT INTO T VALUES (3, @s)   
```  
  
 Puede convertir explícitamente () la cadena al `xml` tipo:  
  
```  
INSERT INTO T VALUES (3, cast (@s as xml))  
```  
  
 También se puede utilizar convert(), tal como se muestra a continuación:  
  
```  
INSERT INTO T VALUES (3, convert (xml, @s))   
```  
  
### <a name="example-convert-a-string-to-typed-xml-and-assign-it-to-a-variable"></a>Ejemplo: convertir una cadena a xml con tipo y asignarla a una variable  
 En el ejemplo siguiente, una cadena se convierte al `xml` tipo y se asigna a una variable del `xml` tipo de datos:  
  
```  
declare @x xml  
declare  @s varchar(100)  
SET @s = '<Cust><Fname>Andrew</Fname><Lname>Fuller</Lname></Cust>'   
set @x =convert (xml, @s)  
select @x  
```  
  
## <a name="using-the-select-statement-with-a-for-xml-clause"></a>Usar la instrucción SELECT con la cláusula FOR XML  
 Se puede utilizar la cláusula FOR XML en una instrucción SELECT para devolver resultados como XML. Por ejemplo:  
  
```  
DECLARE @xmlDoc xml  
SET @xmlDoc = (SELECT Column1, Column2  
               FROM   Table1, Table2  
               WHERE   Some condition  
               FOR XML AUTO)  
 ...  
```  
  
 La instrucción SELECT devuelve un fragmento XML de texto que se analiza durante la asignación a la `xml` variable de tipo de datos.  
  
 También puede utilizar la [Directiva Type](type-directive-in-for-xml-queries.md) en la cláusula for XML que devuelve directamente un resultado de consulta for XML como `xml` tipo:  
  
```  
Declare @xmlDoc xml  
SET @xmlDoc = (SELECT ProductModelID, Name  
               FROM   Production.ProductModel  
               WHERE  ProductModelID=19  
               FOR XML AUTO, TYPE)  
SELECT @xmlDoc  
```  
  
 El resultado es el siguiente:  
  
```  
<Production.ProductModel ProductModelID="19" Name="Mountain-100" />...  
```  
  
 En el ejemplo siguiente, el resultado con tipo `xml` de una consulta for XML se inserta en una `xml` columna de tipo:  
  
```  
CREATE TABLE T1 (c1 int, c2 xml)  
go  
INSERT T1(c1, c2)  
SELECT 1, (SELECT ProductModelID, Name  
           FROM Production.ProductModel  
           WHERE ProductModelID=19  
           FOR XML AUTO, TYPE)  
SELECT * FROM T1  
go  
```  
  
 Para obtener más información sobre FOR XML, vea [FOR XML &#40;SQL Server&#41;](for-xml-sql-server.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devuelve instancias de tipo de datos `xml` al cliente como resultado de las distintas construcciones del servidor, como consultas FOR XML que utilizan la directiva TYPE, o donde se utiliza el tipo de datos `xml` para devolver XML a partir de parámetros de salida, variables y columnas SQL. En el código de la aplicación cliente, el proveedor ADO.NET solicita que la información de tipos de datos `xml` se envíe en una codificación binaria desde el servidor. No obstante, si se está utilizando FOR XML sin la directiva TYPE, los datos XML se devuelven como un tipo de cadena. En cualquier caso, el proveedor del cliente siempre podrá controlar cualquier formato de tipo XML.  
  
## <a name="using-constant-assignments"></a>Usar asignaciones de constantes  
 Se puede utilizar una constante de cadena cuando se espera una instancia del `xml` tipo de datos. Es lo mismo que una conversión (CAST) implícita de cadena a XML. Por ejemplo:  
  
```  
DECLARE @xmlDoc xml  
SET @xmlDoc = '<Cust><Fname>Andrew</Fname><Lname>Fuller</Lname></Cust>'   
-- Or  
SET @xmlDoc = N'<?xml version="1.0" encoding="ucs-2"?><doc/>'  
```  
  
 En el ejemplo anterior se convierte implícitamente la cadena al `xml` tipo de datos y se asigna a una `xml` variable de tipo.  
  
 En el ejemplo siguiente se inserta una cadena de constante en una `xml` columna de tipo:  
  
```  
CREATE TABLE T(c1 int primary key, c2 xml)  
INSERT INTO T VALUES (3, '<Cust><Fname>Andrew</Fname><Lname>Fuller</Lname></Cust>')   
```  
  
> [!NOTE]  
>  El XML con tipo se valida con el esquema especificado. Para obtener más información, vea [Comparar XML con tipo y XML sin tipo](compare-typed-xml-to-untyped-xml.md).  
  
## <a name="using-bulk-load"></a>Usar la carga masiva  
 La funcionalidad mejorada [OPENROWSET (Transact-SQL)](/sql/t-sql/functions/openrowset-transact-sql) permite la carga masiva de documentos XML en la base de datos. Puede cargar de forma masiva instancias XML desde archivos en las `xml` columnas de tipo de la base de datos. Para obtener ejemplos prácticos, vea [Ejemplos de importación y exportación en bloque documentos XML &#40;SQL Server&#41;](../import-export/examples-of-bulk-import-and-export-of-xml-documents-sql-server.md). Para obtener más información sobre cómo cargar documentos XML, vea [Cargar datos XML](load-xml-data.md).  
  
## <a name="in-this-section"></a>En esta sección  
  
|Tema|Descripción|  
|-----------|-----------------|  
|[Recuperar y consultar datos XML](retrieve-and-query-xml-data.md)|Describe las partes de las instancias XML que no se conservan cuando se almacenan en bases de datos.|  
  
## <a name="see-also"></a>Consulte también  
 [Comparar XML con tipo y XML sin tipo](compare-typed-xml-to-untyped-xml.md)   
 [métodos del tipo de datos xml](/sql/t-sql/xml/xml-data-type-methods)   
 [Lenguaje de manipulación de datos XML &#40;XML DML&#41;](/sql/t-sql/xml/xml-data-modification-language-xml-dml)   
 [Datos XML &#40;SQL Server&#41;](xml-data-sql-server.md)  
  
  
