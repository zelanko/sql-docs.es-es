---
title: "Creación de instancias de datos XML | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: xml
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 1fd7895dae9dd1e1008c848b471cf02b0b53953a
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2018
---
# <a name="create-instances-of-xml-data"></a>Crear instancias de datos XML
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
En este tema se describe cómo generar las instancias XML.  
  
 En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], podrá generar instancias XML de las formas siguientes:  
  
-   Instancias de cadenas de conversión de tipo.  
  
-   Usar la instrucción SELECT con la cláusula FOR XML.  
  
-   Usar asignaciones de constantes.  
  
-   Usar la carga masiva.  
  
## <a name="type-casting-string-and-binary-instances"></a>Instancias de cadenas de conversión de tipo e instancias binarias  
 Se puede analizar cualquier tipo de datos de cadena de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , como [**n**][**var**]**char**, **[n]text**, **varbinary**e **image**, en el tipo de datos **xml** convirtiendo (a través de CAST o CONVERT) la cadena al tipo de datos **xml** . Se comprueba el XML sin tipo para confirmar que su formato es correcto. Si hay un esquema asociado al tipo **xml** , también se realiza una validación. Para obtener más información, vea [Comparar XML con tipo y XML sin tipo](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md).  
  
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
 Si un tipo definido por el usuario CLR tiene una serialización XML, las instancias de dicho tipo pueden convertirse explícitamente a un tipo de datos XML. Para obtener más información sobre la serialización XML de un tipo de datos definido por el usuario CLR, vea [Serialización XML de objetos de base de datos de CLR](http://msdn.microsoft.com/library/ac84339b-9384-4710-bebc-01607864a344).  
  
### <a name="white-space-handling-in-typed-xml"></a>Control de los espacios en blanco en XML con tipo  
 En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], los espacios en blanco en el contenido de los elementos se consideran no significativos si aparecen en una secuencia de datos de caracteres únicamente de espacios en blanco delimitados por caracteres de marcado, como etiquetas iniciales o finales, y no se crea una entidad para los mismos. Las secciones CDATA se omiten. Este control de los espacios en blanco es distinto de lo que se describe en la especificación XML 1.0 publicada por el World Wide Web Consortium (W3C). Esto se debe a que el analizador de XML de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] solo reconoce un número limitado de subconjuntos de DTD, tal como se define en XML 1.0. Para obtener más información sobre los subconjuntos de DTD limitados que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite, vea [CAST y CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md).  
  
 De forma predeterminada, el analizador de XML descarta los espacios en blanco insignificantes cuando convierte datos de cadena a XML si se da alguna de las condiciones siguientes:  
  
-   El atributo `xml:space` no está definido en un elemento o sus elementos antecesores.  
  
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
  
 Si no se utiliza el parámetro *style* o su valor es 0, no se mantendrán los espacios en blanco insignificantes para la conversión de la instancia DT xml. Para obtener más información sobre cómo usar el operador CONVERT y su parámetro *style* al convertir datos de cadena a instancias DT xml, vea [CAST y CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md).  
  
### <a name="example-cast-a-string-value-to-typed-xml-and-assign-it-to-a-column"></a>Ejemplo: convertir un valor de cadena a xml con tipo y asignarlo a una columna  
 En el ejemplo siguiente se convierte una variable de cadena que contiene un fragmento de XML al tipo de datos **xml** y, a continuación, se almacena en la columna de tipo **xml** :  
  
```  
CREATE TABLE T(c1 int primary key, c2 xml)  
go  
DECLARE  @s varchar(100)  
SET @s = '<Cust><Fname>Andrew</Fname><Lname>Fuller</Lname></Cust>'   
```  
  
 La siguiente operación de inserción se convierte implícitamente de una cadena al tipo **xml** :  
  
```  
INSERT INTO T VALUES (3, @s)   
```  
  
 Se puede convertir la cadena explícitamente con cast() al tipo **xml** :  
  
```  
INSERT INTO T VALUES (3, cast (@s as xml))  
```  
  
 También se puede utilizar convert(), tal como se muestra a continuación:  
  
```  
INSERT INTO T VALUES (3, convert (xml, @s))   
```  
  
### <a name="example-convert-a-string-to-typed-xml-and-assign-it-to-a-variable"></a>Ejemplo: convertir una cadena a xml con tipo y asignarla a una variable  
 En el ejemplo siguiente, se convierte una cadena a tipo **xml** y se asigna a una variable de tipo de datos **xml** :  
  
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
  
 La instrucción SELECT devuelve un fragmento de XML de texto que a continuación se analiza durante la asignación a la variable de tipo de datos **xml** .  
  
 También se puede utilizar la [directiva TYPE](../../relational-databases/xml/type-directive-in-for-xml-queries.md) en la cláusula FOR XML, lo que devuelve directamente un resultado de consulta FOR XML como tipo **xml** :  
  
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
  
 En el ejemplo siguiente, el resultado **xml** con tipo de una consulta FOR XML se inserta en una columna de tipo **xml** :  
  
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
  
 Para obtener más información sobre FOR XML, vea [FOR XML &#40;SQL Server&#41;](../../relational-databases/xml/for-xml-sql-server.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devuelve instancias de tipo de datos **xml** al cliente como resultado de las distintas construcciones del servidor, como consultas FOR XML que utilizan la directiva TYPE, o donde se utiliza el tipo de datos **xml** para devolver XML a partir de parámetros de salida, variables y columnas SQL. En el código de la aplicación cliente, el proveedor ADO.NET solicita que la información de tipos de datos **xml** se envíe en una codificación binaria desde el servidor. No obstante, si se está utilizando FOR XML sin la directiva TYPE, los datos XML se devuelven como un tipo de cadena. En cualquier caso, el proveedor del cliente siempre podrá controlar cualquier formato de tipo XML.  
  
## <a name="using-constant-assignments"></a>Usar asignaciones de constantes  
 Se puede utilizar una constante de cadena cuando se espera una instancia de tipo de datos **xml** . Es lo mismo que una conversión (CAST) implícita de cadena a XML. Por ejemplo:  
  
```  
DECLARE @xmlDoc xml  
SET @xmlDoc = '<Cust><Fname>Andrew</Fname><Lname>Fuller</Lname></Cust>'   
-- Or  
SET @xmlDoc = N'<?xml version="1.0" encoding="ucs-2"?><doc/>'  
```  
  
 En el ejemplo anterior se convierte implícitamente la cadena al tipo de datos **xml** y se asigna a una variable de tipo **xml** .  
  
 En el ejemplo siguiente se inserta una cadena de constante en una columna de tipo **xml** :  
  
```  
CREATE TABLE T(c1 int primary key, c2 xml)  
INSERT INTO T VALUES (3, '<Cust><Fname>Andrew</Fname><Lname>Fuller</Lname></Cust>')   
```  
  
> [!NOTE]  
>  El XML con tipo se valida con el esquema especificado. Para obtener más información, vea [Comparar XML con tipo y XML sin tipo](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md).  
  
## <a name="using-bulk-load"></a>Usar la carga masiva  
 La funcionalidad mejorada [OPENROWSET (Transact-SQL)](../../t-sql/functions/openrowset-transact-sql.md) permite la carga masiva de documentos XML en la base de datos. Se pueden cargar de forma masiva instancias XML desde archivos a columnas de tipo **xml** de la base de datos. Para obtener ejemplos prácticos, vea [Ejemplos de importación y exportación en bloque documentos XML &#40;SQL Server&#41;](../../relational-databases/import-export/examples-of-bulk-import-and-export-of-xml-documents-sql-server.md). Para obtener más información sobre cómo cargar documentos XML, vea [Cargar datos XML](../../relational-databases/xml/load-xml-data.md).  
  
## <a name="in-this-section"></a>En esta sección  
  
|Tema|Description|  
|-----------|-----------------|  
|[Recuperar y consultar datos XML](../../relational-databases/xml/retrieve-and-query-xml-data.md)|Describe las partes de las instancias XML que no se conservan cuando se almacenan en bases de datos.|  
  
## <a name="see-also"></a>Ver también  
 [Comparar XML con tipo y XML sin tipo](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [Métodos de tipo de datos xml](../../t-sql/xml/xml-data-type-methods.md)   
 [Lenguaje de manipulación de datos XML &#40;XML DML&#41;](../../t-sql/xml/xml-data-modification-language-xml-dml.md)   
 [Datos XML &#40;SQL Server&#41;](../../relational-databases/xml/xml-data-sql-server.md)  
  
  
