---
title: 'Crear secciones CDATA mediante SQL: Use-CDATA (SQLXML)'
ms.date: 01/11/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
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
ms.reviewer: ''
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 289e0e7ecb720afc4440283a97bcb7d55ccee8b8
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/19/2019
ms.locfileid: "75257495"
---
# <a name="creating-cdata-sections-using-sqluse-cdata-sqlxml-40"></a>Crear secciones CDATA mediante sql:use-cdata (SQLXML 4.0)

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  En XML, las secciones CDATA se usan para establecer secuencias de escape en bloques de texto que contienen caracteres que, de lo contrario, se reconocerían como caracteres de marcado.  
  
 A veces, una [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] base de datos de Microsoft puede contener caracteres que el analizador XML trata como caracteres de marcado. por ejemplo, los corchetes angulares (< y >), el símbolo menor o igual que (<=) y la y comercial (&) se tratan como caracteres de marcado. Sin embargo, puede ajustar este tipo de caracteres especiales en una sección CDATA para evitar que se traten como caracteres de marcado. El analizador XML trata el texto de la sección CDATA como texto simple.  
  
 La anotación **SQL: Use-CDATA** se usa para especificar que los datos devueltos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] por se deben ajustar en una sección CDATA (es decir, indica si el valor de una columna especificada por **SQL: Field** debe incluirse en una sección CDATA). La anotación **SQL: Use-CDATA** solo se puede especificar en elementos que se asignan a una columna de base de datos.  
  
 La anotación **SQL: Use-CDATA** toma un valor booleano (0 = false, 1 = true). Los valores permitidos son 0, 1, true y false.  
  
 Esta anotación no se puede usar con **SQL: URL-encode** ni en los tipos de atributo ID, idref, IDREFS, NMTOKEN y NMTOKENS.  
  
## <a name="examples"></a>Ejemplos  
 Para crear muestras funcionales mediante los ejemplos siguientes, debe cumplir determinados requisitos. Para obtener más información, vea [Requirements for Running SQLXML examples](../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md).  
  
### <a name="a-specifying-sqluse-cdata-on-an-element"></a>a. Especificar sql:use-cdata en un elemento  
 En el esquema siguiente, **SQL: Use-CDATA** se establece en 1 (true) para el ** \<>AddressLine1** dentro del ** \<elemento>de dirección** . Como resultado, los datos se devuelven en una sección CDATA.  
  
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
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>Para probar una consulta XPath de ejemplo en el esquema  
  
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
  
     Para obtener más información, vea [usar ado para ejecutar consultas SQLXML 4,0](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
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
  
  
