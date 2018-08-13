---
title: 'SQL: limit-campo y SQL: limit-value (SQLXML 4.0) | Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- limiting values [SQLXML]
- limit-value annotation
- limit-field annotation
- sql:limit-field
- sql:limit-value
- filtering [SQLXML]
ms.assetid: 402c21cf-9566-463f-a928-f94270c11db3
caps.latest.revision: 21
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: bea85f19dde9e91bd62a603bdab4c98031567f3c
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/06/2018
ms.locfileid: "39551155"
---
# <a name="annotation-interpretation---sqllimit-field-and-sqllimit-value"></a>Interpretación de anotaciones: sql:limit-field y sql:limit-value
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Carga masiva XML procesa las anotaciones **sql:limit-field** y **sql:limit-value** por su definición. Para obtener más información, consulte [filtrar valores mediante SQL: limit-campo y SQL: limit-valor &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-using/filtering-values-using-sql-limit-field-and-sql-limit-value-sqlxml-4-0.md).  
  
 Por ejemplo, supongamos que una base de datos contiene las tablas siguientes:  
  
-   Customer (CustomerID, CompanyName)  
  
-   Addresses (CustomerID, StreetAddress, AddressType)  
  
 Un cliente puede tener muchas direcciones y cada dirección tiene un tipo de dirección asociado (por ejemplo, una dirección de envío o una dirección de facturación).  
  
 Ahora considere esta vista XML de estas tablas tal y como se especifica en el siguiente esquema XSD anotado:  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="CustAddr"  
        parent="Customer"  
        parent-key="CustomerID"  
        child="Address"  
        child-key="CustomerID" />  
  </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="Customer" sql:relation="Customer" >  
   <xsd:complexType>  
        <xsd:attribute name="CustomerID"   type="xsd:int" />   
        <xsd:attribute name="CompanyName"  type="xsd:string" />  
        <xsd:attribute name="BillTo"   
                       type="xsd:string"   
                       sql:relation="Address"   
                       sql:field="StreetAddress"  
                       sql:limit-field="AddressType"  
                       sql:limit-value="billing"  
                       sql:relationship="CustAddr" >  
        </xsd:attribute>  
        <xsd:attribute name="ShipTo"   
                       type="xsd:string"   
                       sql:relation="Address"   
                       sql:field="StreetAddress"  
                       sql:limit-field="AddressType"  
                       sql:limit-value="shipping"  
                       sql:relationship="CustAddr" >  
        </xsd:attribute>  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 Al recibir este esquema y estos datos XML, Carga masiva XML inserta el valor que se especifica para el atributo BillTo en la columna StreetAddress de la tabla CustAddress junto con el valor de "facturación" de la columna AddressType.  
  
 De igual forma, Carga masiva XML inserta el valor que se especifica para el atributo ShipTo en la columna StreetAddress junto con el valor de "envío" de la columna AddressType.  
  
### <a name="to-test-a-working-sample"></a>Para probar un ejemplo funcional  
  
1.  Guarde el esquema que se proporciona en este ejemplo como SampleSchema.xml.  
  
2.  Cree estas tablas:  
  
    ```  
    CREATE TABLE Customer(  
                     CustomerID     int         PRIMARY KEY,  
                     CompanyName    varchar(20) NOT NULL)  
    GO  
    CREATE TABLE Address(  
                      CustomerID     int        FOREIGN KEY REFERENCES   
                                                 Customer(CustomerID),   
                      StreetAddress  varchar(50),  
                      AddressType    varchar(10))  
    GO  
    ```  
  
3.  Guarde los siguientes datos de ejemplo como SampleXMLData.xml:  
  
    ```  
    <Customer CustomerID="1111" CompanyName="Sean Chai" City="NY"   
                 BillTo="111 Maple (Billing) "   
                 ShipTo="111 Maple (Shipping)" />  
    <Customer CustomerID="1112" CompanyName="Dont Know" City="LA"   
                 BillTo="222 Spruce (Billing)"   
                 ShipTo="222 Spruce (Shipping)" />  
    ```  
  
4.  Para ejecutar Carga masiva XML, guarde y ejecute este ejemplo de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic Scripting Edition (VBScript) como Sample.vbs:  
  
    ```  
    set objBL = CreateObject("SQLXMLBulkLoad.SQLXMLBulkload.4.0")  
    objBL.ConnectionString = "provider=SQLOLEDB;data source=localhost;database=tempdb;integrated security=SSPI"  
    objBL.ErrorLogFile = "c:\error.log"  
    objBL.XMLFragment = True  
    objBL.CheckConstraints=True  
    objBL.Execute "c:\SampleSchema.xml", "c:\SampleXMLData.xml"  
    set objBL=Nothing  
    ```  
  
 Éste es el esquema XDR equivalente:  
  
```  
<?xml version="1.0" ?>  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"  
        xmlns:dt="urn:schemas-microsoft-com:datatypes"  
        xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  
<ElementType name="Customer" sql:relation="Customer" >  
    <AttributeType name="CustomerID" />  
    <AttributeType name="CompanyName" />  
    <AttributeType name="BillTo" />  
    <AttributeType name="ShipTo" />  
  
    <attribute type="CustomerID" />  
    <attribute type="CompanyName" />  
    <attribute type="BillTo"   
                sql:limit-field="AddressType"  
                sql:limit-value="billing"  
                sql:field="StreetAddress"  
                sql:relation="Address" >  
                <sql:relationship   
                        key="CustomerID"  
                        key-relation="Customer"  
                        foreign-relation="Address"  
                        foreign-key="CustomerID" />  
    </attribute>  
    <attribute type="ShipTo"   
                sql:limit-field="AddressType"  
                sql:limit-value="shipping"  
                sql:field="StreetAddress"  
                sql:relation="Address" >  
                <sql:relationship   
                     key="CustomerID"  
                     key-relation="Customer"  
                     foreign-relation="Address"  
                     foreign-key="CustomerID" />  
    </attribute>  
</ElementType>  
</Schema>  
```  
  
  
