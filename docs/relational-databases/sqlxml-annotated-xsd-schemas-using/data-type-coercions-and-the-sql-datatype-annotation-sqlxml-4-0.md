---
title: 'Conversiones de tipos de datos y la anotación (SQLXML 4.0) de SQL: DataType | Documentos de Microsoft'
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
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
caps.latest.revision: 29
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 25685856bbb1b088f7c2825e27973915f850dea7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="data-type-coercions-and-the-sqldatatype-annotation-sqlxml-40"></a>Conversión de tipos de datos y la anotación sql:datatype (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  En un esquema XSD, el **xsd: Type** atributo especifica el tipo de datos XSD de un elemento o atributo. Cuando se usa un esquema XSD para extraer datos de la base de datos, el tipo de datos especificado se usa para dar formato a los datos.  
  
 Además de especificar un tipo XSD en un esquema, también puede especificar un Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de datos mediante el uso de la **SQL: DataType** anotación. El **xsd: Type** y **SQL: DataType** atributos controlan la asignación entre los tipos de datos XSD y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de datos.  
  
## <a name="xsdtype-attribute"></a>Atributo xsd:type  
 Puede usar el **xsd: Type** atributo para especificar el tipo de datos XML de un atributo o elemento que se asigna a una columna. El **xsd: Type** afecta al documento que se devuelve desde el servidor y también en la consulta XPath que se ejecuta. Cuando se ejecuta una consulta XPath en un esquema de asignación que contiene **xsd: Type**, XPath utiliza el tipo de datos especificado al procesar la consulta. Para obtener más información acerca de cómo usa XPath **xsd: Type**, consulte [asignación de tipos de datos de XSD a tipos de datos de XPath &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/mapping-xsd-data-types-to-xpath-data-types-sqlxml-4-0.md).  
  
 En un documento devuelto, todos los tipos de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se convierten en representaciones de cadena. Algunos tipos de datos requieren conversiones adicionales. En la tabla siguiente se enumera las conversiones que se usan para distintos **xsd: Type** valores.  
  
|Tipo de datos XSD|Conversión de SQL Server|  
|-------------------|---------------------------|  
|Boolean|CONVERT(bit, COLUMN)|  
|Date|LEFT(CONVERT(nvarchar(4000), COLUMN, 126), 10)|  
|decimal|CONVERT(money, COLUMN)|  
|id/idref/idrefs|id-prefix + CONVERT(nvarchar(4000), COLUMN, 126)|  
|nmtoken/nmtokens|id-prefix + CONVERT(nvarchar(4000), COLUMN, 126)|  
|Time|SUBSTRING(CONVERT(nvarchar(4000), COLUMN, 126), 1+CHARINDEX(N'T', CONVERT(nvarchar(4000), COLUMN, 126)), 24)|  
|Todos los demás|Ninguna conversión adicional|  
  
> [!NOTE]  
>  Algunos de los valores devueltos por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pueden no ser compatibles con los tipos de datos XML que se especifican mediante **xsd: Type**, ya sea porque la conversión no es posible (por ejemplo, convertir "XYZ" en un  **decimal** tipo de datos) o porque el valor supera el intervalo de ese tipo de datos (por ejemplo, -100000 convertido en un **UnsignedShort** tipo XSD). Las conversiones de tipos incompatibles pueden dar lugar a documentos XML no válidos o a errores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="mapping-from-sql-server-data-types-to-xsd-data-types"></a>Asignar tipos de datos SQL Server a tipos de datos XSD  
 En la tabla siguiente se muestra una asignación obvia de tipos de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a tipos de datos XSD. Si se conoce el tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], esta tabla proporciona el tipo XSD correspondiente que puede especificarse en el esquema XSD.  
  
|Tipo de datos de SQL Server|Tipo de datos XSD|  
|--------------------------|-------------------|  
|**bigint**|**Long**|  
|**binario**|**Base64Binary**|  
|**bit**|**boolean**|  
|**char**|**string**|  
|**datetime**|**dateTime**|  
|**decimal**|**decimal**|  
|**float**|**double**|  
|**imagen**|**Base64Binary**|  
|**int**|**int**|  
|**money**|**decimal**|  
|**nchar**|**string**|  
|**ntext**|**string**|  
|**nvarchar**|**string**|  
|**numeric**|**decimal**|  
|**real**|**float**|  
|**smalldatetime**|**dateTime**|  
|**smallint**|**Corto**|  
|**smallmoney**|**decimal**|  
|**sql_variant**|**string**|  
|**sysname**|**string**|  
|**texto**|**string**|  
|**timestamp**|**dateTime**|  
|**tinyint**|**UnsignedByte**|  
|**varbinary**|**Base64Binary**|  
|**varchar**|**string**|  
|**uniqueidentifier**|**string**|  
  
## <a name="sqldatatype-annotation"></a>Anotación sql:datatype  
 El **SQL: DataType** anotación se utiliza para especificar el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de datos; esta anotación debe especificarse cuando:  
  
-   Es la carga masiva en un **dateTime** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] columna desde un XSD **dateTime**, **fecha**, o **tiempo** tipo. En este caso, debe identificar el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de tipo de datos de columna mediante el uso de **SQL: DataType = "dateTime"**. Esta regla también se aplica a los diagramas de actualización.  
  
-   Es la carga masiva en una columna de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **uniqueidentifier** tipo y el valor XSD es un GUID que incluye llaves ({y}). Cuando se especifica **SQL: DataType = "uniqueidentifier"**, las llaves se quitan del valor antes de insertarlo en la columna. Si **SQL: DataType** no se especifica, el valor se envía con las llaves y la inserción o actualización tienen errores.  
  
-   El tipo de datos XML **base64Binary** asigna a varios [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de datos (**binario**, **imagen**, o **varbinary**). Para asignar el tipo de datos XML **base64Binary** a una determinada [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de datos, use la **SQL: DataType** anotación. Esta anotación especifica el tipo de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] explícito de la columna a la que asigna el atributo. Esto resulta de gran utilidad cuando los datos se almacenan en las bases de datos. Mediante la especificación de la **SQL: DataType** anotación, puede identificar el explícita [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de datos.  
  
 En general, se recomienda que especifique **SQL: DataType** en el esquema.  
  
## <a name="examples"></a>Ejemplos  
 Para crear muestras funcionales mediante los ejemplos siguientes, debe cumplir determinados requisitos. Para obtener más información, consulte [requisitos para ejecutar los ejemplos de SQLXML](../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md).  
  
### <a name="a-specifying-xsdtype"></a>A. Especificar xsd:type  
 Este ejemplo se muestra cómo un XSD **fecha** tipo que se especifica mediante la **xsd: Type** atributo en el esquema afecta al documento XML resultante. El esquema proporciona una vista XML de la tabla Sales.SalesOrderHeader de la base de datos AdventureWorks.  
  
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
  
-   Especifica **xsd: Type = fecha** en el **OrderDate** atributo, la parte de fecha del valor devuelto por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para el **OrderDate** se muestra el atributo.  
  
-   Especifica **xsd: Type = tiempo** en el **ShipDate** atributo, la parte de hora del valor devuelto por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para el **ShipDate** se muestra el atributo.  
  
-   No especifique **xsd: Type** en el **DueDate** de atributo, el mismo valor que se devuelve por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se muestra.  
  
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
  
     Para obtener más información, consulte [utilizar ADO para ejecutar consultas de SQLXML 4.0](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
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
  
### <a name="b-specifying-sql-data-type-using-sqldatatype"></a>B. Especificar el tipo de datos SQL usando sql:datatype  
 Para obtener un ejemplo funcional, vea el ejemplo G en [ejemplos de carga masiva XML &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/xml-bulk-load-examples-sqlxml-4-0.md). En este ejemplo, se carga de forma masiva un valor GUID que incluye "{" y "}". Especifica el esquema de este ejemplo **SQL: DataType** para identificar el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de tipo de datos como **uniqueidentifier**. En este ejemplo se muestra cuándo **SQL: DataType** debe especificarse en el esquema.  
  
  
