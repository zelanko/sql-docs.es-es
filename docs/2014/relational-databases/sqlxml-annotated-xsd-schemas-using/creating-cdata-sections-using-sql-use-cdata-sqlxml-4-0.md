---
title: 'Creación de secciones de CDATA mediante SQL: use-cdata (SQLXML 4.0) | Documentos de Microsoft'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- markup characters [SQLXML]
- special characters [SQLXML]
- use-cdata annotation
- plain text [SQLXML]
- CDATA sections
- escaping blocks of text [SQLXML]
- annotated XSD schemas, CDATA sections
- sql:use-cdata
ms.assetid: 26d2b9dc-f857-44ff-bcd4-aaf64ff809d0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cddde2ed1e40b2ea21cf4ebff75bea3beed8f2ce
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66014006"
---
# <a name="creating-cdata-sections-using-sqluse-cdata-sqlxml-40"></a>Crear secciones CDATA mediante sql:use-cdata (SQLXML 4.0)
  En XML, las secciones CDATA se usan para establecer secuencias de escape en bloques de texto que contienen caracteres que, de lo contrario, se reconocerían como caracteres de marcado.  
  
 Una base de datos en Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a veces pueden contener caracteres que se tratan como caracteres de marcado por el analizador XML; los corchetes angulares, por ejemplo, (\< y >), el símbolo menor o igual que (< =) y el "y" comercial (&) son se tratan como caracteres de marcado. Sin embargo, puede ajustar este tipo de caracteres especiales en una sección CDATA para evitar que se traten como caracteres de marcado. El analizador XML trata el texto de la sección CDATA como texto simple.  
  
 La anotación `sql:use-cdata` se usa para especificar que los datos que devuelve [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se deberían ajustar en una sección CDATA (es decir, indica si el valor de una columna especificada a través de `sql:field` se debería agregar en una sección CDATA). La anotación `sql:use-cdata` únicamente se puede especificar en los elementos que asignan a una columna de base de datos.  
  
 La anotación `sql:use-cdata` toma un valor booleano (0 = false, 1 = true). Los valores permitidos son 0, 1, true y false.  
  
 Esta anotación no se puede usar con `sql:url-encode` ni en los tipos de atributo ID, IDREF, IDREFS, NMTOKEN y NMTOKENS.  
  
## <a name="examples"></a>Ejemplos  
 Para crear muestras funcionales mediante los ejemplos siguientes, debe cumplir determinados requisitos. Para obtener más información, consulte [requisitos para ejecutar los ejemplos de SQLXML](../sqlxml/requirements-for-running-sqlxml-examples.md).  
  
### <a name="a-specifying-sqluse-cdata-on-an-element"></a>A. Especificar sql:use-cdata en un elemento  
 En el siguiente esquema, `sql:use-cdata` está establecido en 1 (True) para el  **\<AddressLine1 >** dentro de la  **\<dirección >** elemento. Como resultado, los datos se devuelven en una sección CDATA.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:element name="Address"   
               sql:relation="Person.Address"   
               sql:key-fields="AddressID" >  
   <xsd:complexType>  
        <xsd:sequence>  
          <xsd:element name="AddressID"  type="xsd:string" />  
          <xsd:element name="AddressLine1" type="xsd:string"   
                       sql:use-cdata="1" />  
        </xsd:sequence>  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>Para probar una consulta de XPath de ejemplo con respecto al esquema  
  
1.  Copie el código de esquema anterior y péguelo en un archivo de texto. Guarde el archivo como UseCData.xml.  
  
2.  Copie la plantilla siguiente y péguela en un archivo de texto. Guarde el archivo como UseCDataT.xml en el mismo directorio donde guardó UseCData.xml.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
        <sql:xpath-query mapping-schema="UseCData.xml">  
            /Address[AddressID < 11]  
        </sql:xpath-query>  
    </ROOT>  
    ```  
  
     La ruta de acceso al directorio especificada para el esquema de asignación (UseCData.xml) es relativa al directorio donde se guarda la plantilla. También puede especificarse una ruta de acceso absoluta como, por ejemplo:  
  
    ```  
    mapping-schema="C:\SqlXmlTest\UseCData.xml"  
    ```  
  
3.  Cree y use el script de prueba SQLXML 4.0 (Sqlxml4test.vbs) para ejecutar la plantilla.  
  
     Para obtener más información, consulte [utilizar ADO para ejecutar consultas de SQLXML 4.0](../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Éste es el conjunto de resultados parciales:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">   
  <Address>   
    <AddressID>1</CustomerID>   
    <AddressLine1>   
      <![CDATA[ 1970 Napa Ct.  ]]>   
    </AddressLine1>   
  </Address>  
  <Address>  
    <AddressLine1>   
      <![CDATA[ 9833 Mt. Dias Blv. ]]>   
    </AddressLine1>   
  </Address>  
  ...  
</ROOT>  
```  
  
  
