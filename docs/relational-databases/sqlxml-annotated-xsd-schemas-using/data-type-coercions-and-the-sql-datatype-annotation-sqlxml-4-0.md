---
title: 'Conversiones de tipos de datos y la anotación sql: DataType (SQLXML 4,0) | Microsoft Docs'
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
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
author: MightyPen
ms.author: genemi
ms.reviewer: ''
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: fc7393d3f8f52dcbceeb9ef2ca295ef28a7b7222
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/25/2019
ms.locfileid: "72905977"
---
# <a name="data-type-coercions-and-the-sqldatatype-annotation-sqlxml-40"></a>Conversión de tipos de datos y la anotación sql:datatype (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  En un esquema XSD, el atributo **xsd: Type** especifica el tipo de datos XSD de un elemento o atributo. Cuando se usa un esquema XSD para extraer datos de la base de datos, el tipo de datos especificado se usa para dar formato a los datos.  
  
 Además de especificar un tipo XSD en un esquema, también puede especificar un tipo de datos de Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante la anotación **SQL: DataType** . Los atributos **xsd: Type** y **SQL: DataType** controlan la asignación entre los tipos de datos XSD y los tipos de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="xsdtype-attribute"></a>Atributo xsd:type  
 Puede usar el atributo **xsd: Type** para especificar el tipo de datos XML de un atributo o elemento que se asigna a una columna. El **xsd: Type** afecta al documento que se devuelve desde el servidor y también a la consulta XPath que se ejecuta. Cuando se ejecuta una consulta XPath en un esquema de asignación que contiene **xsd: Type**, XPath usa el tipo de datos especificado al procesar la consulta. Para obtener más información sobre cómo XPath utiliza **xsd: Type**, vea [asignar tipos de datos XSD a tipos &#40;de datos&#41;de XPath SQLXML 4,0](../../relational-databases/sqlxml-annotated-xsd-schemas-using/mapping-xsd-data-types-to-xpath-data-types-sqlxml-4-0.md).  
  
 En un documento devuelto, todos los tipos de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se convierten en representaciones de cadena. Algunos tipos de datos requieren conversiones adicionales. En la tabla siguiente se enumeran las conversiones que se usan para los distintos valores de **xsd: Type** .  
  
|Tipo de datos XSD|Conversión de SQL Server|  
|-------------------|---------------------------|  
|Booleano|CONVERT(bit, COLUMN)|  
|date|LEFT(CONVERT(nvarchar(4000), COLUMN, 126), 10)|  
|DECIMAL|CONVERT(money, COLUMN)|  
|id/idref/idrefs|id-prefix + CONVERT(nvarchar(4000), COLUMN, 126)|  
|nmtoken/nmtokens|id-prefix + CONVERT(nvarchar(4000), COLUMN, 126)|  
|time|SUBSTRING(CONVERT(nvarchar(4000), COLUMN, 126), 1+CHARINDEX(N'T', CONVERT(nvarchar(4000), COLUMN, 126)), 24)|  
|Todos las demás|Ninguna conversión adicional|  
  
> [!NOTE]  
>  Algunos de los valores devueltos por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podrían no ser compatibles con los tipos de datos XML especificados mediante **xsd: Type**, ya sea porque la conversión no es posible (por ejemplo, convertir "XYZ" en un tipo de datos **decimal** ) o porque el valor supera el intervalo de ese tipo de datos (por ejemplo,-100000 convertido en un tipo XSD **UnsignedShort** ). Las conversiones de tipos incompatibles pueden dar lugar a documentos XML no válidos o a errores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="mapping-from-sql-server-data-types-to-xsd-data-types"></a>Asignar tipos de datos SQL Server a tipos de datos XSD  
 En la tabla siguiente se muestra una asignación obvia de tipos de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a tipos de datos XSD. Si se conoce el tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], esta tabla proporciona el tipo XSD correspondiente que puede especificarse en el esquema XSD.  
  
|Tipo de datos de SQL Server|Tipo de datos XSD|  
|--------------------------|-------------------|  
|**bigint**|**tal**|  
|**binario**|**base64Binary**|  
|**bit**|**boolean**|  
|**char**|**string**|  
|**datetime**|**dateTime**|  
|**decimal**|**decimal**|  
|**float**|**double**|  
|**image**|**base64Binary**|  
|**int**|**int**|  
|**money**|**decimal**|  
|**nchar**|**string**|  
|**nvarchar(max)**|**string**|  
|**nvarchar**|**string**|  
|**numeric**|**decimal**|  
|**real**|**float**|  
|**smalldatetime**|**dateTime**|  
|**smallint**|**short**|  
|**smallmoney**|**decimal**|  
|**sql_variant**|**string**|  
|**sysname**|**string**|  
|**varchar(max)**|**string**|  
|**timestamp**|**dateTime**|  
|**tinyint**|**unsignedByte**|  
|**varbinary**|**base64Binary**|  
|**varchar**|**string**|  
|**uniqueidentifier**|**string**|  
  
## <a name="sqldatatype-annotation"></a>Anotación sql:datatype  
 La anotación **SQL: DataType** se utiliza para especificar el tipo de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]; esta anotación debe especificarse cuando:  
  
-   Está cargando de forma masiva en una columna **datetime**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a partir de un tipo de **fecha**y **hora** ( **DateTime**) xsd. En este caso, debe identificar el tipo de datos de la columna [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante **SQL: DataType = "DateTime"** . Esta regla también se aplica a los diagramas de actualización.  
  
-   Está cargando de forma masiva en una columna de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo **uniqueidentifier** y el valor XSD es un GUID que incluye llaves ({y}). Cuando se especifica **SQL: DataType = "uniqueidentifier"** , las llaves se quitan del valor antes de insertarse en la columna. Si no se especifica **SQL: DataType** , el valor se envía con las llaves y se produce un error en la inserción o la actualización.  
  
-   El tipo de datos XML **base64Binary** se asigna a varios tipos de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (**Binary**, **Image**o **varbinary**). Para asignar el tipo de datos XML **base64Binary** a un tipo de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] específico, use la anotación **SQL: DataType** . Esta anotación especifica el tipo de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] explícito de la columna a la que asigna el atributo. Esto resulta de gran utilidad cuando los datos se almacenan en las bases de datos. Al especificar la anotación **SQL: DataType** , puede identificar el tipo de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] explícito.  
  
 Por lo general, se recomienda especificar **SQL: DataType** en el esquema.  
  
## <a name="examples"></a>Ejemplos  
 Para crear muestras funcionales mediante los ejemplos siguientes, debe cumplir determinados requisitos. Para obtener más información, vea [Requirements for Running SQLXML examples](../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md).  
  
### <a name="a-specifying-xsdtype"></a>A. Especificar xsd:type  
 Este ejemplo muestra cómo un tipo de **fecha** XSD que se especifica mediante el atributo **xsd: Type** en el esquema afecta al documento XML resultante. El esquema proporciona una vista XML de la tabla Sales.SalesOrderHeader de la base de datos AdventureWorks.  
  
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
  
-   Especifica **xsd: Type = Date** en el atributo **OrderDate** , se muestra la parte de fecha del valor devuelto por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para el atributo **OrderDate** .  
  
-   Especifica **xsd: Type = Time** en el atributo **ShipDate** , se muestra la parte de hora del valor devuelto por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para el atributo **ShipDate** .  
  
-   No especifica **xsd: Type** en el atributo **DueDate** , se muestra el mismo valor devuelto por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>Para probar una consulta XPath de ejemplo en el esquema  
  
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

     Para obtener más información, vea [usar ado para ejecutar consultas SQLXML 4,0](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
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
 Para obtener un ejemplo en funcionamiento, vea el ejemplo G en [XML &#40;bulk Load&#41;examples SQLXML 4,0](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/xml-bulk-load-examples-sqlxml-4-0.md). En este ejemplo, se carga de forma masiva un valor GUID que incluye "{" y "}". El esquema de este ejemplo especifica **SQL: DataType** para identificar el tipo de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como **uniqueidentifier**. En este ejemplo se muestra Cuándo **SQL: DataType** debe especificarse en el esquema.  
  
  
