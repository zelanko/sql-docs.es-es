---
title: 'Conversiones de tipos de datos y las anotaciones (SQLXML 4.0) de SQL: DataType | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- mapping data types [SQLXML]
- type attribute
- sql:datatype
- data types [SQLXML], converting
- annotated XSD schemas, mapping data types
- xsd:type
- datatype annotation
- converting data types [SQLXML]
- data types [SQLXML], mapping data types
- XSD schemas [SQLXML], mapping data types
ms.assetid: db192105-e8aa-4392-b812-9d727918c005
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 7662587e1cffad5b111c747c0af2116991743296
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63228909"
---
# <a name="data-type-coercions-and-the-sqldatatype-annotation-sqlxml-40"></a>Conversión de tipos de datos y la anotación sql:datatype (SQLXML 4.0)
  En un esquema XSD, el atributo `xsd:type` especifica el tipo de datos XSD de un elemento o atributo. Cuando se usa un esquema XSD para extraer datos de la base de datos, el tipo de datos especificado se usa para dar formato a los datos.  
  
 Además de especificar un tipo XSD en un esquema, también puede especificar un tipo de datos de Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizando la anotación `sql:datatype`. Los atributos `xsd:type` y `sql:datatype` controlan la asignación entre los tipos de datos XSD y los tipos de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="xsdtype-attribute"></a>Atributo xsd:type  
 Puede usar el atributo `xsd:type` para especificar el tipo de datos XML de un atributo o elemento que se asigna a una columna. `xsd:type` afecta al documento que se devuelve del servidor y también a la consulta XPath que se ejecuta. Cuando una consulta XPath se ejecuta en un esquema de asignación que contiene el atributo `xsd:type`, XPath usa el tipo de datos especificado al procesar la consulta. Para obtener más información sobre el uso XPath `xsd:type`, consulte [asignación de tipos de datos XSD a tipos de datos XPath &#40;SQLXML 4.0&#41;](../sqlxml-annotated-xsd-schemas-xpath-queries/xpath-data-types-sqlxml-4-0.md).  
  
 En un documento devuelto, todos los tipos de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se convierten en representaciones de cadena. Algunos tipos de datos requieren conversiones adicionales. En la tabla siguiente se indican las conversiones que se usan para distintos valores de `xsd:type`.  
  
|Tipo de datos XSD|Conversión de SQL Server|  
|-------------------|---------------------------|  
|Boolean|CONVERT(bit, COLUMN)|  
|date|LEFT(CONVERT(nvarchar(4000), COLUMN, 126), 10)|  
|Decimal|CONVERT(money, COLUMN)|  
|id/idref/idrefs|id-prefix + CONVERT(nvarchar(4000), COLUMN, 126)|  
|nmtoken/nmtokens|id-prefix + CONVERT(nvarchar(4000), COLUMN, 126)|  
|Time|SUBSTRING(CONVERT(nvarchar(4000), COLUMN, 126), 1+CHARINDEX(N'T', CONVERT(nvarchar(4000), COLUMN, 126)), 24)|  
|Todos las demás|Ninguna conversión adicional|  
  
> [!NOTE]  
>  Es posible que algunos de los valores devueltos por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no sean compatibles con los tipos de datos XML especificados con `xsd:type`, ya sea porque la conversión no es posible (por ejemplo, convertir "XYZ" en un tipo de datos `decimal`) o porque el valor supera el intervalo de ese tipo de datos (por ejemplo, -100000 convertido en un tipo XSD `UnsignedShort`). Las conversiones de tipos incompatibles pueden dar lugar a documentos XML no válidos o a errores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="mapping-from-sql-server-data-types-to-xsd-data-types"></a>Asignar tipos de datos SQL Server a tipos de datos XSD  
 En la tabla siguiente se muestra una asignación obvia de tipos de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a tipos de datos XSD. Si se conoce el tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], esta tabla proporciona el tipo XSD correspondiente que puede especificarse en el esquema XSD.  
  
|Tipo de datos de SQL Server|Tipo de datos XSD|  
|--------------------------|-------------------|  
|`bigint`|`long`|  
|`binary`|`base64Binary`|  
|`bit`|`boolean`|  
|`char`|`string`|  
|`datetime`|`dateTime`|  
|`decimal`|`decimal`|  
|`float`|`double`|  
|`image`|`base64Binary`|  
|`int`|`int`|  
|`money`|`decimal`|  
|`nchar`|`string`|  
|`ntext`|`string`|  
|`nvarchar`|`string`|  
|`numeric`|`decimal`|  
|`real`|`float`|  
|`smalldatetime`|`dateTime`|  
|`smallint`|`short`|  
|`smallmoney`|`decimal`|  
|`sql_variant`|`string`|  
|`sysname`|`string`|  
|`text`|`string`|  
|`timestamp`|`dateTime`|  
|`tinyint`|`unsignedByte`|  
|`varbinary`|`base64Binary`|  
|`varchar`|`string`|  
|`uniqueidentifier`|`string`|  
  
## <a name="sqldatatype-annotation"></a>Anotación sql:datatype  
 La anotación `sql:datatype` se usa para especificar el tipo de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]; esta anotación debe especificarse cuando:  
  
-   Es la carga masiva en un `dateTime` [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] columna desde un XSD `dateTime`, `date`, o `time` tipo. En este caso, debe identificar el tipo de datos de la columna [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizando `sql:datatype="dateTime"`. Esta regla también se aplica a los diagramas de actualización.  
  
-   Es la carga masiva en una columna de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `uniqueidentifier` tipo y el valor XSD es un GUID que incluye llaves ({y}). Cuando se especifica `sql:datatype="uniqueidentifier"`, las llaves se quitan del valor antes de insertarlo en la columna. Si no se especifica `sql:datatype`, el valor se envía con las llaves y se produce un error en la inserción o actualización.  
  
-   El tipo de datos XML `base64Binary` se asigna a varios tipos de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (`binary`, `image` o `varbinary`). Para asignar el tipo de datos XML `base64Binary` a un tipo de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] concreto, use la anotación `sql:datatype`. Esta anotación especifica el tipo de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] explícito de la columna a la que asigna el atributo. Esto resulta de gran utilidad cuando los datos se almacenan en las bases de datos. Puede identificar el tipo de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] explícito especificando la anotación `sql:datatype`.  
  
 Generalmente, es recomendable especificar `sql:datatype` en el esquema.  
  
## <a name="examples"></a>Ejemplos  
 Para crear muestras funcionales mediante los ejemplos siguientes, debe cumplir determinados requisitos. Para obtener más información, consulte [requisitos para ejecutar los ejemplos de SQLXML](../sqlxml/requirements-for-running-sqlxml-examples.md).  
  
### <a name="a-specifying-xsdtype"></a>A. Especificar xsd:type  
 En este ejemplo se muestra cómo un tipo `date` de XSD que se especifica mediante el atributo `xsd:type` en el esquema afecta al documento XML resultante. El esquema proporciona una vista XML de la tabla Sales.SalesOrderHeader de la base de datos AdventureWorks.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:element name="Order" sql:relation="Sales.SalesOrderHeader">  
     <xsd:complexType>  
       <xsd:attribute name="SalesOrderID" type="xsd:string" />   
       <xsd:attribute name="CustomerID"   type="xsd:string" />   
       <xsd:attribute name="OrderDate"    type="xsd:date" />   
       <xsd:attribute name="DueDate"  />   
       <xsd:attribute name="ShipDate"  type="xsd:time" />   
     </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 En este esquema XSD, hay tres atributos que devuelven un valor de fecha de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Cuando el esquema:  
  
-   Especifica `xsd:type=date` en el **OrderDate** atributo, la parte de fecha del valor devuelto por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para el **OrderDate** se muestra el atributo.  
  
-   Especifica `xsd:type=time` en el **ShipDate** atributo, la parte de hora del valor devuelto por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para el **ShipDate** se muestra el atributo.  
  
-   No especifique `xsd:type` en el **DueDate** atributo, el mismo valor que devuelve [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se muestra.  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>Para probar una consulta de XPath de ejemplo con respecto al esquema  
  
1.  Copie el código de esquema anterior y péguelo en un archivo de texto. Guarde el archivo como xsdType.xml.  
  
2.  Copie la plantilla siguiente y péguela en un archivo de texto. Guarde el archivo como xsdTypeT.xml en el mismo directorio donde guardó xsdType.xml.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="xsdType.xml">  
        /Order  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     La ruta de acceso al directorio especificada para el esquema de asignación (xsdType.xml) es relativa al directorio donde se guarda la plantilla. También puede especificarse una ruta de acceso absoluta como, por ejemplo:  
  
    ```  
    mapping-schema="C:\SqlXmlTest\xsdType.xml"  
    ```  
  
3.  Cree y use el script de prueba SQLXML 4.0 (Sqlxml4test.vbs) para ejecutar la plantilla.  
  
     Para obtener más información, consulte [utilizar ADO para ejecutar consultas de SQLXML 4.0](../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Éste es el conjunto de resultados parciales:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Order SalesOrderID="43659"   
         CustomerID="676"   
         OrderDate="2001-07-01"   
         DueDate="2001-07-13T00:00:00"   
         ShipDate="00:00:00" />   
  <Order SalesOrderID="43660"   
         CustomerID="117"   
         OrderDate="2001-07-01"   
         DueDate="2001-07-13T00:00:00"   
         ShipDate="00:00:00" />   
 ...  
</ROOT>  
```  
  
 Éste es el esquema XDR equivalente:  
  
```  
<?xml version="1.0" ?>  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"  
        xmlns:dt="urn:schemas-microsoft-com:datatypes"  
        xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  
<ElementType name="Order" sql:relation="Sales.SalesOrderHeader">  
    <AttributeType name="SalesOrderID" />  
    <AttributeType name="CustomerID"  />  
    <AttributeType name="OrderDate" dt:type="date" />  
    <AttributeType name="DueDate" />  
    <AttributeType name="ShipDate" dt:type="time" />  
  
    <attribute type="SalesOrderID" sql:field="OrderID" />  
    <attribute type="CustomerID" sql:field="CustomerID" />  
    <attribute type="OrderDate" sql:field="OrderDate" />  
    <attribute type="DueDate" sql:field="DueDate" />  
    <attribute type="ShipDate" sql:field="ShipDate" />  
</ElementType>  
</Schema>  
```  
  
### <a name="b-specifying-sql-data-type-using-sqldatatype"></a>b. Especificar el tipo de datos SQL usando sql:datatype  
 Para obtener un ejemplo funcional, vea el ejemplo G en [ejemplos de carga masiva XML &#40;SQLXML 4.0&#41;](../sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/xml-bulk-load-examples-sqlxml-4-0.md). En este ejemplo, se carga de forma masiva un valor GUID que incluye "{" y "}". El esquema de este ejemplo especifica `sql:datatype` para identificar el tipo de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como `uniqueidentifier`. En este ejemplo se muestra cuándo debe especificarse `sql:datatype` en el esquema.  
  
  
