---
title: Formato XML del lado cliente y de servidor (SQLXML)
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- NESTED mode
- FOR XML clause, formatting
- client-side XML formatting
- server-side XPath
- server-side XML formatting
- AUTO mode
- client-side XPath
ms.assetid: f807ab7a-c5f8-4e61-9b00-23aebfabc47e
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 421c48590098f9dbf4ce075c213fcd1cda720649
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "75247011"
---
# <a name="client-side-vs-server-side-xml-formatting-sqlxml-40"></a>Lado cliente y Aplicación de formato XML en el servidor (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  En este tema se describen las diferencias generales que existen entre la aplicación de formato XML del lado cliente y del lado servidor en SQLXML.  
  
## <a name="multiple-rowset-queries-not-supported-in-client-side-formatting"></a>En el formato del cliente, no se admiten consultas de varios conjuntos de filas  
 Cuando la aplicación de formato XML es del lado cliente, no se admiten consultas que generen varios conjuntos de filas. Supongamos, por ejemplo, que tiene un directorio virtual en el que ha especificado que la aplicación formato se realice del lado cliente. Considere esta plantilla de ejemplo, que tiene dos instrucciones SELECT en un ** \<bloque SQL: query>** :  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <sql:query>  
     SELECT FirstName FROM Person.Contact FOR XML Nested;   
     SELECT LastName FROM Person.Contact FOR XML Nested    
  </sql:query>  
</ROOT>  
```  
  
 Si ejecuta esta plantilla en el código de la aplicación, se devolverá un error, puesto que el formato XML del lado cliente no admite el formato de varios conjuntos de filas. Si especifica las consultas en dos bloques ** \<SQL: query>** independientes, obtendrá los resultados deseados.  
  
## <a name="timestamp-maps-differently-in-client--vs-server-side-formatting"></a>timestamp se asigna de distinto modo cuando la aplicación de formato se realiza en el cliente o en el servidor  
 En el formato XML del servidor, la columna de base de datos de tipo **timestamp** se asigna al tipo XDR de i8 (cuando se especifica la opción XMLDATA en la consulta).  
  
 En el formato XML del lado cliente, la columna de base de datos de tipo **timestamp** se asigna al **URI** o al tipo XDR **bin. base64** (dependiendo de si se especifica la opción Binary Base64 en la consulta). El tipo XDR **bin. base64** es útil si usa las características diagrama y de carga masiva, ya que este tipo se convierte [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en el tipo de **marca** de tiempo. De esta forma, las operaciones de inserción, actualización o eliminación se realizan correctamente.  
  
## <a name="deep-variants-are-used-in-server-side-formatting"></a>En el formato del servidor se usan tipos VARIANT profundos  
 En la aplicación de formato XML en el servidor, se usan los tipos profundos de un tipo VARIANT. Si aplica el formato XML del lado cliente, los datos VARIANT se convierten en una cadena Unicode y no se usan los subtipos de VARIANT.  
  
## <a name="nested-mode-vs-auto-mode"></a>Diferencias entre el modo NESTED y el modo AUTO  
 El modo NESTED de la instrucción FOR XML del lado cliente es similar al modo AUTO de la instrucción FOR XML del servidor, con las siguientes excepciones:  
  
### <a name="when-you-query-views-using-auto-mode-on-the-server-side-the-view-name-is-returned-as-the-element-name-in-the-resulting-xml"></a>Al consultar vistas utilizando el modo AUTO en el servidor, el nombre de la vista se devuelve como el nombre del elemento en el código XML resultante.  
 Por ejemplo, suponga que se crea la vista siguiente en la tabla person. contact de AdventureWorksdatabase:  
  
```  
CREATE VIEW ContactView AS (SELECT ContactID as CID,  
                               FirstName  as FName,  
                               LastName  as LName  
                        FROM Person.Contact)  
```  
  
 La plantilla siguiente especifica una consulta en la vista ContactView y especifica también que la aplicación de formato XML se realice en el servidor:  
  
```  
 <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <sql:query client-side-xml="0">  
    SELECT *  
    FROM   ContactView  
    FOR XML AUTO  
  </sql:query>  
</ROOT>  
```  
  
 Al ejecutar la plantilla, se devuelve el código XML siguiente. (Solo se muestran resultados parciales). Tenga en cuenta que los nombres de elemento son los nombres de las vistas en las que se ejecuta la consulta.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <ContactView CID="1" FName="Gustavo" LName="Achong" />   
  <ContactView CID="2" FName="Catherine" LName="Abel" />   
...  
</ROOT>  
```  
  
 Al especificar el formato XML del lado cliente utilizando el modo NESTED correspondiente, los nombres de la tabla base se devuelven como los nombres de elemento en el código XML resultante. Por ejemplo, la siguiente plantilla revisada ejecuta la misma instrucción SELECT, pero el formato XML se realiza en el lado cliente (es decir, **Client-Side-XML** se establece en true en la plantilla):  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <sql:query client-side-xml="1">  
    SELECT *  
    FROM   ContactView  
    FOR XML NESTED  
  </sql:query>  
</ROOT>  
```  
  
 Al ejecutar esta plantilla, se genera el código XML siguiente. Observe que, en este caso, el nombre del elemento es el nombre de la tabla base.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Person.Contact CID="1" FName="Gustavo" LName="Achong" />   
  <Person.Contact CID="2" FName="Catherine" LName="Abel" />   
...  
</ROOT>  
```  
  
### <a name="when-you-use-auto-mode-of-the-server-side-for-xml-the-table-aliases-specified-in-the-query-are-returned-as-element-names-in-the-resulting-xml"></a>Cuando se utiliza el modo AUTO de la instrucción FOR XML del servidor, los alias de tabla especificados en la consulta se devuelven como nombres de elemento en el código XML resultante.  
 Por ejemplo, fíjese en esta plantilla:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <sql:query client-side-xml="0">  
    SELECT FirstName as fname,  
           LastName as lname  
    FROM   Person.Contact C  
    FOR XML AUTO  
  </sql:query>  
</ROOT>  
```  
  
 Al ejecutar la plantilla, se genera el código XML siguiente:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <C fname="Gustavo" lname="Achong" />   
  <C fname="Catherine" lname="Abel" />   
...  
</ROOT>   
```  
  
 Cuando se utiliza el modo NESTED de la instrucción FOR XML del lado cliente, los nombres de tabla se devuelven como nombres de elemento en el código XML resultante. (No se utilizan los alias de tabla especificados en la consulta). Por ejemplo, considere esta plantilla:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <sql:query client-side-xml="1">  
    SELECT FirstName as fname,  
           LastName as lname  
    FROM   Person.Contact C  
    FOR XML NESTED  
  </sql:query>  
</ROOT>  
```  
  
 Al ejecutar la plantilla, se genera el código XML siguiente:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Person.Contact fname="Gustavo" lname="Achong" />   
  <Person.Contact fname="Catherine" lname="Abel" />   
...  
</ROOT>  
```  
  
### <a name="if-you-have-a-query-that-returns-columns-as-dbobject-queries-you-cannot-use-aliases-for-these-columns"></a>Si tiene una consulta que devuelve las columnas como consultas dbobject, no puede utilizar alias para estas columnas.  
 Por ejemplo, fíjese en la plantilla siguiente, que ejecuta una consulta que devuelve un identificador de empleado y una foto.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
<sql:query client-side-xml="1">  
   SELECT ProductPhotoID, LargePhoto as P  
   FROM   Production.ProductPhoto  
   WHERE  ProductPhotoID=5  
   FOR XML NESTED, elements  
</sql:query>  
</ROOT>  
```  
  
 Al ejecutar esta plantilla, la columna Photo se devuelve como una consulta dbobject. En esta consulta dbobject, `@P` hace referencia a un nombre de columna que no existe.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Production.ProductPhoto>  
    <ProductPhotoID>5</ProductPhotoID>  
    <LargePhoto>dbobject/Production.ProductPhoto[@ProductPhotoID='5']/@P</LargePhoto>  
  </Production.ProductPhoto>  
</ROOT>  
```  
  
 Si el formato XML se realiza en el servidor (**Client-Side-XML = "0"**), puede usar el alias para las columnas que devuelven las consultas dbobject en las que se devuelven los nombres reales de las tablas y columnas (aunque se hayan especificado alias). Por ejemplo, la siguiente plantilla ejecuta una consulta y el formato XML se realiza en el servidor (no se especifica la opción **Client-Side-XML** y la opción **ejecutar en el cliente** no está seleccionada para la raíz virtual). La consulta especifica también el modo AUTO (no el modo NESTED del lado cliente).  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
<sql:query   
   SELECT ProductPhotoID, LargePhoto as P  
   FROM   Production.ProductPhoto  
   WHERE  ProductPhotoID=5  
   FOR XML AUTO, elements  
</sql:query>  
</ROOT>  
```  
  
 Cuando se ejecuta esta plantilla, se devuelve el documento XML siguiente (observe que no se utilizan alias en la consulta dbobject para la columna LargePhoto):  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Production.ProductPhoto>  
    <ProductPhotoID>5</ProductPhotoID>  
    <LargePhoto>dbobject/Production.ProductPhoto[@ProductPhotoID='5']/@LargePhoto</LargePhoto>  
  </Production.ProductPhoto>  
</ROOT>  
```  
  
### <a name="client-side-vs-server-side-xpath"></a>Diferencias entre XPath en el cliente y en el servidor  
 No existen diferencias de funcionamiento entre XPath en el cliente y en el servidor, con las siguientes salvedades:  
  
-   Las conversiones de datos que se aplican al utilizar consultas XPath del lado cliente son diferentes de las que se aplican cuando se utilizan consultas XPath en el servidor. XPath en el cliente utiliza CAST en lugar de CONVERT mode 126.  
  
-   Cuando se especifica **Client-Side-XML = "0"** (false) en una plantilla, se solicita el formato XML del lado servidor. Por lo tanto, no es posible especificar FOR XML NESTED porque el servidor no reconoce la opción NESTED. Esto genera un error. Deben utilizarse los modos AUTO, RAW o EXPLICIT, que el servidor sí que reconoce.  
  
-   Cuando se especifica **Client-Side-XML = "1"** (true) en una plantilla, se solicita el formato XML del lado cliente. En este caso, puede especificarse FOR XML NESTED. Si especifica FOR XML AUTO, el formato XML se produce en el lado servidor, aunque se especifica **Client-Side-XML = "1"** en la plantilla.  
  
## <a name="see-also"></a>Consulte también  
 [Consideraciones de seguridad de FOR XML &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/for-xml-security-considerations-sqlxml-4-0.md)   
 [Formato XML del lado cliente &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml/formatting/client-side-xml-formatting-sqlxml-4-0.md)   
 [Formato XML del lado servidor &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml/formatting/server-side-xml-formatting-sqlxml-4-0.md)  
  
  
