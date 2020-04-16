---
title: Atributos de ID válidos mediante sql:prefix (SQLXML)
description: Aprenda a crear atributos de tipo ID, IDREF e IDREFS válidos mediante sql:prefix (SQLXML 4.0).
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- IDREFS relationships [SQLXML]
- annotated XSD schemas, ID type attribute
- IDREF type attribute [SQLXML]
- annotated XSD schemas, IDREFS type attribute
- ID type attribute [SQLXML]
- sql:prefix
- prefix annotation
- IDREF relationships [SQLXML]
- IDREFS type attribute [SQLXML]
- annotated XSD schemas, IDREF type attribute
- ID relationships [SQLXML]
ms.assetid: 1c7f77d3-81f3-4820-bb63-c4aaa4ea9aa1
author: MightyPen
ms.author: genemi
ms.reviewer: ''
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 336db1dba88e245492fb4c2e9fcefddb751b59ab
ms.sourcegitcommit: a3f5c3742d85d21f6bde7c6ae133060dcf1ddd44
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/15/2020
ms.locfileid: "81388187"
---
# <a name="creating-valid-id-idref-and-idrefs-type-attributes-using-sqlprefix-sqlxml-40"></a>Crear atributos válidos de tipo ID, IDREF e IDREFS mediante sql:prefix (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Es posible especificar que un atributo sea un atributo de tipo ID. Los atributos especificados como IDREF o IDREFS pueden usarse para hacer referencia a los atributos de tipo ID, lo que habilita los vínculos entre documentos.  
  
 ID, IDREF e IDREFS corresponden a relaciones PK/FK (clave principal/clave externa) de la base de datos, con algunas diferencias. En un documento XML, los valores de los atributos de tipo ID deben ser distintos. Si los atributos **CustomerID** y **OrderID** se especifican como tipo de identificador en un documento XML, estos valores deben ser distintos. Sin embargo, en una base de datos, las columnas CustomerID y OrderID pueden tener los mismos valores. (Por ejemplo, CustomerID = 1 y OrderID = 1 sería válido en la base de datos).  
  
 Para que los atributos ID, IDREFS e IDREF sean válidos:  
  
-   El valor de ID debe ser único dentro del documento XML.  
  
-   Para cada atributo IDREF e IDREFS, los valores de ID a los que se haga referencia deben estar en el documento XML.  
  
-   El valor de un atributo ID, IDREF e IDREFS debe ser un token con nombre. (Por ejemplo, el valor entero 101 no puede ser un valor ID.)  
  
-   Los atributos de tipo ID, IDREF e IDREFS no se pueden asignar a columnas del tipo **text**, **ntext**o **image** o cualquier otro tipo de datos binarios (por ejemplo, **timestamp**).  
  
 Si un documento XML contiene varios identificadores, utilice la anotación **sql:prefix** para asegurarse de que los valores son únicos.  
  
 Tenga en cuenta que la anotación **sql:prefix** no se puede utilizar con el atributo fijo XSD.  
  
## <a name="examples"></a>Ejemplos  
 Para crear muestras funcionales mediante los ejemplos siguientes, debe cumplir determinados requisitos. Para obtener más información, vea [Requisitos para ejecutar ejemplos de SQLXML](../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md).  
  
### <a name="a-specifying-id-and-idrefs-types"></a>A. Especificar tipos ID e IDREFS  
 En el esquema ** \<** siguiente, el elemento Customer>consta de la ** \<>** elemento secundario Order. El ** \<elemento Order>** también tiene un elemento secundario, el ** \<elemento de>OrderDetail.**  
  
 El atributo **OrderIDList** de ** \<Customer>** es un atributo de tipo IDREFS que hace referencia al atributo **OrderID** del ** \<** elemento Order>.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="CustOrders"  
                 parent="Sales.Customer"  
                 parent-key="CustomerID"  
                 child="Sales.SalesOrderHeader"  
                 child-key="CustomerID" />  
    <sql:relationship name="OrderOrderDetail"  
                 parent="Sales.SalesOrderHeader"  
                 parent-key="SalesOrderID"  
                 child="Sales.SalesOrderDetail"  
                 child-key="SalesOrderID" />  
  </xsd:appinfo>  
</xsd:annotation>  
  <xsd:element name="Customer" sql:relation="Sales.Customer" >  
   <xsd:complexType>  
     <xsd:sequence>  
        <xsd:element name="Order" sql:relation="Sales.SalesOrderHeader"    
               sql:relationship="CustOrders" maxOccurs="unbounded" >  
          <xsd:complexType>  
              <xsd:sequence>  
                <xsd:element name="OrderDetail"   
                             sql:relation="Sales.SalesOrderDetail"   
                   sql:relationship="OrderOrderDetail"   
                   maxOccurs="unbounded" >  
                  <xsd:complexType>  
                   <xsd:attribute name="SalesOrderID" type="xsd:integer" />  
                   <xsd:attribute name="ProductID" type="xsd:string" />  
                   <xsd:attribute name="OrderQty" type="xsd:integer" />  
                  </xsd:complexType>  
               </xsd:element>  
             </xsd:sequence>  
             <xsd:attribute name="SalesOrderID"   
                            type="xsd:ID" sql:prefix="ord-" />  
             <xsd:attribute name="OrderDate" type="xsd:date" />  
             <xsd:attribute name="CustomerID" type="xsd:string" />  
          </xsd:complexType>  
      </xsd:element>  
    </xsd:sequence>  
    <xsd:attribute name="CustomerID" type="xsd:string" />  
    <xsd:attribute name="OrderIDList" type="xsd:IDREFS"   
                   sql:relation="Sales.SalesOrderHeader" sql:field="SalesOrderID"  
                   sql:relationship="CustOrders" sql:prefix="ord-">  
    </xsd:attribute>  
  </xsd:complexType>  
</xsd:element>  
</xsd:schema>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>Para probar una consulta XPath de ejemplo con el esquema  
  
1.  Copie el código de esquema anterior y péguelo en un archivo de texto. Guarde el archivo como sqlPrefix.xml.  
  
2.  Copie la plantilla siguiente y péguela en un archivo de texto. Guarde el archivo como sqlPrefixT.xml en el mismo directorio donde guardó sqlPrefix.xml.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="sqlPrefix.xml">  
        /Customer[@CustomerID=1]  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     La ruta de acceso al directorio especificada para el esquema de asignación (sqlPrefix.xml) es relativa al directorio donde se guarda la plantilla. También puede especificarse una ruta de acceso absoluta como, por ejemplo:  
  
    ```  
    mapping-schema="C:\SqlXmlTest\sqlPrefix.xml"  
    ```  
  
3.  Cree y use el script de prueba SQLXML 4.0 (Sqlxml4test.vbs) para ejecutar la plantilla.  
  
     Para obtener más información, consulte Uso de [ADO para ejecutar consultas SQLXML](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Éste es el resultado parcial:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Customer CustomerID="1" OrderIDList="ord-43860 ord-44501 ord-45283 ord-46042">  
    <Order SalesOrderID="ord-43860" OrderDate="2001-08-01" CustomerID="1">  
      <OrderDetail SalesOrderID="43860" ProductID="729" OrderQty="1" />   
      <OrderDetail SalesOrderID="43860" ProductID="732" OrderQty="1" />   
      <OrderDetail SalesOrderID="43860" ProductID="738" OrderQty="1" />   
      <OrderDetail SalesOrderID="43860" ProductID="753" OrderQty="2" />   
      ...  
    </Order>  
    ...  
 </Customer>  
</ROOT>  
```  
  
  
