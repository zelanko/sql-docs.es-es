---
title: 'Solicitar referencias URL a datos BLOB mediante SQL: encode (SQLXML 4,0) | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- sql:encode
- encode annotation
- URL references to BLOB data [SQLXML]
- references to BLOB data [SQLXML]
- annotated XSD schemas, URL references to BLOB data
- requesting URL references to BLOB data
- BLOBs, URL references
- Base 64-encoded format
ms.assetid: 2f8cd93b-c636-462b-8291-167197233ee0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 153a88bcb31f65d4e6aff007cfbee7d1f7afc6df
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66013731"
---
# <a name="requesting-url-references-to-blob-data-using-sqlencode-sqlxml-40"></a>Solicitar referencias URL a los datos BLOB mediante sql:encode (SQLXML 4.0)
  En un esquema XSD anotado, cuando un atributo (o elemento) se asigna a una columna de BLOB en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]de Microsoft, los datos se devuelven en formato codificado de base 64 en XML.  
  
 Si desea obtener una referencia a los datos (un URI) que se van a devolver, que se pueden usar posteriormente para recuperar los datos BLOB en un formato binario, especifique la anotación `sql:encode`. Puede especificar `sql:encode` en un atributo o elemento de tipo simple.  
  
 Especifique la anotación `sql:encode` para indicar que se debe devolver al campo una dirección URL en lugar del valor del campo. 
  `sql:encode` depende de la clave principal para generar un SELECT singleton en la dirección URL. La clave principal se puede especificar mediante la `sql:key-fields` anotación.  
  
 La anotación `sql:encode` puede tener asignada la dirección "url" o el valor "predeterminado". Un valor de "valor predeterminado" devuelve los datos en formato codificado de base 64.  
  
 La anotación `sql:encode` no se puede usar con `sql:use-cdata` o en los tipos de atributo ID, IDREF, IDREFS, NMTOKEN o NMTOKENS. Tampoco se puede utilizar con el atributo **fixed** xsd.  
  
> [!NOTE]  
>  Las columnas de tipo BLOB no se pueden usar como parte de una clave o clave externa.  
  
## <a name="examples"></a>Ejemplos  
 Para crear muestras funcionales mediante los ejemplos siguientes, debe cumplir determinados requisitos. Para obtener más información, vea [Requirements for Running SQLXML examples](../sqlxml/requirements-for-running-sqlxml-examples.md).  
  
### <a name="a-specifying-sqlencode-to-obtain-a-url-reference-to-blob-data"></a>A. Especificar sql:encode para obtener una referencia de URL a los datos BLOB  
 En este ejemplo, el esquema de asignación `sql:encode` especifica en el atributo **LargePhoto** para recuperar la referencia de URI a una fotografía de producto específica (en lugar de recuperar los datos binarios en formato codificado de base 64).  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  
  <xsd:element name="ProductPhoto" sql:relation="Production.ProductPhoto"   
               sql:key-fields="ProductPhotoID" >  
   <xsd:complexType>  
      <xsd:attribute name="ProductPhotoID"  type="xsd:int"  />  
     <xsd:attribute name="LargePhoto" type="xsd:string" sql:encode="url" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>Para probar una consulta XPath de ejemplo en el esquema  
  
1.  Copie el código de esquema anterior y péguelo en un archivo de texto. Guarde el archivo como sqlEncode.xml.  
  
2.  Copie la plantilla siguiente y péguela en un archivo de texto. Guarde el archivo como sqlEncodeT.xml en el mismo directorio donde guardó sqlEncode.xml.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
        <sql:xpath-query mapping-schema="sqlEncode.xml">  
            /ProductPhoto[@ProductPhotoID=100]  
        </sql:xpath-query>  
    </ROOT>  
    ```  
  
     La ruta de acceso al directorio especificada para el esquema de asignación (sqlEncode.xml) es relativa al directorio donde se guarda la plantilla. También puede especificarse una ruta de acceso absoluta como, por ejemplo:  
  
    ```  
    mapping-schema="C:\SqlXmlTest\sqlEncode.xml"  
    ```  
  
3.  Cree y use el script de prueba SQLXML 4.0 (Sqlxml4test.vbs) para ejecutar la plantilla.  
  
     Para obtener más información, vea [usar ado para ejecutar consultas SQLXML 4,0](../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 El resultado es el siguiente:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
   <ProductPhoto ProductPhotoID="100"  
                 LargePhoto="dbobject/Production.ProductPhoto[@ProductPhotoID="100"]/@LargePhoto" />   
</ROOT>  
```  
  
  
