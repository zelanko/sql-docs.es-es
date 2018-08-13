---
title: Diferencias entre XPath en el cliente y Formato XML en el servidor (SQLXML 4.0) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
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
caps.latest.revision: 31
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 8cfab453586c78eed385474cc55237066475c4f6
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/06/2018
ms.locfileid: "39559755"
---
# <a name="client-side-vs-server-side-xml-formatting-sqlxml-40"></a>Diferencias entre XPath en el cliente y Aplicación de formato XML en el servidor (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  En este tema se describen las diferencias generales que existen entre la aplicación de formato XML del lado cliente y del lado servidor en SQLXML.  
  
## <a name="multiple-rowset-queries-not-supported-in-client-side-formatting"></a>En el formato del cliente, no se admiten consultas de varios conjuntos de filas  
 Cuando la aplicación de formato XML es del lado cliente, no se admiten consultas que generen varios conjuntos de filas. Supongamos, por ejemplo, que tiene un directorio virtual en el que ha especificado que la aplicación formato se realice del lado cliente. Considere la posibilidad de esta plantilla de ejemplo, que tiene dos instrucciones SELECT en una  **\<SQL: >** bloque:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <sql:query>  
     SELECT FirstName FROM Person.Contact FOR XML Nested;   
     SELECT LastName FROM Person.Contact FOR XML Nested    
  </sql:query>  
</ROOT>  
```  
  
 Si ejecuta esta plantilla en el código de la aplicación, se devolverá un error, puesto que el formato XML del lado cliente no admite el formato de varios conjuntos de filas. Si especifica las consultas en dos separar  **\<SQL: >** bloques, obtendrá los resultados deseados.  
  
## <a name="timestamp-maps-differently-in-client--vs-server-side-formatting"></a>timestamp se asigna de distinto modo cuando la aplicación de formato se realiza en el cliente o en el servidor  
 En el XML en el servidor de formato, la columna de base de datos de **timestamp** tipo se asigna al tipo XDR i8 (cuando se especifica la opción XMLDATA en la consulta).  
  
 En XML en el cliente de formato, la columna de base de datos de **marca de tiempo** tipo se asigna a cualquiera la **uri** o el **bin.base64** tipo XDR (dependiendo de si el binario base64 opción se especifica en la consulta). El **bin.base64** tipo XDR es útil si usa las características de diagrama de actualización y la carga masiva, porque este tipo se convierte en el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **timestamp** tipo. De esta forma, las operaciones de inserción, actualización o eliminación se realizan correctamente.  
  
## <a name="deep-variants-are-used-in-server-side-formatting"></a>En el formato del servidor se usan tipos VARIANT profundos  
 En la aplicación de formato XML en el servidor, se usan los tipos profundos de un tipo VARIANT. Si aplica el formato XML del lado cliente, los datos VARIANT se convierten en una cadena Unicode y no se usan los subtipos de VARIANT.  
  
## <a name="nested-mode-vs-auto-mode"></a>Diferencias entre el modo NESTED y el modo AUTO  
 El modo NESTED de la instrucción FOR XML del lado cliente es similar al modo AUTO de la instrucción FOR XML del servidor, con las siguientes excepciones:  
  
### <a name="when-you-query-views-using-auto-mode-on-the-server-side-the-view-name-is-returned-as-the-element-name-in-the-resulting-xml"></a>Al consultar vistas utilizando el modo AUTO en el servidor, el nombre de la vista se devuelve como el nombre del elemento en el código XML resultante.  
 Por ejemplo, supongamos que la vista siguiente se crea en la tabla Person.Contact en la AdventureWorksdatabase:  
  
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
  
 Al ejecutar la plantilla, se devuelve el código XML siguiente. (Solo se muestran resultados parciales). Observe que los nombres de elemento son los nombres de las vistas en las que se ejecuta la consulta.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <ContactView CID="1" FName="Gustavo" LName="Achong" />   
  <ContactView CID="2" FName="Catherine" LName="Abel" />   
...  
</ROOT>  
```  
  
 Al especificar el formato XML del lado cliente utilizando el modo NESTED correspondiente, los nombres de la tabla base se devuelven como los nombres de elemento en el código XML resultante. Por ejemplo, la siguiente plantilla modificada ejecuta la misma instrucción SELECT, pero el formato XML se realiza en el lado cliente (es decir, **client-side-xml** está establecido en true en la plantilla):  
  
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
  
 Cuando se utiliza el modo NESTED de la instrucción FOR XML del lado cliente, los nombres de tabla se devuelven como nombres de elemento en el código XML resultante. (No se utilizan los alias de tabla especificados en la consulta). Por ejemplo, fíjese en esta plantilla:  
  
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
  
 Si el formato XML se realiza en el servidor (**client-side-xml = "0"**), puede utilizar el alias para las columnas que devuelven consultas dbobject en qué tabla y columna reales se devuelven los nombres (aunque haya especificado alias). Por ejemplo, la plantilla siguiente ejecuta una consulta y el formato XML se realiza en el servidor (el **client-side-xml** no se especifica la opción y la **ejecutar en el cliente** opción no está seleccionada para el raíz virtual). La consulta especifica también el modo AUTO (no el modo NESTED del lado cliente).  
  
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
  
-   Al especificar **client-side-xml = "0"** (false) en una plantilla, que está solicitando en formato XML del lado servidor. Por lo tanto, no es posible especificar FOR XML NESTED porque el servidor no reconoce la opción NESTED. Esto genera un error. Deben utilizarse los modos AUTO, RAW o EXPLICIT, que el servidor sí que reconoce.  
  
-   Al especificar **client-side-xml = "1"** (true) en una plantilla, que solicita un formato XML del lado cliente. En este caso, puede especificarse FOR XML NESTED. Si se especifica FOR XML AUTO, el formato XML se produce en el servidor aunque **client-side-xml = "1"** se especifica en la plantilla.  
  
## <a name="see-also"></a>Vea también  
 [Para conocer las consideraciones de seguridad XML &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/for-xml-security-considerations-sqlxml-4-0.md)   
 [Aplicación de formato XML del lado cliente &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml/formatting/client-side-xml-formatting-sqlxml-4-0.md)   
 [Aplicación de formato XML del lado servidor &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml/formatting/server-side-xml-formatting-sqlxml-4-0.md)  
  
  
