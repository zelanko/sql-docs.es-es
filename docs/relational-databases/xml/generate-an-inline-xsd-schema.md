---
title: Generar un esquema XSD insertado | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- XSD schemas [SQL Server]
- XMLSCHEMA option
- schemas [SQL Server], XML
- XDR schemas
- FOR XML clause, inline XSD schema generation
- inline XSD schema generation [SQL Server]
- XMLDATA option
ms.assetid: 04b35145-1cca-45f4-9eb7-990abf2e647d
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 97b83987abdcc4896ddec0a117b04f629fa8d024
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47603029"
---
# <a name="generate-an-inline-xsd-schema"></a>Generar un esquema XSD insertado
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  En una cláusula FOR XML, se puede solicitar que una consulta devuelva un esquema insertado con los resultados de la consulta. Si se desea un esquema XDR, se utiliza la palabra clave XMLDATA en la cláusula FOR XML. Si se desea un esquema XSD, se utiliza la palabra clave XMLSCHEMA.  
  
 En este tema se describe la palabra clave XMLSCHEMA y se explica la estructura del esquema XSD insertado resultante. A continuación se indican las limitaciones que existen al solicitar esquemas insertados:  
  
-   XMLSCHEMA solo se puede especificar en los modos RAW y AUTO, no en el modo EXPLICIT.  
  
-   Si una consulta FOR XML anidada especifica la directiva TYPE, el resultado de la consulta es de tipo **xml** se trata como una instancia de datos XML sin tipo. Para obtener más información, vea [Datos XML &#40;SQL Server&#41;](../../relational-databases/xml/xml-data-sql-server.md).  
  
 Cuando se especifica XMLSCHEMA en una consulta FOR XML, se reciben un esquema y datos XML, el resultado de la consulta. Cada elemento de nivel superior de los datos hace referencia al esquema anterior por medio de una declaración de espacio de nombres predeterminado que, a su vez, hace referencia al espacio de nombres de destino del esquema insertado.  
  
 Por ejemplo:  
  
```  
<xsd:schema targetNamespace="urn:schemas-microsoft-com:sql:SqlRowSet1" xmlns:schema="urn:schemas-microsoft-com:sql:SqlRowSet1" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:sqltypes="http://schemas.microsoft.com/sqlserver/2004/sqltypes" elementFormDefault="qualified">  
  <xsd:import namespace="http://schemas.microsoft.com/sqlserver/2004/sqltypes" schemaLocation="http://schemas.microsoft.com/sqlserver/2004/sqltypes/sqltypes.xsd" />  
  <xsd:element name="Production.ProductModel">  
    <xsd:complexType>  
      <xsd:attribute name="ProductModelID" type="sqltypes:int" use="required" />  
      <xsd:attribute name="Name" use="required">  
        <xsd:simpleType sqltypes:sqlTypeAlias="[AdventureWorks2012].[dbo].[Name]">  
          <xsd:restriction base="sqltypes:nvarchar" sqltypes:localeId="1033" sqltypes:sqlCompareOptions="IgnoreCase IgnoreKanaType IgnoreWidth" sqltypes:sqlSortId="52">  
            <xsd:maxLength value="50" />  
          </xsd:restriction>  
        </xsd:simpleType>  
      </xsd:attribute>  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
<Production.ProductModel xmlns="urn:schemas-microsoft-com:sql:SqlRowSet1" ProductModelID="1" Name="Classic Vest" />  
```  
  
 Se obtienen el esquema XML y el resultado XML. El elemento de nivel superior <`ProductModel`> del resultado hace referencia al esquema a través de la declaración del espacio de nombres predeterminado, xmlns="urn:schemas-microsoft-com:sql:SqlRowSet1" .  
  
 La parte del resultado que corresponde al esquema puede contener varios documentos de esquema, que describen varios espacios de nombres. Como mínimo se devuelven los dos documentos de esquema siguientes:  
  
-   Un documento de esquema para el espacio de nombres **Sqltypes** , para el que se devuelven los tipos SQL base.  
  
-   Otro documento de esquema que describe la forma del resultado de la consulta FOR XML.  
  
 Asimismo, si se incluyen tipos de datos **xml** con tipo en el resultado de la consulta, se incluyen los esquemas asociados a esos tipos de datos **xml** con tipo.  
  
 El espacio de nombres de destino del documento de esquema que describe la forma del resultado de la consulta FOR XML contiene una parte fija y una parte numérica que se incrementa automáticamente. El formato de este espacio de nombres se muestra a continuación, siendo *n* un entero positivo. Por ejemplo, en la consulta anterior, urn:schemas-microsoft-com:sql:SqlRowSet1 es el espacio de nombres de destino.  
  
```  
urn:schemas-microsoft-com:sql:SqlRowSetn  
```  
  
 Es posible que no se desee el cambio de espacios de nombres de destino que se produce en el resultado obtenido entre una ejecución y otra. Por ejemplo, si se consulta el XML resultante, el cambio del espacio de nombres de destino hará que sea necesario actualizar la consulta. Existe la posibilidad de especificar un espacio de nombres de destino cuando se agrega la opción XMLSCHEMA en la cláusula FOR XML. En ese caso, el XML resultante incluiría el espacio de nombres suministrado, que permanecería invariable con independencia de las veces que se ejecute la consulta.  
  
```  
SELECT ProductModelID, Name  
FROM   Production.ProductModel  
WHERE ProductModelID=1  
FOR XML AUTO, XMLSCHEMA ('MyURI')  
```  
  
## <a name="entity-elements"></a>Elementos de entidad  
 Para explicar los detalles de la estructura del esquema XSD generado para el resultado de la consulta, primero es necesario describir el elemento de entidad.  
  
 Un elemento de entidad de los datos XML devueltos por una consulta FOR XML es un elemento que se genera a partir de una tabla, no a partir de una columna. Por ejemplo, la siguiente consulta FOR XML devuelve información de contacto de la tabla `Person` de la base de datos `AdventureWorks2012` .  
  
```  
SELECT BusinessEntityID, FirstName  
FROM Person.Person  
WHERE BusinessEntityID = 1  
FOR XML AUTO, ELEMENTS  
```  
  
 El resultado es el siguiente:  
  
 `<Person>`  
  
 `<BusinessEntityID>1</BusinessEntityID>`  
  
 `<FirstName>Ken</FirstName>`  
  
 `</Person>`  
  
 En este resultado, <`Person`> es el elemento de entidad. En el resultado XML puede haber varios elementos de entidad, cada uno de los cuales tiene una declaración global en el esquema XSD insertado. Por ejemplo, la consulta siguiente recupera la información de encabezado y los detalles de un pedido de venta específico.  
  
```  
SELECT  SalesOrderHeader.SalesOrderID, ProductID, OrderQty  
FROM    Sales.SalesOrderHeader, Sales.SalesOrderDetail  
WHERE   SalesOrderHeader.SalesOrderID = SalesOrderDetail.SalesOrderID  
AND     SalesOrderHeader.SalesOrderID=5001  
FOR XML AUTO, ELEMENTS, XMLSCHEMA  
```  
  
 Dado que en la consulta se especifica la directiva ELEMENTS, el XML resultante está centrado en elementos. La consulta especifica también la directiva XMLSCHEMA. Por lo tanto, se devuelve un esquema XSD insertado. El resultado es el siguiente:  
  
 `<xsd:schema targetNamespace="urn:schemas-microsoft-com:sql:SqlRowSet1" xmlns:schema="urn:schemas-microsoft-com:sql:SqlRowSet1" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:sqltypes="http://schemas.microsoft.com/sqlserver/2004/sqltypes" elementFormDefault="qualified">`  
  
 `<xsd:import namespace="http://schemas.microsoft.com/sqlserver/2004/sqltypes" schemaLocation="http://schemas.microsoft.com/sqlserver/2004/sqltypes/sqltypes.xsd" />`  
  
 `<xsd:element name="Sales.SalesOrderHeader">`  
  
 `<xsd:complexType>`  
  
 `<xsd:sequence>`  
  
 `<xsd:element name="SalesOrderID" type="sqltypes:int" />`  
  
 `<xsd:element ref="schema:Sales.SalesOrderDetail" minOccurs="0" maxOccurs="unbounded" />`  
  
 `</xsd:sequence>`  
  
 `</xsd:complexType>`  
  
 `</xsd:element>`  
  
 `<xsd:element name="Sales.SalesOrderDetail">`  
  
 `<xsd:complexType>`  
  
 `<xsd:sequence>`  
  
 `<xsd:element name="ProductID" type="sqltypes:int" />`  
  
 `<xsd:element name="OrderQty" type="sqltypes:smallint" />`  
  
 `</xsd:sequence>`  
  
 `</xsd:complexType>`  
  
 `</xsd:element>`  
  
 `</xsd:schema>`  
  
 Observe lo siguiente en la consulta anterior:  
  
-   En el resultado, <`SalesOrderHeader`> y <`SalesOrderDetail`> son elementos de entidad. Por este motivo, se declaran de manera global en el esquema. Dicho de otro modo, la declaración aparece en el nivel superior dentro del elemento <`Schema`>.  
  
-   <`SalesOrderID`>, <`ProductID`> y <`OrderQty`> no son elementos de entidad porque se asignan a columnas. Los datos de columna se devuelven como elementos en el XML, debido a la directiva ELEMENTS. Éstos se asignan a elementos locales del tipo complejo del elemento de entidad. Observe que, si no se especifica la directiva ELEMENTS, los valores `SalesOrderID`, `ProductID` y `OrderQty` se asignan a los atributos locales del tipo complejo del elemento de entidad correspondiente.  
  
## <a name="attribute-name-clashes"></a>Conflictos de nombres de atributos  
 Lo descrito a continuación se basa en las tablas `CustOrder` y `CustOrderDetail` . Para probar los ejemplos siguientes, cree estas tablas y agregue sus propios datos de ejemplo:  
  
```  
CREATE TABLE CustOrder (OrderID int primary key, CustomerID int)  
GO  
CREATE TABLE CustOrderDetail (OrderID int, ProductID int, Qty int)  
GO  
```  
  
 En FOR XML, a veces se utiliza el mismo nombre para indicar diferentes propiedades, atributos. Por ejemplo, la siguiente consulta en modo RAW centrada en atributos genera dos atributos con el mismo nombre, OrderID. Esto genera un error.  
  
```  
SELECT CustOrder.OrderID,   
       CustOrderDetail.ProductID,   
       CustOrderDetail.OrderID  
FROM   dbo.CustOrder, dbo.CustOrderDetail  
WHERE  CustOrder.OrderID = CustOrderDetail.OrderID  
FOR XML RAW, XMLSCHEMA  
```  
  
 Sin embargo, como es aceptable que dos elementos tengan el mismo nombre, el problema desaparece al agregar la directiva ELEMENTS:  
  
```  
SELECT CustOrder.OrderID,  
       CustOrderDetail.ProductID,   
       CustOrderDetail.OrderID  
from   dbo.CustOrder, dbo.CustOrderDetail  
where  CustOrder.OrderID = CustOrderDetail.OrderID  
FOR XML RAW, XMLSCHEMA, ELEMENTS  
```  
  
 Éste es el resultado. Observe que en el esquema XSD insertado, el elemento OrderID se define dos veces. En una de las declaraciones, minOccurs se establece en 0, que se corresponde con el valor de OrderID en la tabla CustOrderDetail, y en la segunda se asigna a la columna de clave principal OrderID de la tabla `CustOrder` , donde minOccurs es 1 de forma predeterminada.  
  
 `<xsd:schema targetNamespace="urn:schemas-microsoft-com:sql:SqlRowSet1" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:sqltypes="http://schemas.microsoft.com/sqlserver/2004/sqltypes" elementFormDefault="qualified">`  
  
 `<xsd:import namespace="http://schemas.microsoft.com/sqlserver/2004/sqltypes" schemaLocation="http://schemas.microsoft.com/sqlserver/2004/sqltypes/sqltypes.xsd" />`  
  
 `<xsd:element name="row">`  
  
 `<xsd:complexType>`  
  
 `<xsd:sequence>`  
  
 `<xsd:element name="OrderID" type="sqltypes:int" />`  
  
 `<xsd:element name="ProductID" type="sqltypes:int" minOccurs="0" />`  
  
 `<xsd:element name="OrderID" type="sqltypes:int" minOccurs="0" />`  
  
 `</xsd:sequence>`  
  
 `</xsd:complexType>`  
  
 `</xsd:element>`  
  
 `</xsd:schema>`  
  
## <a name="element-name-clashes"></a>Conflictos de nombres de elementos  
 En FOR XML se puede utilizar el mismo nombre para indicar dos subelementos. Por ejemplo, la consulta siguiente recupera los valores de ListPrice y DealerPrice de los productos, pero la consulta especifica el mismo alias, Price, para estas dos columnas. Por tanto, el conjunto de resultados obtenido tiene dos columnas con el mismo nombre.  
  
### <a name="case-1-both-subelements-are-nonkey-columns-of-the-same-type-and-can-be-null"></a>Caso 1: ambos subelementos son columnas sin clave, son del mismo tipo y pueden ser NULL  
 En la consulta siguiente, ambos subelementos son columnas sin clave, son del mismo tipo y pueden ser NULL.  
  
```  
DROP TABLE T  
go  
CREATE TABLE T (ProductID int primary key, ListPrice money, DealerPrice money)  
go  
INSERT INTO T values (1, 1.25, null)  
go  
  
SELECT ProductID, ListPrice Price, DealerPrice Price  
FROM   T  
for    XML RAW, ELEMENTS, XMLSCHEMA  
```  
  
 Éste es el XML correspondiente que se genera. Solo se muestra una parte del XSD insertado:  
  
 `…`  
  
 `<xsd:schema targetNamespace="urn:schemas-microsoft-com:sql:SqlRowSet1" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:sqltypes="http://schemas.microsoft.com/sqlserver/2004/sqltypes" elementFormDefault="qualified">`  
  
 `<xsd:import namespace="http://schemas.microsoft.com/sqlserver/2004/sqltypes" />`  
  
 `<xsd:element name="row">`  
  
 `<xsd:complexType>`  
  
 `<xsd:sequence>`  
  
 `<xsd:element name="ProductID" type="sqltypes:int" />`  
  
 `<xsd:element name="Price" type="sqltypes:money" minOccurs="0" maxOccurs="2" />`  
  
 `</xsd:sequence>`  
  
 `</xsd:complexType>`  
  
 `</xsd:element>`  
  
 `</xsd:schema>`  
  
 `<row xmlns="urn:schemas-microsoft-com:sql:SqlRowSet1">`  
  
 `<ProductID>1</ProductID>`  
  
 `<Price>1.2500</Price>`  
  
 `</row>`  
  
 Tenga en cuenta lo siguiente en el esquema XSD insertado:  
  
-   Tanto ListPrice como DealerPrice son del mismo tipo, `money`, y ambos pueden ser NULL en la tabla. Por tanto, como es posible que no se devuelvan en el XML resultante, solo hay un único elemento secundario <`Price`> en la declaración de tipo complejo del elemento <`row`> con minOccurs=0 y maxOccurs=2.  
  
-   En el resultado, como el valor de `DealerPrice` es NULL en la tabla, solo se devuelve `ListPrice` como elemento <`Price`>. Si se agrega el parámetro `XSINIL` a la directiva ELEMENTS, se recibirán los dos elementos que tienen el valor `xsi:nil` establecido en TRUE para el elemento <`Price`> que corresponde a DealerPrice. También se recibirán dos elementos secundarios <`Price`> en la definición de tipo complejo del elemento <`row`> del esquema XSD insertado, con el atributo `nillable` establecido en TRUE para ambos. Este fragmento es un resultado parcial:  
  
 `…`  
  
 `<xsd:schema targetNamespace="urn:schemas-microsoft-com:sql:SqlRowSet1" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:sqltypes="http://schemas.microsoft.com/sqlserver/2004/sqltypes" elementFormDefault="qualified">`  
  
 `<xsd:import namespace="http://schemas.microsoft.com/sqlserver/2004/sqltypes" />`  
  
 `<xsd:element name="row">`  
  
 `<xsd:complexType>`  
  
 `<xsd:sequence>`  
  
 `<xsd:element name="ProductID" type="sqltypes:int" nillable="1" />`  
  
 `<xsd:element name="Price" type="sqltypes:money" nillable="1" />`  
  
 `<xsd:element name="Price" type="sqltypes:money" nillable="1" />`  
  
 `</xsd:sequence>`  
  
 `</xsd:complexType>`  
  
 `</xsd:element>`  
  
 `</xsd:schema>`  
  
 `<row xmlns="urn:schemas-microsoft-com:sql:SqlRowSet1" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">`  
  
 `<ProductID>1</ProductID>`  
  
 `<Price>1.2500</Price>`  
  
 `<Price xsi:nil="true" />`  
  
 `</row>`  
  
### <a name="case-2-one-key-and-one-nonkey-column-of-the-same-type"></a>Caso 2: una columna de clave y una columna sin clave del mismo tipo  
 La siguiente consulta ilustra una columna de clave y una columna sin clave del mismo tipo.  
  
```  
CREATE TABLE T (Col1 int primary key, Col2 int, Col3 nvarchar(20))  
go  
INSERT INTO T VALUES (1, 1, 'test')  
go   
```  
  
 La siguiente consulta en la tabla **T** especifica el mismo alias para Col1 y Col2, donde Col1 es una clave primaria y no puede ser NULL, y Col2 puede ser NULL. Se generan dos elementos del mismo nivel que son elementos secundarios del elemento <`row`>.  
  
```  
SELECT Col1 as Col, Col2 as Col, Col3  
FROM T  
FOR XML RAW, ELEMENTS, XMLSCHEMA  
```  
  
 Éste es el resultado. Solo se muestra un fragmento del esquema XSD insertado.  
  
 `…`  
  
 `<xsd:schema targetNamespace="urn:schemas-microsoft-com:sql:SqlRowSet1" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:sqltypes="http://schemas.microsoft.com/sqlserver/2004/sqltypes" elementFormDefault="qualified">`  
  
 `<xsd:import namespace="http://schemas.microsoft.com/sqlserver/2004/sqltypes" />`  
  
 `<xsd:element name="row">`  
  
 `<xsd:complexType>`  
  
 `<xsd:sequence>`  
  
 `<xsd:element name="Col" type="sqltypes:int" />`  
  
 `<xsd:element name="Col" type="sqltypes:int" minOccurs="0" />`  
  
 `<xsd:element name="Col3" minOccurs="0">`  
  
 `<xsd:simpleType>`  
  
 `<xsd:restriction base="sqltypes:nvarchar"`  
  
 `sqltypes:localeId="1033"`  
  
 `sqltypes:sqlCompareOptions="IgnoreCase`  
  
 `IgnoreKanaType IgnoreWidth"`  
  
 `sqltypes:sqlSortId="52">`  
  
 `<xsd:maxLength value="20" />`  
  
 `</xsd:restriction>`  
  
 `</xsd:simpleType>`  
  
 `</xsd:element>`  
  
 `</xsd:sequence>`  
  
 `</xsd:complexType>`  
  
 `</xsd:element>`  
  
 `</xsd:schema>`  
  
 `<row xmlns="urn:schemas-microsoft-com:sql:SqlRowSet1">`  
  
 `<Col>1</Col>`  
  
 `<Col>1</Col>`  
  
 `<Col3>test</Col3>`  
  
 `</row>`  
  
 Observe que, en el esquema XSD insertado, el elemento <`Col`> que se corresponde con Col2 tiene minOccurs establecido en 0.  
  
### <a name="case-3-both-elements-of-different-types-and-corresponding-columns-can-be-null"></a>Caso 3: los dos elementos son de tipos diferentes y las columnas correspondientes pueden ser NULL  
 La consulta siguiente se especifica utilizando la tabla de ejemplo mostrada en el caso 2:  
  
```  
SELECT Col1, Col2 as Col, Col3 as Col  
FROM T  
FOR XML RAW, ELEMENTS, XMLSCHEMA  
```  
  
 En la consulta siguiente, se asignan los mismos alias a Col2 y Col3. De esta forma se generan dos elementos del mismo nivel, que tienen el mismo nombre y que son elementos secundarios del elemento <`raw`> del resultado. Las dos columnas son de tipos diferentes y pueden ser NULL. Éste es el resultado. Solo se muestra una parte del esquema XSD insertado.  
  
 `…`  
  
 `<xsd:schema targetNamespace="urn:schemas-microsoft-com:sql:SqlRowSet1" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:sqltypes="http://schemas.microsoft.com/sqlserver/2004/sqltypes" elementFormDefault="qualified">`  
  
 `<xsd:import namespace="http://schemas.microsoft.com/sqlserver/2004/sqltypes" />`  
  
 `<xsd:simpleType name="Col1">`  
  
 `<xsd:restriction base="sqltypes:int" />`  
  
 `</xsd:simpleType>`  
  
 `<xsd:simpleType name="Col2">`  
  
 `<xsd:restriction base="sqltypes:nvarchar" sqltypes:localeId="1033"`  
  
 `sqltypes:sqlCompareOptions="IgnoreCase`  
  
 `IgnoreKanaType IgnoreWidth" sqltypes:sqlSortId="52">`  
  
 `<xsd:maxLength value="20" />`  
  
 `</xsd:restriction>`  
  
 `</xsd:simpleType>`  
  
 `<xsd:element name="row">`  
  
 `<xsd:complexType>`  
  
 `<xsd:sequence>`  
  
 `<xsd:element name="Col1" type="sqltypes:int" />`  
  
 `<xsd:element name="Col" minOccurs="0" maxOccurs="2" type="xsd:anySimpleType" />`  
  
 `</xsd:sequence>`  
  
 `</xsd:complexType>`  
  
 `</xsd:element>`  
  
 `</xsd:schema>`  
  
 `<row xmlns="urn:schemas-microsoft-com:sql:SqlRowSet1">`  
  
 `<Col1>1</Col1>`  
  
 `<Col xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"`  
  
 `xsi:type="Col1">1</Col>`  
  
 `<Col xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"`  
  
 `xsi:type="Col2">test</Col>`  
  
 `</row>`  
  
 Tenga en cuenta lo siguiente en el esquema XSD insertado:  
  
-   Dado que Col2 y Col3 pueden ser NULL, la declaración del elemento <`Col`> especifica minOccurs como 0 y maxOccurs como 2.  
  
-   Como los dos elementos <`Col`> están en el mismo nivel, hay una sola declaración de elemento en el esquema. Por otra parte, como los dos elementos son de tipos simples, aunque diferentes, el tipo del elemento es `xsd:anySimpleType` en el esquema. En el resultado, cada tipo de instancia se identifica mediante el atributo `xsi:type`.  
  
-   En el resultado, cada instancia del elemento <`Col`> hace referencia a su tipo de instancia por medio del atributo `xsi:type`.  
  
  
