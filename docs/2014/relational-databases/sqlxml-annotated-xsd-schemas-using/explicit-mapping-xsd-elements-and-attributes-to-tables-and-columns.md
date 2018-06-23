---
title: Asignación explícita de atributos y elementos XSD a tablas y columnas (SQLXML 4.0) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- explicit schema mapping [SQLXML]
- XPath queries [SQLXML], annotated XSD schemas in queries
- sql:field
- row mapping [SQLXML]
- attribute mapping [SQLXML], explicit mapping
- field annotation
- XSD schemas [SQLXML], mapping attributes and elements
- names [SQLXML]
- relation annotation
- table/view mapping [SQLXML], explicit mapping
- sql:relation
- mapping schema [SQLXML], explicit mapping
- annotated XSD schemas, mapping attributes and elements
- column mapping [SQLXML]
- element mapping [SQLXML], explicit mapping
- table mapping [SQLXML], explicit mapping
- element/attribute mapping [SQLXML]
ms.assetid: 7a5ebeb6-7322-4141-a307-ebcf95976146
caps.latest.revision: 27
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: ba2b9df8e9104afe0dc7c1645cc4cc64dd01d2ce
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36109432"
---
# <a name="explicit-mapping-of-xsd-elements-and-attributes-to-tables-and-columns-sqlxml-40"></a>Asignación explícita de elementos y atributos XSD a tablas y columnas (SQLXML 4.0)
  Cuando se utiliza un esquema XSD para proporcionar una vista XML de la base de datos relacional, los elementos y atributos del esquema se deben asignar a tablas y columnas de la base de datos. Las filas de la tabla o vista de la base de datos se asignarán a elementos del documento XML. Los valores de columna de la base de datos se asignan a atributos o elementos.  
  
 Cuando se especifican consultas XPath en el esquema XSD agregado, los datos de los elementos y atributos del esquema se recuperan de las tablas y columnas a las que se asignan. Para obtener un único valor de la base de datos, la asignación especificada en el esquema XSD debe tener una especificación de campo y relación. Si el nombre de un elemento o atributo no es el mismo que el nombre de la tabla/vista o columna al que se asigna, las anotaciones `sql:relation` y `sql:field` se utilizan para especificar la asignación entre un elemento o atributo de un documento XML y la tabla (vista) o columna de una base de datos.  
  
## <a name="sql-relation"></a>sql-relation  
 La anotación `sql:relation` se agrega para asignar un nodo XML en el esquema XSD a una tabla de base de datos. El nombre de una tabla (vista) se especifica como el valor de la anotación `sql:relation`.  
  
 Cuando se especifica `sql:relation` en un elemento, el ámbito de esta anotación se aplica a todos los atributos y elementos secundarios que se describen en la definición del tipo complejo de ese elemento, proporcionando por lo tanto un acceso directo para escribir anotaciones.  
  
 El `sql:relation` anotación también es útil cuando los identificadores que son válidos en [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no son válidos en XML. Por ejemplo, "Order Details" es un nombre de tabla válido en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pero no en XML. En casos como éste, la anotación `sql:relation` se puede utilizar para especificar la asignación, por ejemplo:  
  
```  
<xsd:element name="OD" sql:relation="[Order Details]">  
```  
  
## <a name="sql-field"></a>sql-field  
 La anotación `sql-field` asigna un elemento o atributo a una columna de base de datos. La anotación `sql:field` se agrega para asignar un nodo XML del esquema a una columna de base de datos. No se puede especificar `sql:field` en un elemento de contenido vacío.  
  
## <a name="examples"></a>Ejemplos  
 Para crear muestras funcionales mediante los ejemplos siguientes, debe cumplir determinados requisitos. Para obtener más información, consulte [requisitos para ejecutar los ejemplos de SQLXML](../sqlxml/requirements-for-running-sqlxml-examples.md).  
  
### <a name="a-specifying-the-sqlrelation-and-sqlfield-annotations"></a>A. Especificar las anotaciones sql:relation y sql:field  
 En este ejemplo, el esquema XSD consta de un  **\<póngase en contacto con >** elemento de tipo complejo con  **\<FName >** y  **\<LName >** los elementos secundarios y los **ContactID** atributo.  
  
 El `sql:relation` anotación asigna el  **\<póngase en contacto con >** elemento a la tabla Person.Contact en la base de datos de AdventureWorks. El `sql:field` mapas de anotación la  **\<FName >** elemento a la columna FirstName y  **\<LName >** elemento a la columna LastName.  
  
 Se especifica ninguna anotación para la **ContactID** atributo. Esto produce una asignación predeterminada del atributo a la columna del mismo nombre.  
  
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
        <xsd:attribute name="ContactID"   
                       type="xsd:integer" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>Para probar una consulta de XPath de ejemplo con respecto al esquema  
  
1.  Copie el código de esquema anterior y péguelo en un archivo de texto. Guarde el archivo como MySchema-annotated.xml.  
  
2.  Copie la plantilla siguiente siguiente y péguelo en un archivo de texto. Guarde el archivo como MySchema-annotatedT.xml en el mismo directorio donde guardó MySchema-annotated.xml.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="MySchema-annotated.xml">  
        /Contact  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     La ruta de acceso al directorio especificada para el esquema de asignación (MySchema-annotated.xml) es relativa al directorio donde se guarda la plantilla. También puede especificarse una ruta de acceso absoluta como, por ejemplo:  
  
    ```  
    mapping-schema="C:\SqlXmlTest\MySchema-annotated.xml"  
    ```  
  
3.  Cree y use el script de prueba SQLXML 4.0 (Sqlxml4test.vbs) para ejecutar la plantilla.  
  
     Para obtener más información, consulte [utilizar ADO para ejecutar consultas SQLXML](../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Éste es el conjunto de resultados parciales:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">   
 <Contact ContactID="1">   
    <FName>Gustavo</FName>   
    <LName>Achong</LName>   
 </Contact>   
  .....  
</ROOT>  
```  
  
  