---
title: Asignación explícita elementos y atributos XSD a tablas y columnas | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: xml
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
author: MightyPen
ms.author: genemi
ms.reviewer: ''
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a9d363d4e2efd5d288128d6d1a428ddcb00fa54c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65980902"
---
# <a name="explicit-mapping-xsd-elements-and-attributes-to-tables-and-columns"></a>Asignación explícita de elementos y atributos XSD a tablas y columnas
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Cuando se utiliza un esquema XSD para proporcionar una vista XML de la base de datos relacional, los elementos y atributos del esquema se deben asignar a tablas y columnas de la base de datos. Las filas de la tabla o vista de la base de datos se asignarán a elementos del documento XML. Los valores de columna de la base de datos se asignan a atributos o elementos.  
  
 Cuando se especifican consultas XPath en el esquema XSD agregado, los datos de los elementos y atributos del esquema se recuperan de las tablas y columnas a las que se asignan. Para obtener un único valor de la base de datos, la asignación especificada en el esquema XSD debe tener una especificación de campo y relación. Si el nombre de un elemento o atributo no es el mismo nombre que el nombre de tabla o vista o columna al que se asigna, el **SQL: relation** y **SQL: Field** anotaciones se usan para especificar la asignación entre un elemento o atributo de un documento XML y la tabla (vista) o una columna en una base de datos.  
  
## <a name="sql-relation"></a>sql-relation  
 El **SQL: relation** anotación se agrega para asignar un nodo XML en el esquema XSD a una tabla de base de datos. Se especifica el nombre de una tabla (vista) como el valor de la **SQL: relation** anotación.  
  
 Cuando **SQL: relation** se especifica en un elemento, el ámbito de esta anotación se aplica a todos los atributos y elementos secundarios que se describen en la definición de tipo complejo de ese elemento, lo que proporciona un acceso directo para escritura anotaciones.  
  
 El **SQL: relation** anotación también es útil cuando los identificadores que son válidos en [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no son válidos en XML. Por ejemplo, "Order Details" es un nombre de tabla válido en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pero no en XML. En tales casos, el **SQL: relation** anotación puede usarse para especificar la asignación, por ejemplo:  
  
```  
<xsd:element name="OD" sql:relation="[Order Details]">  
```  
  
## <a name="sql-field"></a>sql-field  
 El **sql campo** anotación asigna un elemento o atributo a una columna de base de datos. El **SQL: Field** anotación se agrega para asignar un nodo XML en el esquema a una columna de base de datos. No puede especificar **SQL: Field** en un elemento de contenido vacío.  
  
## <a name="examples"></a>Ejemplos  
 Para crear muestras funcionales mediante los ejemplos siguientes, debe cumplir determinados requisitos. Para obtener más información, consulte [requisitos para ejecutar los ejemplos de SQLXML](../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md).  
  
### <a name="a-specifying-the-sqlrelation-and-sqlfield-annotations"></a>A. Especificar las anotaciones sql:relation y sql:field  
 En este ejemplo, el esquema XSD consta de un  **\<contacto >** elemento de tipo complejo con  **\<FName >** y  **\<LName >** elementos secundarios y la **ContactID** atributo.  
  
 El **SQL: relation** anotación asigna el  **\<póngase en contacto con >** elemento a la tabla Person.Contact en la base de datos AdventureWorks. El **SQL: Field** anotación asigna el  **\<FName >** elemento a la columna FirstName y el  **\<LName >** elemento para el apellido columna.  
  
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
  
     Para obtener más información, consulte [utilizar ADO para ejecutar consultas SQLXML](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
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
  
  
