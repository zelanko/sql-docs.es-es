---
title: Asignación explícita elementos y atributos XSD a tablas y columnas | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-xml
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
caps.latest.revision: 28
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: b411f418f684ad54a7a04bce0a8c90484f475dc9
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="explicit-mapping-xsd-elements-and-attributes-to-tables-and-columns"></a>Asignación explícita elementos y atributos XSD a tablas y columnas
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Cuando se utiliza un esquema XSD para proporcionar una vista XML de la base de datos relacional, los elementos y atributos del esquema se deben asignar a tablas y columnas de la base de datos. Las filas de la tabla o vista de la base de datos se asignarán a elementos del documento XML. Los valores de columna de la base de datos se asignan a atributos o elementos.  
  
 Cuando se especifican consultas XPath en el esquema XSD agregado, los datos de los elementos y atributos del esquema se recuperan de las tablas y columnas a las que se asignan. Para obtener un único valor de la base de datos, la asignación especificada en el esquema XSD debe tener una especificación de campo y relación. Si el nombre de un elemento o atributo no es el mismo nombre que el nombre de tabla o vista o columna a la que se asigna, el **SQL: relation** y **SQL: Field** anotaciones se usan para especificar la asignación entre un elemento o atributo de un documento XML y la tabla (vista) o columna en una base de datos.  
  
## <a name="sql-relation"></a>sql-relation  
 El **SQL: relation** anotación se agrega a un nodo XML en el esquema XSD se asignan a una tabla de base de datos. El nombre de una tabla (vista) se especifica como el valor de la **SQL: relation** anotación.  
  
 Cuando **SQL: relation** se especifica en un elemento, el ámbito de esta anotación se aplica a todos los atributos y elementos secundarios que se describen en la definición de tipo complejo de ese elemento, por lo tanto, proporcionar un acceso directo para escribir anotaciones.  
  
 El **SQL: relation** anotación también es útil cuando los identificadores que son válidos en [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no son válidos en XML. Por ejemplo, "Order Details" es un nombre de tabla válido en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pero no en XML. En tales casos, la **SQL: relation** anotación puede utilizarse para especificar la asignación, por ejemplo:  
  
```  
<xsd:element name="OD" sql:relation="[Order Details]">  
```  
  
## <a name="sql-field"></a>sql-field  
 El **campo sql** anotación asigna un elemento o atributo a una columna de base de datos. El **SQL: Field** anotación se agrega para asignar un nodo XML en el esquema a una columna de base de datos. No se puede especificar **SQL: Field** en un elemento de contenido vacío.  
  
## <a name="examples"></a>Ejemplos  
 Para crear muestras funcionales mediante los ejemplos siguientes, debe cumplir determinados requisitos. Para obtener más información, consulte [requisitos para ejecutar los ejemplos de SQLXML](../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md).  
  
### <a name="a-specifying-the-sqlrelation-and-sqlfield-annotations"></a>A. Especificar las anotaciones sql:relation y sql:field  
 En este ejemplo, el esquema XSD consta de un  **\<póngase en contacto con >** elemento de tipo complejo con  **\<FName >** y  **\<LName >** los elementos secundarios y los **ContactID** atributo.  
  
 El **SQL: relation** anotación asigna el  **\<póngase en contacto con >** elemento a la tabla Person.Contact en la base de datos de AdventureWorks. El **SQL: Field** mapas de anotación la  **\<FName >** elemento a la columna FirstName y  **\<LName >** elemento LastName columna.  
  
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
  
  
