---
title: Introducción a los esquemas XSD anotados (SQLXML 4,0) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- namespaces [SQLXML], annotated XSD schemas
- mapping schema [SQLXML], about mapping schema
- views [SQLXML]
- valid XSD schemas [SQLXML]
- annotations [SQLXML]
- XSD schemas [SQLXML], creating XML views
- annotated XSD schemas, creating XML views
- minimum XSD schema
- annotated XSD schemas, examples
- XML views [SQLXML]
ms.assetid: 15282db1-65c4-43be-bdb7-e9ef49cb33a2
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 8b00f2a5f7d6bf9b0ac127b5df736d4a40c94219
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/01/2020
ms.locfileid: "82702935"
---
# <a name="introduction-to-annotated-xsd-schemas-sqlxml-40"></a>Introducción a los esquemas XSD anotados (SQLXML 4.0)
  Puede crear vistas XML de datos relacionales utilizando el lenguaje de definición de esquemas XML (XSD). Estas vistas pueden consultarse después utilizando consultas XPath (Lenguaje de rutas XML). Es parecido a crear vistas utilizando instrucciones CREATE VIEW y, a continuación, especificar consultas SQL en la vista.  
  
 Un esquema XML describe la estructura de un documento XML y también describe las distintas restricciones en los datos del documento. Cuando se especifican consultas XPath en el esquema, la estructura del documento XML devuelto viene determinada por el esquema en el que se ejecuta la consulta XPath.  
  
 En un esquema XSD, el elemento ** \< xsd: Schema>** incluye todo el esquema; todas las declaraciones de elementos deben estar dentro del elemento ** \< xsd: Schema>** . Puede describir los atributos que definen el espacio de nombres en el que reside el esquema y los espacios de nombres que se usan en el esquema como propiedades del elemento ** \< xsd: Schema>** .  
  
 Un esquema XSD válido debe contener el elemento ** \< xsd: Schema>** definido como se indica a continuación:  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<!-- additional schema definitions here -->  
</xsd:schema>  
```  
  
 El elemento ** \< xsd: Schema>** se deriva de la especificación del espacio de nombres del esquema XML en http://www.w3.org/2001/XMLSchema .  
  
## <a name="annotations-to-the-xsd-schema"></a>Anotaciones en el esquema XSD  
 Puede usar un esquema XSD con anotaciones que describan la asignación a una base de datos, consultar la base de datos y devolver los resultados en forma de documento XML. Las anotaciones se proporcionan para asignar un esquema XSD a las tablas y columnas de base de datos. Pueden especificarse consultas XPath en la vista XML creada por el esquema XSD para consultar la base de datos y obtener los resultados en un documento XML.  
  
> [!NOTE]  
>  En [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLXML 4.0, el lenguaje de esquemas XSD admite las anotaciones introducidas por el lenguaje de esquemas reducidos de datos XML (XDR) anotados de [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)]. Los esquemas XDR anotados han quedado desusados en SQLXML 4.0.  
  
 En el contexto de la base de datos relacional, resulta de gran utilidad para asignar el esquema XSD arbitrario a un almacén relacional. Una forma de conseguirlo es anotar el esquema XSD. Un esquema XSD con anotaciones se conoce como *esquema de asignación*, que proporciona información relativa al modo en que se asignan los datos XML al almacén relacional. Un esquema de asignación es realmente una vista XML de los datos relacionales. Estas asignaciones pueden usarse para recuperar los datos relacionales como un documento XML.  
  
## <a name="namespace-for-annotations"></a>Espacio de nombres para las anotaciones  
 En un esquema XSD, las anotaciones se especifican mediante el espacio de nombres **urn: schemas-microsoft-com: mapping-schema**. Como se muestra en el ejemplo siguiente, la manera más fácil de especificar el espacio de nombres es especificarlo en la etiqueta ** \< xsd: Schema>** .  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
...  
</xsd:schema>  
```  
  
 Se utiliza un prefijo de espacio de nombres arbitrario. En esta documentación, el prefijo **SQL** se utiliza para denotar el espacio de nombres de la anotación y distinguir las anotaciones de este espacio de nombres de las de otros espacios de nombres.  
  
## <a name="example-of-an-annotated-xsd-schema"></a>Ejemplo de un esquema XSD anotado  
 En el ejemplo siguiente, el esquema XSD está compuesto de un elemento ** \< Person. contact>** . El elemento ** \< employee>** tiene un atributo **ContactID** y ** \< FirstName>** y ** \< LastName>** elementos secundarios:  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema">  
  <xsd:element name="Contact" >  
   <xsd:complexType>  
     <xsd:sequence>  
        <xsd:element name="FName"    
                     type="xsd:string" />   
        <xsd:element name="LName"  
                     type="xsd:string" />  
     </xsd:sequence>  
        <xsd:attribute name="ConID" type="xsd:integer" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 Se han agregado anotaciones a este esquema XSD para asignar sus elementos y atributos a las tablas y columnas de base de datos:  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:element name="Contact" sql:relation="Person.Contact" >  
   <xsd:complexType>  
     <xsd:sequence>  
        <xsd:element name="FName"  
                     sql:field="FirstName"   
                     type="xsd:string" />   
        <xsd:element name="LName"    
                     sql:field="LastName"    
                     type="xsd:string" />  
     </xsd:sequence>  
        <xsd:attribute name="ConID"   
                       sql:field="ContactID"   
                       type="xsd:integer" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 En el esquema de asignación, el elemento de ** \<>de contacto** se asigna a la tabla person. contact de la base de datos de ejemplo AdventureWorks mediante la `sql:relation` anotación. Los atributos ConID, FName y LName se asignan a las columnas ContactID, FirstName y LastName de la tabla Person.Contact mediante las anotaciones `sql:field`.  
  
 Este esquema XSD anotado proporciona la vista XML de los datos relacionales. Esta vista XML puede consultarse utilizando el lenguaje XPath. Una consulta XPath devuelve como resultado un documento XML en lugar del conjunto de filas que devuelven las consultas SQL.  
  
> [!NOTE]  
>  En el esquema de asignación, la distinción de mayúsculas y minúsculas para los valores relacionales especificados (como el nombre de tabla y el nombre de columna) depende de que SQL Server utilice la configuración de intercalación con distinción de mayúsculas y minúsculas. Para más información, consulte [Compatibilidad con la intercalación y Unicode](../../collations/collation-and-unicode-support.md).  
  
## <a name="other-resources"></a>Otros recursos  
 Puede buscar más información sobre el lenguaje de definición de esquemas XML (XSD), el lenguaje de rutas XML (XPath) y el lenguaje de transformación basado en hojas de estilo (XSLT) en los siguientes sitios web:  
  
-   XML Schema Part 0: manual, recomendación de W3C (http://www.w3.org/TR/xmlschema-0/)  
  
-   XML Schema Part 1: Structures, W3C Recommendation (http://www.w3.org/TR/xmlschema-1/)  
  
-   Esquema XML parte 2: tipos de archivo, recomendación de W3C (http://www.w3.org/TR/xmlschema-2/)  
  
-   Lenguaje de rutas XML (XPath) (http://www.w3.org/TR/xpath)  
  
-   Transformaciones XSL (XSLT) (http://www.w3.org/TR/xslt)  
  
## <a name="see-also"></a>Consulte también  
 [Consideraciones sobre la seguridad del esquema anotado &#40;SQLXML 4,0&#41;](../../sqlxml-annotated-xsd-schemas-xpath-queries/security/annotated-schema-security-considerations-sqlxml-4-0.md)   
 [Los esquemas XDR anotados &#40;han quedado en desuso en SQLXML 4,0&#41;](annotated-xdr-schemas-deprecated-in-sqlxml-4-0.md)  
  
  
