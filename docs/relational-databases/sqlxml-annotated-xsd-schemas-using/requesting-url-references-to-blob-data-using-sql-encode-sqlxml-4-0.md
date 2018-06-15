---
title: 'Solicitar referencias URL para datos BLOB mediante sql: encode (SQLXML 4.0) | Documentos de Microsoft'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
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
caps.latest.revision: 28
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 537e2656730c7659edd22ac68722bf43e892ad3d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32970660"
---
# <a name="requesting-url-references-to-blob-data-using-sqlencode-sqlxml-40"></a>Solicitar referencias URL a los datos BLOB mediante sql:encode (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  En un esquema XSD anotado, cuando un atributo (o elemento) se asigna a una columna de BLOB en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]de Microsoft, los datos se devuelven en formato codificado de base 64 en XML.  
  
 Si desea obtener una referencia a los datos (un URI) que se devuelvan que puede usarse posteriormente para recuperar los datos BLOB en un formato binario, especifique la **sql: codificar** anotación. Puede especificar **sql: codificar** en un atributo o elemento de tipo simple.  
  
 Especifique el **sql: codificar** anotación para indicar que se debe devolver una dirección URL para el campo en lugar del valor del campo. **SQL: codificar** depende de la clave principal para generar un select singleton en la dirección URL. La clave principal puede especificarse mediante la **SQL: Key-campos** anotación.  
  
 El **sql: codificar** anotación se puede asignar la dirección "url" o el valor "predeterminado". Un valor de "valor predeterminado" devuelve los datos en formato codificado de base 64.  
  
 El **sql: codificar** anotación no puede utilizarse con **SQL: use-cdata** o en el atributo ID, IDREF, IDREFS, NMTOKEN o NMTOKENS tipos. También no se puede utilizar con XSD **fijo** atributo.  
  
> [!NOTE]  
>  Las columnas de tipo BLOB no se pueden usar como parte de una clave o clave externa.  
  
## <a name="examples"></a>Ejemplos  
 Para crear muestras funcionales mediante los ejemplos siguientes, debe cumplir determinados requisitos. Para obtener más información, consulte [requisitos para ejecutar los ejemplos de SQLXML](../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md).  
  
### <a name="a-specifying-sqlencode-to-obtain-a-url-reference-to-blob-data"></a>A. Especificar sql:encode para obtener una referencia de URL a los datos BLOB  
 En este ejemplo, se especifica el esquema de asignación **sql: codificar** en el **LargePhoto** atributo para recuperar la referencia URI a una fotografía del producto determinada (en lugar de recuperar los datos binarios en Base 64: formato codificado).  
  
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
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>Para probar una consulta de XPath de ejemplo con respecto al esquema  
  
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
  
     Para obtener más información, consulte [utilizar ADO para ejecutar consultas de SQLXML 4.0](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 El resultado es el siguiente:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
   <ProductPhoto ProductPhotoID="100"  
                 LargePhoto="dbobject/Production.ProductPhoto[@ProductPhotoID="100"]/@LargePhoto" />   
</ROOT>  
```  
  
  
